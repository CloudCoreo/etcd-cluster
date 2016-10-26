etcd-cluster
============

This repository is the [CloudCoreo](https://www.cloudcoreo.com) stack for etcd.

## Description
This stack will add a scalable, highly availabe, self healing etcd cluster to your cloud environment based on the [CloudCoreo leader election cluster here](http://hub.cloudcoreo.com/stack/leader-elect-cluster_35519).

etcd is an open sourced, distributed, consistent key-value store from the folks over at CoreOS.

Default values will result in a 3 datacenter deployment behind an internal load balancer addressable via a DNS record. 

## How does it work?
You must provide a route53 dns zone. This will be a CNAME pointing to an internal ELB. The internal ELB will provide healthchecks for the etcd servers and automatically replace failed nodes. The url will be dictated by the variable: `ETCD_CLUSTER_NAME` which defaults to "etcd".

i.e. if your `ETCD_CLUSTER_NAME` is left as the default "etcd", your etcd cluster UI will be available at `http://etcd.<dns_name>`

This is a private ELB so you can only access via VPN or bastion depending on how your network is set up.

When a failure takes place, the Autoscaling group will replace the failed node. The addition of a new node triggers a clean up process to remove stale members of the cluster.

## REQUIRED VARIABLES
### `DNS_ZONE`:
  * description: the dns zone (eg. example.com)
### `VPC_NAME`:
  * description: the cloudcoreo defined vpc to add this cluster to
### `VPC_CIDR`:
  * description: the cloudcoreo defined vpc to add this cluster to
### `PRIVATE_SUBNET_NAME`:
  * description: the private subnet in which the cluster should be added
### `PRIVATE_ROUTE_NAME`:
  * description: the private subnet in which the cluster should be added

## OVERRIDE OPTIONAL VARIABLES
### `VPC_NAME`:
  * description: the cloudcoreo defined vpc to add this cluster to
  * default: dev-vpc
### `VPC_CIDR`:
  * description: the cloudcoreo defined vpc to add this cluster to
  * default: 10.1.0.0/16
### `PRIVATE_SUBNET_NAME`:
  * description: the private subnet in which the cluster should be added
  * default: dev-private-subnet
### `PRIVATE_ROUTE_NAME`:
  * description: the private subnet in which the cluster should be added
  * default: dev-private-route
### `ETCD_PKG_VERSION`:
  * description: etcd version
  * default: 2.2.0
### `ETCD_CLUSTER_NAME`:
  * default: dev-etcd
  * description: the name of the etcd cluster - this will become your dns record too
### `ETCD_ELB_TRAFFIC_PORTS`:
  * default:
  * description: ports that need to allow traffic into the ELB
### `ETCD_ELB_TRAFFIC_CIDRS`:
  * default:
  * description: the cidrs to allow traffic from on the ELB itself
### `ETCD_TCP_HEALTH_CHECK_PORT`:
  * default: 2379
  * description: the tcp port the ELB will check to verify ETCD is running
### `ETCD_CLUSTER_INSTANCE_TRAFFIC_PORTS`:
  * default: 
  * description: ports to allow traffic on directly to the instances
### `ETCD_CLUSTER_INSTANCE_TRAFFIC_CIDRS`:
  * default: 
  * description: cidrs that are allowed to access the instances directly
### `ETCD_INSTANCE_SIZE`:
  * default: t2.small
  * description: the image size to launch
### `ETCD_CLUSTER_SIZE_MIN`:
  * default: 3
  * description: the minimum number of instances to launch
### `ETCD_CLUSTER_SIZE_MAX`:
  * default: 5
  * description: the maxmium number of instances to launch
### `ETCD_INSTANCE_HEALTH_CHECK_GRACE_PERIOD`:
  * default: 600
  * description: the time in seconds to allow for instance to boot before checking health
### `ETCD_CLUSTER_UPGRADE_COOLDOWN`:
  * default: 300
  * description: the time in seconds between rolling instances during an upgrade
### `TIMEZONE`:
  * default: America/Chicago
  * description: the timezone the servers should come up in
### `ETCD_ELB_LISTENERS`:
  * default: >
  * description: The listeners to apply to the ELB
### `ETCD_INSTANCE_KEY_NAME`:
  * default: ""
  * description: the ssh key to associate with the instance(s) - blank will disable ssh
### `DATADOG_KEY`:
  * default: ""
  * description: "If you have a datadog key, enter it here and we will install the agent"
### `ETCD_WAIT_FOR_CLUSTER_MIN`:
  * default: true
  * description: true if the cluster should wait for all instances to be in a running state


## Tags
1. Service Discovery
1. key-value store
1. CoreOS
1. High Availability
1. Shared Configuration

## Categories

1. Servers

## Diagram
![alt text](https://raw.githubusercontent.com/CloudCoreo/etcd-cluster/master/images/etcd-diagram.png "etcd Cluster Diagram")

## Icon
![alt text](https://raw.githubusercontent.com/CloudCoreo/etcd-cluster/master/images/etcd-stacked-color.png "etcd icon")

