---
title: The search for On Premises Container Native Storage
date: 2019-04-15 00:00:00 +0000
categories:
- cloudnative
- kubernetes
tags:
- featured
- sticky
layout: post
author: vamsi
image: "/assets/images/ceph.jpeg"
color: "#C12D2D"

---
Gone are the days where Kubernetes was an exclusive cloud construct. For Enterprises, a viable container strategy that allows them to move applications of all nature on-premises from PoC to production is absolutely indispensable.

Container Native Storage is a key component to ensure enterprises' success in this journey of modernization.

### If Containers are stateless why do they need storage ?

> _Je n’ai fait celle-ci plus longue que parce que je n’ai pas eu le loisir de la faire plus courte. - Charles Babbage

![](../assets/images/CephCharles.jpg)

Roughly translated to

> _I did this longer because I did not have the time to make it shorter._

![](../assets/images/twist.jpeg)

#### Twist it a little

> ##### _Are only **stateless** (parts of) applications suitable for **containerization** ?_

![](../assets/images/twist2.jpeg)

#### Twist it a little further

> ##### _Are **containers** suited to run only **stateless** applications ?_

### Procrastination can't be forever.

In the beginning everything was rosy when containers were merely scratching the surface and the focus was primarily on container scaling and networking .

Then everyone realized that entire applications could not take advantage of containerization because of that one component of that application that needed to manage state.

_Along came the first generation of Persistence support for Containers in form of HostPaths, NFS Mounts etc._

Then came the second wave of volume provisioners and container native storage solutions. But there was barely any focus on on-premises container native storage.

<div class="alert alert-orange mt-5 d-flex align-items-center">
<div>
<span class="align-self-center iconbox iconsmall fill rounded-circle bg-danger text-white shadow border-0 mr-2"><i class="fas fa-bullhorn"></i>
</span>
</div>
This was Barely Sufficient
</div>

### Why ?

Containers move dynamically across different Nodes/ VMs in a clustered environment during their lifecycle.

While data written by the containers onto storage provisioned the conventional way cannot ( Eg.HostPath) so instead of moving data , we need to move volumes and the attachment of volumes across VMs where containers get scheduled.

Even if we do manage to use NFS , the problem is that NFS Mounts need to be created and mounted across every node in the cluster and has to be repeated for every additional node that gets added.

### In Enterprises

This issue gets exacerbated further in enterprises

* There are new applications that are developed on container technologies
* Applications that refuse to move to container technologies and

> #### then there are **_containerized monoliths_**

Containerized monoliths have very strong focus on persistence using share everything and share nothing storage.

* They run in highly restricted environments like DMZs.
* They follow the traditional 3 tier architecture.
* Run on App Servers like Weblogic, Websphere, JBoss etc.
* They communicate to Web Servers, Database servers, Enterprise Service Bus

### Design Considerations for Container Native Storage Solution

**Presentable** : Storage should be presentable to Containers

* Can my containers understand see and write data to the storage solution
* Can the volumes move across VMs freely as containers get rescheduled?

**Declarative**: Should be composable/declarative just like Containers

* Can I define a YAML file / JSON File to provision storage
* Declarative file that allows me to provision storage for my containers

**Flexibility**: One solution to be able to manage both shared nothing and share everything storage architecture from an application standpoint

* Can the same solution spin up block volumes , file storage and object storage for containers

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
* Thin provisioning
* QoS by leveraging my heterogeneous hardware landscape
  * Distribute data across high and low performing hardware
  * Use high and low performance hardware exclusively where needed.

### Dumb Hardware | Smart Software

**_The intelligence of my container native storage solution should arise from Software not hardware_**

> _This makes my storage solution extensible and can co-exist with a heterogeneous storage and compute landscape_

### The Landscape

![](https://i2.wp.com/softwareengineeringdaily.com/wp-content/uploads/2018/09/image1.png)

### Based on the factors evaluated,

A clear winner emerges

* Ceph

#### Why ?

* _Open source and no additional license costs_
* _Backed by a strong community_
* _Battle tested for 10 + years_
* _Distributed and scalable, transparent to application_
* _Supported under Oracle Linux Premier Support Contract_
* _Can work across all types of storage that are presentable to VMs from JBODs to SANs_
* _Supports Striping / Erasure Coding/ HA/ DR/ Encryption_
* _Can provide FSS , Object Storage and Block Volumes to both Docker and Kubernetes through volume provisioners_
* _Hardware / Cloud Vendor Agnostic_
* _Same setup on-premise and on the cloud_
* _Can be extended using Rook to reduce administration overhead on Kubernetes_
* _Can be isolated from the multiple Kubernetes Clusters which is typical in an enterprise environment_

#### What others made it

* Gluster + Heketi

### Further Reading

* [https://www.networkcomputing.com/data-centers/gluster-vs-ceph-open-source-storage-goes-head-head](https://www.networkcomputing.com/data-centers/gluster-vs-ceph-open-source-storage-goes-head-head "https://www.networkcomputing.com/data-centers/gluster-vs-ceph-open-source-storage-goes-head-head")
* [https://medium.com/vescloud/kubernetes-storage-performance-comparison-9e993cb27271](https://medium.com/vescloud/kubernetes-storage-performance-comparison-9e993cb27271 "https://medium.com/vescloud/kubernetes-storage-performance-comparison-9e993cb27271")
* [https://searchstorage.techtarget.com/tip/GlusterFS-vs-Ceph-Weighing-the-open-source-combatants](https://searchstorage.techtarget.com/tip/GlusterFS-vs-Ceph-Weighing-the-open-source-combatants "https://searchstorage.techtarget.com/tip/GlusterFS-vs-Ceph-Weighing-the-open-source-combatants")
* [https://technologyadvice.com/blog/information-technology/ceph-vs-gluster/](https://technologyadvice.com/blog/information-technology/ceph-vs-gluster/ "https://technologyadvice.com/blog/information-technology/ceph-vs-gluster/")