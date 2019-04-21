---
title: Networking is the real reason why enterprises find Kubernetes deployments don't
  scale on-premises
date: 2019-04-21 12:08:00 +05:30
categories:
- kubernetes
- enterprise
- privatecloud
tags:
- featured
author: vamsi
layout: post
---

<u>P.S: I work for Oracle but the views expressed in this article are my own.</u>

Read on if your enterprise Data Center/ IT Landscape has one/many the following characteristics. 

> The one word that sums up your IT Landscape is  "**Heterogenous**"

##### Data Center/ Networking: 

```Markdown
- Your Data Center has the concept of a DMZ/ Trusted and Untrusted Zones/ Internet - Intranet etc implemented using physical and logical networking constructs.  
- You have Core Switches(L3) and Access Switches(L2) tying your data center together
- Your data center and branches are connected through an MPLS , multi-data centers are probably connected with a leased line 
- You have a WAF, perimeter firewall, anti DDOS mostly from different vendors
- Your have a dedicated hardware load balancer/ application delivery controller 
```

##### Infrastructure :

```markdown
- You have a SAN Switch connecting to storage arrays from Hitachi/ Dell-EMC/ Oracle/ HPE
- You have ESXi/ AIX / AHV/ KVM/ OVMs/ Hyper-V in your hypervisor landscape
- You have both Intel and RISC Compute
- You also have recently invested in some kind of HCI ( Hyper Converged Infrastructure )
```

##### Application/DB Landscape : 

```markdown
- Your Database workloads are mostly Oracle, MSSQL, DB2, MySQL
- The majority of your app layer and middleware runs Weblogic, WebSphere, JBOSS, Tomcat
- You only load balance your Web Tier , Web Tier is mostly a reverse proxy
```

Please ignore this article if you have a Software Defined Data Center where you have implemented paradigms like 

```Markdown
- Software Defined Everything
- Infrastructure as Code
- Immutable / Idempotent Configurations
- Git as the source of truth
```

Unless you've been living under a rock, you have read/experienced how container technology is re-defining the enterprise IT.  To simplify it

```markdown
**Docker** /LxC/Kata/Rkt		= VMs
**Kuberneres**/Mesos 			= vSphere/vCenter 
```

If containers are so great, why are enterprises finding it hard to run applications on Kubernetes in production on their data centers ? 

A common sales pitch from vendors that sell  

```markdown
# Myth 1 : 
Open source Kubernetes is hard  
Enterprise Grade Kubernetes is easy
```

The word enterprise-grade Kubernetes is almost a cliche especially when every vendor thinks their baby is the most beautiful. While it is true that some paid solutions make provisioning easier (Some solutions better than the other ) 

> The notion that a managed Kubernetes Service is all you need to attain agility with containers is ridiculous. 

### What is the hardest p



### 

