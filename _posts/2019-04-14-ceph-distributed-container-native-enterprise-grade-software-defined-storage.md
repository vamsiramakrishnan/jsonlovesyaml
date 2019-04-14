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

> Je n’ai fait celle-ci plus longue que parce que je n’ai pas eu le loisir de la faire plus courte.

### Design Considerations for Container Native Storage Solution

1. **Presentable** : Storage should be presentable to Containers 

   > Can my containers understand see and write data to the storage solution
   >
   > Can the volumes move across VMs/ Servers and attach themselves to containers the same way Containers move across VMs / Servers
2. **Declarative**: Should be composable/declarative just like Containers 

   > Can I define a YAML file / JSON File or any declarative file that allows me to provision storage for my containers 
3. **Portable** : Should be just as portable as Containers are, 

   > Can I use the same storage solution for both Docker Swarm and Kubernetes 
   >
   > On-prem Kubernetes and the managed Kubernetes on Cloud
4. **Distributed**: Should follow the same distributed architecture for 

   fault tolerance and scalability

   > Can I increase capacity ? 
   >
   > Distribute data across nodes for performance ?
   >
   > Can I control the number of copies of data retained ?

### Additional Needs for an Enterprise

1. **Security** :  

   > Data encryption at rest and in-motion ?
   >
   > Principles of Role Based Access Control ?
   >
   > Can data encryption be transparent to the application ?
2. **HA/Business Continuity/ QoS:** 

   > 
3. 