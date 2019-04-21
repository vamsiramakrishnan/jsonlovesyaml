---
title: Networking is the real reason why Kubernetes deployments don't scale on-premises
  for enterprises
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

<u>! I work for Oracle and the views expressed in this article are my own.</u>

Read on if your enterprise Data Center/ IT Landscape has one/many the following characteristics.

> The one word that sums up your IT Landscape is  "**Heterogenous**"

##### Data Center/ Networking:

    - Your Data Center has the concept of a DMZ/ Trusted and Untrusted Zones/ Internet - Intranet etc implemented using physical and logical networking constructs.  
    - Core Switches(L3) and Access Switches(L2) tie your data center together 
    - You have a WAF, perimeter firewall, anti DDOS mostly from different vendors
    - Your have a dedicated hardware load-balancer/ application delivery controller 

##### Infrastructure :

    - You have SAN Switches connecting multiple storage arrays from Hitachi/ Dell-EMC
    - You have ESXi/ AIX / AHV/ KVM/ OVMs/ Hyper-V in your hypervisor landscape
    - You have both Intel and RISC Compute

##### Application/DB Landscape :

    - Your Database workloads are mostly Oracle, MSSQL, DB2, MySQL
    - The majority of your app layer and middleware runs Weblogic, WebSphere, JBOSS, Tomcat. 
    - You only load balance your Web Tier 
    - Web Tier is mostly a reverse proxy

### App / Infra Modernization Journey :   

`- You also have recently invested in HCI ( Hyper Converged Infrastructure ) , PaaS `

Some of your net new workloads are demanding a container/cloud native environment within your data center

- You are working on pivoting Service Oriented Architecture/ APIs to leverage and modernize legacy applications

Refactoring  some of 

Please ignore this article if you have a Software Defined Data Center where you have implemented paradigms like

    - Software Defined Everything
    - Infrastructure as Code
    - Immutable / Idempotent Configurations
    - Git as the source of truth

Unless you've been living under a rock, you have read/experienced how container technology is re-defining the enterprise IT.

To simplify it

    Docker/LxC/Kata/Rkt        = VMs
    Kuberneres/Mesos           = vSphere/vCenter 

##### Q1. Will containers work for me ?

**Yes**, they definitely are and can bring in significant benefits. The benefits snowball exponentially

##### Q2. Will containers work for me in my data center on-premises ?

**Yes**, they will, but there are some hurdles to overcome. <u> Read On </u>

##### Q3. If containers are so great, why are enterprises finding it hard to run applications on Kubernetes in production on their data centers ?

DIY Kubernetes is hard and buying an enterprise grade Kubernetes solves all of my day-2 problems

The word enterprise-grade Kubernetes is almost a cliche especially when every vendor thinks their baby is the most beautiful. While it is true that some paid solutions make provisioning easier (Some solutions better than the other )

> The notion that a managed Kubernetes Service is all you need to attain agility with containers is ridiculous.

### What is the hardest p

### 