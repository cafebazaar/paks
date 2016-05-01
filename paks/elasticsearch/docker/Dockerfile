FROM java:openjdk-8-jre-alpine

MAINTAINER Ali Alaee <ali.alaee@gmail.com> (@alialaee)
MAINTAINER Mohammad Nasirifar <far.nasiri.m@gmail.com> (@colonelmo)

EXPOSE 9200 9300

ENV VERSION 2.3.1

RUN apk add --update curl ca-certificates sudo && \

  ( curl -Lskj https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$VERSION/elasticsearch-$VERSION.tar.gz | \
  gunzip -c - | tar xf - ) && \
  mv /elasticsearch-$VERSION /elasticsearch && \
  rm -rf $(find /elasticsearch | egrep "(\.(exe|bat)$|sigar/.*(dll|winnt|x86-linux|solaris|ia64|freebsd|macosx))") && \
  apk del curl

VOLUME ["/data"]

COPY config /elasticsearch/config

ADD do_not_use.yml /elasticsearch/config/elasticsearch.yml
RUN /elasticsearch/bin/plugin install io.fabric8/elasticsearch-cloud-kubernetes/2.3.1 --verbose
RUN /elasticsearch/bin/plugin install royrusso/elasticsearch-HQ --verbose
ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml
COPY run.sh /

CMD ["/run.sh"]
