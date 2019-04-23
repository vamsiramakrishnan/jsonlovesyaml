---
categories:
- appmodernization
- containerization
tags: []
layout: post
title: 'Containerize your Monoliths : Painkillers for the Enterprise '
author: vamsi
image: "/assets/images/monolith.png"
color: "#EE0E0E"
date: 2019-04-23 12:43:53 +0000

---
To many CIOs the promise of microservices is a lot like the promise of heaven. But what about right now ? Life is happening now !!

> How the CIO probably hears your delightful insights on Microservices

![Image result for microservices jokes](http://jonasboner.com/images/posts/bla-bla-microservices-bla-bla/bla_bla_microservices_bla_bla_pdf__page_30_of_31_.png)

> Just because containerizing monoliths fixes some problems quickly and easily, doesn't mean it is a bad solution. 

Functional Decomposition is not a security patch or a scalability hack and is not mandatory. You may need it, you may not. Depends on the scale, speed of software changes, number of players involved, the surgical precision to which you want to scale a part of the application. 

Since most of the enterprise applications run Java-EE Applications, I will speak about them

### How

1. Pick an App 
2. Go to App Server 
3. Find the containerized version of the app server on DockerHub
4. Deploy the containerized version of app server into a Kubernetes Cluster
5. Deploy the JAR/WAR/EAR File like nothing ever changed
6. See if it works
7. Customize and harden your app server 
8. Repeat !

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

![](/assets/images/CattleNotPets.png)

#### Build a strong business case for microservices (if needed) and without an obscenely high bill from your ISV 

> From a software delivery perspective , nothing changes in your build or your / the ISV's build process or architecture

* Your JAR/WAR/EAR is safely wrapped inside the Java EE Application Server 
* You may need the support of your ISV to smoothen some rough edges but it definitely is not re-architecting or re-factoring. 

This approach not only allows you to learn quickly from failures, but also helps you build a case for re-architecting. 