---
categories:
- datastrategy
- enterprise
- microservices
tags:
- sticky
- featured
layout: post
title: Eventually consistent backups mean permanently inconsistent business
author: vamsi
image: ''
color: "#C43A3A"

---
### For the impatient

* Backups from eventually consistent systems are permanently inconsistent and obsolete
* Co-ordinating Backups from distributed systems make it even worse
* The worst is when these backups have to be co-ordinated between disparate databases. 
* Sharing the database between microservices is an anti-pattern but co-ordinating how would one co-ordinate backups across databases 
* Use domain driven design to sensibly isolate and decouple components of business logic that is  mutually exclusive 
* Loosely coupling tightly coupled business entities for the sake of ease of development will make life harder as issues of establishing transactional boundaries and integrity come into play
* BAC Theorem

  > When one backs up data from multiple disparate databases in a microservices architecture it is impossible to have both consistency and availability
* Oracle's Multi Tenant Architecture with Container Database design allows developers to isolate databases and operate pluggable databases as individual databases with independent schemas, tablespaces, users while executing coordinated backups without compromising transactional integrity
* For Linear Horizontal Scalability and fault tolerance with ACID Compliance one may deploy oracle sharding. 

### TL;DR

Designing Microservices the right way can be hard. Defining how one would wish to store and organize data in this decomposed system is the toughest problem to solve.  When the application is broken down into smaller services without mimicking the actual business problem, cracks begin to appear and one ends up doing plumbing with the agile/ devops/ gitops/ noOps or whatever fad methodology it is for the rest of it's life. 

> Bad design is everywhere but with microservices you won't even know what hit you

![](/assets/images/AllureMicroservices.png)

Domain driven design is one of the principles used to define context and boundaries of the application while keeping the overall business transaction in mind.  

![](/assets/images/TransactionalBoundaries.png)

When this is done right, one can say

>  We finally got the Service Oriented Architecture right through microservices. 

However this in itself is a topic for a post in itself. 

In this post I would like to touch upon the complexities a CIO would inherit; in a system that is hastily broken up into microservices and use one database per service a.k.a polyglot persistence 

#### What is polyglot persistence

![](https://i1.wp.com/www.jamesserra.com/wp-content/uploads/2015/04/pp2.png?ssl=1)

The constant argument that we see from developers as the benefit of this architecture

* The failure of one database does not bring app's my availability down. 

Some transactions and businesses have the capacity to be modeled this way but some aren't.  For those applications where consistency is key 

> ##### The failure of One database, will force me to push all other databases back in time in order to recover to a consistent state. If I have managed to take a time-coordinated and consistent backup. 

This is a futuristic microservices application that

* is loosely coupled
* each service is written in a language that is most comfortable for the developer
* runs one specialist database per service if it is NodeJs I use Mongo
* one type of database per service
* is event driven
* asynchronous at all levels

In short it is a lazy developer's dream come true and a nightmare for the team that inherits it for operations and maintenance.

![](/assets/images/sampleApplication.png)

Within its own bounded context ( If it exists ) the database may provide provide strong consistency but when you look at it as an overarching system you would see that there are some obvious problems

How would one back this system up that runs multiple databases from multiple vendors and the onus of co-ordination lies with the application tier. 

### BAC Theorem 

There are two paths that a business can take

* Inconsistent business backups with maximum availability
* Consistent backups but with limited availability

### Inconsistent Business Backups, Maximum Availability

* If the design of the system is such that it is eventually consistent, when I backup I am always at the risk of missing a part of the transaction that is yet to get committed no matter what I do.
* This gets exacerbated when I use multiple databases to split and record  parts of a single business transaction.

> At a given point in time I will always have a backup from at least one of the service that is obsolete

* So when I restore from those backups, I will always restore it to a state that is inconsistent to business.

This is commonplace in a microservices architecture where design is done with failure in mind. If your business is okay with inheriting this system you can get maximum availability with a highly inconsistent business.

Technically we call these

* **Broken Links** :

  Broken links are why we sometimes get an apology email from an e-commerce vendor that they would give us store credits because they went out of stock even after we received an order number and confirmation ( Simplified for understanding )
  1. The order database got updated
  2. The inventory database is just about to get updated
  3. The backup happened before the inventory database got updated
  4. The inventory database gets updated but my backup does not have this information
  5. The system crashed and I restored it
  6. The state of the system is such that my orders database has this information but my inventory database does not.
  7. Another order could get executed against the same item successfully needing a manual reconciliation process or
  8. My application could crash because it does not pass the referential integrity test of the orders database if it is enforced in it.
* **Orphan States :** When the e-commerce vendor sees a discrepancy in the bill against the number of orders that were shipped, he got billed for 6000 additional orders while he only processed 5900 orders that month.
  1. Where the exact opposite of the missing links scenario happens
  2. The orders database gets backed up before it can register

This may be agreeable to some use cases in some businesses, so what if i lost a couple comments and a couple posts in Facebook after recovery ? So what if I did not re-populate my video recommendations completely on Netflix after recovery

### Consistent Business Backups, Limited Availability