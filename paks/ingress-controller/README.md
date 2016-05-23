# Nginx Ingress Controller Pak

Pak of [Nginx Ingress Controller](https://github.com/kubernetes/contrib/tree/master/ingress/controllers/nginx).

## Daemonset
The ingress controller in this pak run as `daemonset`, selecting nodes whith label
`loadbalancer=true`. To add a node to your nginx-ingress-controller loadbalancers:

```
kubectl label nodes <node-name> loadbalancer=true
```

Now you can add the external IP of the node to the set of the IPs for the domains
defined in [ingresses](http://kubernetes.io/docs/user-guide/ingress/) in your cluster.

## Example
```
$ kubectl get ingresses
NAME               RULE                          BACKEND   ADDRESS                       AGE
brcj-brcj1         -                                       192.168.64.13,192.168.64.12   4d
                   brcj.lb.cafebazaar.ir         
                   /                             brcj-brcj1:8000

$ curl -XGET http://brcj.lb.cafebazaar.ir/resources/categories/books/items
{"replyProperties":{"serverVersion":"v0.2"}}
```
