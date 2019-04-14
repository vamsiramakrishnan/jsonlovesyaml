---
categories:
- kubernetes
- cloudnative
tags:
- sticky
layout: post
title: Ceph - Distributed | Container Native | Enterprise Grade | Software Defined
  Storage
author: vamsi
image: "/assets/images/ceph.jpeg"
date: 2019-04-14 21:13:14 +0530

---
    If Containers are stateless why do they need storage ? 

> _Je n’ai fait celle-ci plus longue que parce que je n’ai pas eu le loisir de la faire plus courte. - Charles Babbage_

Roughly translated to 

> _I did this longer because I did not have the time to make it shorter._

### Design Considerations for Container Native Storage Solution

1. **Presentable** : Storage should be presentable to Containers

       Can my containers understand see and write data to the storage solution
       Can the volumes move across VMs freely as containers get rescheduled?
2. **Declarative**: Should be composable/declarative just like Containers

       Can I define a YAML file / JSON File to provision storage
       Declarative file that allows me to provision storage for my containers
3. **Portable** : Should be just as portable as Containers are,

       Can I use the same storage solution for both Docker Swarm and Kubernetes
       On-prem Kubernetes and the managed Kubernetes on Cloud
4. **Distributed**: Should follow the same distributed architecture for

   fault tolerance and scalability

       Can I increase capacity elastically ?
       Distribute data across nodes for performance ?
       Will performace scale with size of cluster ?
       Can I control the number of copies of data retained ?

### Additional Needs for an Enterprise

1. **Security** :

       Data encryption at rest and in-motion ?
       Principles of Role Based Access Control ?
       How do I use existing principles of access control to extend to this storage solution ?
       Can data encryption be transparent to the application ?
2. **Business Continuity/ QoS:**

       Can I take snapshots of the data stored and restore it ?
       How easy is it to replicate it across geographies 
       Make sure I can have fine grained control over How Performant | How much redundancy

   ### Dumb Hardware | Smart Software

   > The intelligence of my container native storage solution should arise from Software not hardware  
   >
   > This makes my storage solution extensible and can co-exist with a heterogeneous storage and compute landscape