---
title: Load Balancing/Networking is the real reason why Enterprises find Kubernetes/Containers deployments On-Premises hard
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

Read on if your enterprise Data Center/ IT Landscape has one/many the following characteristics. The one word that sums up your IT Landscape is  "**Heterogenous**"

```Markdown
Data Center : 
- Your Data Center has the concept of a DMZ and security policies associated with it 
- You have Core Switches(L3) and Access Switches(L2) tying your data center together
- You have a WAF, perimeter firewall, anti DDOS
- You have your 

Infrastructure :
- You have a SAN Switch connecting to storage arrays from Hitachi/ Dell-EMC/ Oracle/ HPE
- You have ESXi/ AIX / AHV/ KVM/ OVMs/ Hyper-V in your hypervisor landscape
- You have both Intel and RISC Compute
- You also have recently invested in some kind of HCI ( Hyper Converged Infrastructure )

Application/DB Landscape : 
- Your Database workloads are mostly Oracle, MSSQL, DB2, MySQL
- The majority of your app layer and middleware runs Weblogic, WebSphere, JBOSS, Tomcat
- You load balance your Web Tier , Web Tier is mostly a reverse proxy
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

The word enterprise-grade Kubernetes is almost a cliche especially when every vendor thinks their baby is the most beautiful. While it is true that some paid solutions like PKS ( Pivotal Kubernetes Service ) and OpenShift make provisioning easier, that is not where the problem really lies

> 

### What is the hardest p



### 

