---
categories:
- kubernetes
- cloudnative
tags:
- sticky
layout: post
title: Ceph - On-Premise Container Native Storage
author: vamsi
image: "/assets/images/ceph.jpeg"
date: 2019-04-14 15:43:14 +0000

---
### If Containers are stateless why do they need storage?

![](/assets/images/Ceph_Charles.jpg)

> _Je n’ai fait celle-ci plus longue que parce que je n’ai pas eu le loisir de la faire plus courte. - Charles Babbage_

Roughly translated to

> _I did this longer because I did not have the time to make it shorter._

#### Twist it a little

> ##### _Are only stateless (parts of) applications suitable for containerization ?_

#### Twist it a little further

> ##### _Are  containers suited to run only stateless applications ?_

### Design Considerations for Container Native Storage Solution

**Presentable** : Storage should be presentable to Containers

* Can my containers understand see and write data to the storage solution
* Can the volumes move across VMs freely as containers get rescheduled?

**Declarative**: Should be composable/declarative just like Containers

* Can I define a YAML file / JSON File to provision storage
* Declarative file that allows me to provision storage for my containers

**Portable** : Should be just as portable as Containers are,

* Can I use the same storage solution for both Docker Swarm and Kubernetes
  On-prem Kubernetes and the managed Kubernetes on Cloud

**Distributed**: Should follow the same distributed architecture for fault tolerance and scalability

* Can I increase capacity elastically ?
* Distribute data across nodes for performance ?
* Will performance scale with size of cluster ?
* Can I control the number of copies of data retained ?

### Additional Needs for an Enterprise

**Security** :

* Data encryption at rest and in-motion ?
* Principles of Role Based Access Control ?
* How do I use existing principles of access control to extend to this storage solution ?
* Can data encryption be transparent to the application ?

**Business Continuity/ QoS:**

* Can I take snapshots of the data stored and restore it ?
* How easy is it to replicate it across geographies  
* Make sure I can have fine grained control over number of copies | which part of my hardware 
* Thin provisioning

### Dumb Hardware | Smart Software

* The intelligence of my container native storage solution should arise from Software not hardware
* This makes my storage solution extensible and can co-exist with a heterogeneous storage and compute landscape