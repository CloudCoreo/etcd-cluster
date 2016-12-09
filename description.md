This stack will add a scalable, highly availabe, self healing etcd cluster to your cloud environment based on the [CloudCoreo leader election cluster here](http://hub.cloudcoreo.com/stack/leader-elect-cluster&#95;35519).

etcd is an open sourced, distributed, consistent key-value store from the folks over at CoreOS.

Default values will result in a 3 datacenter deployment behind an internal load balancer addressable via a DNS record. 

## How does it work?
You must provide a route53 dns zone. This will be a CNAME pointing to an internal ELB. The internal ELB will provide healthchecks for the etcd servers and automatically replace failed nodes. The url will be dictated by the variable: `ETCD&#95;CLUSTER&#95;NAME` which defaults to "etcd".

i.e. if your `ETCD&#95;CLUSTER&#95;NAME` is left as the default "etcd", your etcd cluster UI will be available at `http://etcd.<dns&#95;name>`

This is a private ELB so you can only access via VPN or bastion depending on how your network is set up.

When a failure takes place, the Autoscaling group will replace the failed node. The addition of a new node triggers a clean up process to remove stale members of the cluster.
