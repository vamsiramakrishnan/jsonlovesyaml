---
categories:
- devops
- oci
tags:
- featured
layout: post
title: DevOps on Steroids with Oracle Stack
author: vamsi
image: "/uploads/devopsintro.jpeg"
date: 2019-04-14 08:01:52 +0000

---
An article on hyper-optimization of Continuous Integration and Delivery. This article outlines

* The motivation for DevOps
* Describes the design philosophy, history, and, evolution of these principles

The second part to this article is a tutorial on its ease of implementation on Oracle Cloud

#### For the Impatient

Jump straight to the [tutorial](https://medium.com/jsonlovesyaml/devops-on-steroids-with-oracle-kubernetes-engine-oracle-developer-cloud-service-73886b70e715)

#### Why DevOps

> Every IT Organization fighting battles that are flavors of these four fundamental problems. DevOps provides ways and means to reach the light at the end of this tunnel

![](https://cdn-images-1.medium.com/max/1500/0*6q__EJ_wPVWQRIYt.png)

#### Infographics to help understand what DevOps can help you accomplish

![](https://cdn-images-1.medium.com/max/1500/0*87Uhj89jW8q82zO4.png)

Source : Oracle ACE

![](https://cdn-images-1.medium.com/max/1500/0*hoWdmMedYz_oLbUM.png)

Source: Sherweb

#### How did DevOps come into being

The origin of DevOps is debatable but a large group of the audience seems to agree on this version. ([Source](https://devops.com/the-origins-of-devops-whats-in-a-name/))

* At the Agile Conference in Toronto in 2008, Andrew Schafer offered to moderate a meeting titled “Agile Infrastructure.”  
  In the same year, Debois and Shafer formed an Agile Systems Administrator group on Google.
* At the O’Reilly Velocity Conference in 2009, John Allspaw, and Paul Hammond delivered a presentation titled “10+ Deploys per Day.”
* In the year 2013, “The Phoenix Project,” written by Gene Kim, Kevin Behr, and George Spafford. This fictional novel tells the story of an IT manager thrust into a hopeless situation. He’s charged with salvaging a mission-critical e-commerce development project.

#### What inspired DevOps

DevOps draws inspiration from the Toyota Production System, by Taiichi Ohno. ([Source](http://william.holroyd.name/2014/10/13/using-the-toyota-production-system-to-explain-devops/))

![](https://cdn-images-1.medium.com/max/1500/0*OMDAUpG_TEzBo4V4.png)

#### Basic Building Blocks for DevOps at Scale

The scope of DevOps goes way beyond a set of principles and tools. In this article, I will focus on the toolchain and how they align well with DevOps principles

![](https://cdn-images-1.medium.com/max/1500/0*S7dI39JdaRVZLFsG.png)

#### Pillars for DevOps at Planet Scale

![](https://cdn-images-1.medium.com/max/1500/1*5yGJNJgI7sx_et7OIq9KtQ.png)

### Immutable/Idempotent Infrastructure

The motivation to have immutable and idempotent infrastructure arises from these problems

#### Snowflake Servers

    Configuring a Snowflake Server Requires: 
    --> Multi-language command line invocations(Bash, Python, Manual file copies) --> Frequent jumping between GUI screens  
    --> Order of execution is SysAdmin artistry 
    --> Ad-hoc changes
    --> Documented in Email, Excel and Word 

![](https://cdn-images-1.medium.com/max/1500/1*FP3HEfgaFy5BzSsJN5JPpw.png)

Credit: Martin Fowler — Snowflake Server

> “Avoid Snowflake servers like the plague”

#### Pet Servers

    What are our priorities for Pet Servers:
    --> Longevity
    --> Interdependencies
    --> Centralization 
    --> Scale up

> ## “We need cattle not pets”

    Priorities for Cattle Servers:
    --> Disposability
    --> Isolation
    --> Decomposition
    --> Scale Out 

![](https://cdn-images-1.medium.com/max/1500/0*AvOYZkQ-zCsJwC4-.png)

> **_Idempotency_** is a solution to handle snowflake servers

> Immutability is a solution to handle pet servers

#### What is Idempotency

    State drives changes in the system and the system's state is maintained.
    
    Step 1: Declaration of Desired State Step 2: Path to attain Desired StateStep 3: Convergence to Desired State Step 4: Maintenance of Desired State

#### What is Immutability

    Create Read Update Delete (CRUD) ---> Create Read and Delete (CRD)* Immaterial of the number of App Release and Configuration Change Iterations

![](https://cdn-images-1.medium.com/max/1500/0*TeYgG5lODGO_-g9B)

#### Attain Idempotency and Immutability through Infrastructure as Code

Infrastructure is described as code, versioned, and is an essential part of your baseline

![](https://cdn-images-1.medium.com/max/1500/0*r96kS4gDQsSD7FCa.png)

Puppet Blog

### Re-imagine deployments

Courtesy: [(Link)](https://blog.armory.io/advanced-deployment-strategies-with-armory-spinnaker/)

    From Release == Risk of Failure to Release == Reduce Risk of Failure

> Deploy Often | Deploy Fast | Deploy Safe

#### **What are the options:**

![](https://cdn-images-1.medium.com/max/1500/1*To2aLVNxO04PaJxi-ZS_MA.png)

Highlander Deployments

    1) Highlander: Named after the movie, You can only have one at a time* Method: Upgrade all versions of old deployment to the new one at the same time.* Pros: Simplest Strategy * Cons: Slow Rollback speed, Application downtime required

![](https://cdn-images-1.medium.com/max/1500/0*8Ox3t_t-SWoqMKql.png)

Blue Green | Rolling Blue-Green | Canary deployments

    2) Blue/Green:* Method: Create new deployment in parallel, switch over on Load Balancer* Pros: Atomic deployment, One at a time, faster roll back* Cons: Full-throttle traffic could overwhelm application instances where there is no cache build-up.
    
    3) Rolling Blue/Green: * Method: Similar to Blue/Green, variation in traffic switch over rates* Pros: The new application is load tested on real workloads before complete switch-over* Cons: The application must support two different versions running at once.
    
    4) Canary Deployments:* Method: Layered rolling blue-green deployment with defined pass/fail metrics* Pros:   Limits the blast radius to a small percentage of your user-base
    
    5) Shadow Deployments:* Method:  Strategy forwards traffic to both versions without impacting users* Pros: New version undergoes battle tested production workload test* Cons: Complicated to set up and requires extra infrastructure

### Version everything

DevOps heavily depends on the ability to execute fast fail-overs to a known, stable state.

> So Version Everything !

    1) Application code2) Infrastructure3) Configurations4) Data 5) Systems

#### What do I need !!

    Highly Performant , Fault-Tolerant, Scaleable Cloud Infra Oracle Cloud Infrastructure 
    
    1) CI/CD - Oracle Container Pipelines + Spinnaker2) Container Technology - Docker 3) Container Orchestration - Oracle Kubernetes Engine4) Container Native Package Management - Helm5) Artifact Repository + Services - Oracle Developer Cloud Service6) Infrastructure as Code - Terraform + Chef/Puppet/SaltStack

### Let’s talk IT

#### A glimpse into history, past and present

The 2004 vs 2013 — Interpretations of Hyperscale and Velocity in IT

2013 vs 2018 — Interpretations of Hyperscale and Velocity in IT

**A little unbelievable ?**

Click on Run Pen to see the interest in Kubernetes and vSphere over time

#### More proof ahead

![](https://cdn-images-1.medium.com/max/1500/0*L8nqb3HtTbuX_0dy.png)

![](https://cdn-images-1.medium.com/max/1500/0*_LAk3NYuzBsJuSRg.png)

#### A Brief History of Kubernetes

Inspiration to this timeline graphic in [Link](https://blog.risingstack.com/the-history-of-kubernetes/), Swipe right and left to navigate.

#### What is Helm

![](https://cdn-images-1.medium.com/max/1500/0*-NFv_dldehq3-Kj0.jpg)

![](https://cdn-images-1.medium.com/max/1500/0*r3foVxS9GpLp0OoI.jpg)

#### A Brief History of Helm

![](https://cdn-images-1.medium.com/max/1500/0*jyQRjJodnhiwzenq.png)

Source: [https://www.cncf.io/blog/2018/08/07/helm-the-package-manager-for-kubernetes/#](https://www.cncf.io/blog/2018/08/07/helm-the-package-manager-for-kubernetes/# "https://www.cncf.io/blog/2018/08/07/helm-the-package-manager-for-kubernetes/#")

#### Why Helm

    Kubernetes manifests are hard to manage

* Deliver and manage applications, not Kubernetes manifests.
* Tweak Kubernetes manifests based on deployment targets .

#### Go one step Further with Monocular:

Monocular is Helm + Black Magic ( Web UI ) that renders a UI based approach to manage Helm Deployments.

Works well with both internet accessible and air-gapped setups. Other capabilities include

* Browsing Repositories and Charts
* One Click Deployment of Charts
* A view of Existing deployments

#### What is Wercker

* Wercker is a CI/CD developer automation platform designed for Microservices & Container Architecture.
* Wercker uses pipelines / [automated workflows](https://en.wikipedia.org/wiki/Workflow_application). Pipelines take pieces of code any execute a series of steps upon that code.
* Refer to this [blogpost ](https://medium.com/jsonlovesyaml/ci-cd-simplified-with-wercker-kubernetes-on-oracle-cloud-infrastructure-a2332497d36f)for more on [Wercker](https://app.wercker.com/) and its role in CI/CD

![](https://cdn-images-1.medium.com/max/1500/0*Of5fpTWmKKpnyBOz.png)

#### What is Spinnaker

* Spinnaker is a cloud native continuous deployment tool
* Developed and battle-tested by Netflix, recently open-sourced

#### Why do I need Spinnaker if I already have the other tools

Spinnaker integrates with all tools mentioned earlier, assuming the role of a centralized task manager.

![](https://cdn-images-1.medium.com/max/1500/1*5-sSOGbTCPQunNPAjHZeug.png)

Stay tuned for the tutorial.

Please leave your thoughts below