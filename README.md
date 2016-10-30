audit RDS
============================
This stack will monitor RDS and alert on things CloudCoreo developers think are violations of best practices


## Description
This repo is designed to work with CloudCoreo. It will monitor RDS against best practices for you and send a report to the email address designated by the config.yaml AUDIT&#95;AWS&#95;RDS&#95;ALERT&#95;RECIPIENT value


## Hierarchy
![composite inheritance hierarchy](https://raw.githubusercontent.com/CloudCoreo/etcd-cluster/master/images/hierarchy.png "composite inheritance hierarchy")



## Required variables with no default

### `DNS_ZONE`:
  * description: the dns zone (eg. example.com)

### `ETCD_CLUSTER_AMI`:
  * description: the ami to launch for the etcd cluster - default is Amazon Linux AMI 2015.03 (HVM), SSD Volume Type


## Required variables with default

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
  * description: the name of the etcd cluster - this will become your dns record too
  * default: dev-etcd

### `ETCD_ELB_TRAFFIC_PORTS`:
  * description: ports that need to allow traffic into the ELB
  * default: 94b, 94c

### `ETCD_ELB_TRAFFIC_CIDRS`:
  * description: the cidrs to allow traffic from on the ELB itself
  * default: 10.0.0.0/8

### `ETCD_TCP_HEALTH_CHECK_PORT`:
  * description: the tcp port the ELB will check to verify ETCD is running
  * default: 2379

### `ETCD_CLUSTER_INSTANCE_TRAFFIC_PORTS`:
  * description: ports to allow traffic on directly to the instances
  * default: 94b, 94c, 16

### `ETCD_CLUSTER_INSTANCE_TRAFFIC_CIDRS`:
  * description: cidrs that are allowed to access the instances directly
  * default: 10.0.0.0/8

### `ETCD_INSTANCE_SIZE`:
  * description: the image size to launch
  * default: t2.small


### `ETCD_CLUSTER_SIZE_MIN`:
  * description: the minimum number of instances to launch
  * default: 3

### `ETCD_CLUSTER_SIZE_MAX`:
  * description: the maxmium number of instances to launch
  * default: 5

### `ETCD_INSTANCE_HEALTH_CHECK_GRACE_PERIOD`:
  * description: the time in seconds to allow for instance to boot before checking health
  * default: 600

### `ETCD_CLUSTER_UPGRADE_COOLDOWN`:
  * description: the time in seconds between rolling instances during an upgrade
  * default: 300

### `TIMEZONE`:
  * description: the timezone the servers should come up in
  * default: America/Chicago



## Optional variables with no default

### `ETCD_ELB_LISTENERS`:
  * description: The listeners to apply to the ELB
  * default: 
```
[
  {
      :elb_protocol => 'tcp',
      :elb_port => 2379,
      :to_protocol => 'tcp',
      :to_port => 2379
  },
  {
      :elb_protocol => 'tcp',
      :elb_port => 2380,
      :to_protocol => 'tcp',
      :to_port => 2380
  }
]

```

### `DATADOG_KEY`:
  * description: If you have a datadog key, enter it here and we will install the agent
  * default: 


### `ETCD_WAIT_FOR_CLUSTER_MIN`:
  * description: true if the cluster should wait for all instances to be in a running state
  * default: true


## Optional variables with default

### `VPC_SEARCH_TAGS`:
  * description: if you have more than one VPC with the same CIDR, and it is not under CloudCoreo control, we need a way to find it. Enter some unique tags that exist on the VPC you want us to find. ['env=production','Name=prod-vpc']

### `PRIVATE_ROUTE_SEARCH_TAGS`:
  * description: if you more than one route table or set of route tables, and it is not under CloudCoreo control, we need a way to find it. Enter some unique tags that exist on your route tables you want us to find. i.e. ['Name=my-private-routetable','env=dev']

### `PRIVATE_SUBNET_SEARCH_TAGS`:
  * description: Usually the private-routetable association is enough for us to find the subnets you need, but if you have more than one subnet, we may need a way to find them. unique tags is a great way. enter them there. i.e. ['Name=my-private-subnet']

### `ETCD_INSTANCE_KEY_NAME`:
  * description: the ssh key to associate with the instance(s) - blank will disable ssh

## Tags
1. Audit
1. Best Practices
1. Alert
1. RDS

## Categories
1. Audit



## Diagram
![diagram](https://raw.githubusercontent.com/CloudCoreo/etcd-cluster/master/images/diagram.png "diagram")


## Icon


