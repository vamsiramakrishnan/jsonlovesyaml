---
layout: post
title: The search for On Premises Container Native Storage
author: vamsi
categories:
- cloudnative
- kubernetes
tags:
- sticky
image: "/assets/images/ceph.jpeg"
color: "#C12D2D"

---
### If Containers are stateless why do they need storage ?

> _Je n’ai fait celle-ci plus longue que parce que je n’ai pas eu le loisir de la faire plus courte. - Charles Babbage

![](/assets/images/CephCharles.jpg)

Roughly translated to

> _I did this longer because I did not have the time to make it shorter._

![](/assets/images/twist.jpeg)

#### Twist it a little

> ##### _Are only stateless (parts of) applications suitable for containerization ?_

![](/assets/images/twist2.jpeg)

#### Twist it a little further

> ##### _Are containers suited to run only stateless applications ?_

### Procrastination can't be forever.

In the beginning everything was rosy when containers were merely scratching the surface and the focus was primarily on container scaling and networking .

Then everyone realized that entire applications could not take advantage of containerization because of that one component of that application that needed to manage state.

> _Along came the first generation of Persistence support for Containers in form of HostPaths, NFS Mounts etc._

**_This was barely sufficient_**

### Why ?

### In Enterprises

* There are new applications that are developed on container technologies
* Applications that refuse to move to container technologies and

> #### then there are **_containerized monoliths_**

Containerized monoliths have very strong focus on persistence using share everything and share nothing storage.

![](https://i2.wp.com/softwareengineeringdaily.com/wp-content/uploads/2018/09/image1.png)

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

**_The intelligence of my container native storage solution should arise from Software not hardware_**

> _This makes my storage solution extensible and can co-exist with a heterogeneous storage and compute landscape_