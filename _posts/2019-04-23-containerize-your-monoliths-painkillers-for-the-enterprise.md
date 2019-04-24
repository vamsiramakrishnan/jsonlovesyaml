---
categories:
- appmodernization
- containerization
tags: []
layout: post
title: 'Containerized Monoliths : Painkillers for the Enterprise '
author: vamsi
image: "/assets/images/monolith.png"
color: "#EE0E0E"
date: 2019-04-23 12:43:53 +0000

---
### The promise of microservices to the CIO of a large enterprise is a lot like the promise of heaven after death.

### But what about right now ? Life is happening now !!

> How the CIO probably hears your delightful insights on Microservices

![Image result for microservices jokes](http://jonasboner.com/images/posts/bla-bla-microservices-bla-bla/bla_bla_microservices_bla_bla_pdf__page_30_of_31_.png)

> Just because containerizing monoliths fixes some problems quickly and easily, doesn't mean it is a bad solution.

* Functional Decomposition is not a security patch or a scalability hack and is not mandatory.
* You may need it, you may not.
* The need depends on the scale, velocity of software changes, the surgical precision to which you want to scale a part of the application.

Since most of the enterprise applications run Java-EE Applications, I will speak about them

### How

1. Pick an Application and get to know what app server it runs on
2. Find the containerized version of the app server on DockerHub
3. Deploy the containerized version of app server into a Kubernetes Cluster
4. Deploy the JAR/WAR/EAR File like nothing ever changed
5. See if it works
6. Customize and harden your app server
7. Repeat !

### Containerizing monoliths within an enterprise help me solve ..

#### The Scaling problem

* Functional decomposition a.k.a Microservices is not for all applications and it only helps one traverse one axis in the scaling cube

  ![Image result for Scale Up Scale Out Functional Decomposition](https://cdn-images-1.medium.com/max/1200/0*0N5pwzzvtQ94DzJN.png)
* Containerizing your monolith can still help you scale horizontally a.k.a create multiple copies of the same application faster.

#### Enforce portability across environments and make them platform agnostic, reduce vendor lock-in

* Allows Infra and OS Teams to simply homogenize and standardize their OS, Servers, help realize better economics of scale.
* In other words you won't have that one fussy app server demanding a certain version of the OS provided by that vendor on the hardware that is sold by the same vendor that makes the app server.
* Your UAT containers will run the exact same way it runs on a developer PC and on production .

In simple words

> No more snowflakes, Only Cattle Not Pets

![](./assets/images/CattleNotPets.png)

#### Build a strong business case for microservices (if needed) and bypass an obscenely high bill from your ISV

> From a software delivery perspective , nothing changes in your build or your / the ISV's build process or architecture

* Your JAR/WAR/EAR is safely wrapped inside the Java EE Application Server
* You may need the support of your ISV to smoothen some rough edges but it definitely is not re-architecting or re-factoring.

This approach not only allows you to learn quickly from failures, but also helps you build a case for re-architecting.

### Pitfalls to watch out for

> Not all App Servers are born equal

* You may or may not find your application server's containerized version.
* Sometimes you may not find the full feature set in the containerized version
* Sometimes these containerized versions may not be supported / recommended for production.

### Other concerns that enterprises usually have 

* _Sounds great but who will certify and support Kubernetes issues ?_ 

  Oracle Linux Premier support covers all CNCF components which include both Docker and Kubernetes 
* _Do I need special tools for monitoring and alerting the Kubernetes Cluster ?_

  If your existing monitoring solution has an add on for kubernetes you could use that , or you could use Prometheus and Grafana and integrate it with Nagios for eg. or use the alert manager from Prometheus itself. 

### Solutions to these pitfalls

* **Weblogic on Kubernetes** is a production ready, full feature-set  Java EE server available for use.
* Oracle has also released a containerized version of **Coherence**
* You can easily address the movement of the **caching layer** into Kubernetes. 
* It has also released an **operator pattern** to simplify domain based deployments on Kubernetes

There will be a follow up technology deep dive post elaborating the steps to follow exactly would you containerise 