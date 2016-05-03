FROM java:8-jre

MAINTAINER Ali Alaee <ali.alaee@gmail.com> (@alialaee)
MAINTAINER Mohammad Nasirifar <far.nasiri.m@gmail.com> (@colonelmo)

EXPOSE 9200 9300

ENV VERSION 2.3.1

RUN curl --progress https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$VERSION/elasticsearch-$VERSION.tar.gz -o /elasticsearch.tar.gz
RUN tar -xf /elasticsearch.tar.gz && rm /elasticsearch.tar.gz && mv /elasticsearch-$VERSION /elasticsearch

VOLUME ["/data"]

COPY config /elasticsearch/config

ADD do_not_use.yml /elasticsearch/config/elasticsearch.yml
RUN /elasticsearch/bin/plugin install io.fabric8/elasticsearch-cloud-kubernetes/2.3.1 --verbose
RUN /elasticsearch/bin/plugin install royrusso/elasticsearch-HQ --verbose
ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml
COPY run.sh /

CMD ["/run.sh"]
