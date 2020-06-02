---
title: Low Cost Serverless Splunk Exporter
date: '2019-04-14T13:21:00.000+00:00'
categories:
- serverless
- oci
- splunk
tags:
- featured
layout: post
author: vamsi
image: "/assets/images/photo-of-stream-during-daytime-3225517.jpg"
color: "#D33535"

---
# Delivering a low-cost, scalable, audit events pipeline to a SIEM (Splunk | QRadar ) from Oracle…

Splunk is a SIEM tool used for Security Analytics. The article outlines the choice of components from Oracle Cloud Infrastructure to stream logs from Oracle Cloud Infrastructure to Splunk. Below are some data points

![](https://cdn-images-1.medium.com/max/2250/0*GVCBf2vDeJDaePI_)

![](https://cdn-images-1.medium.com/max/2656/1*a3LDbDpdQiIup-Zg1sfKvQ.png)

    ------------------------
    STATISTICS
    ------------------------
    
    Number of Data Centers / Regions in Tenancy - 4 Regions
    Number of Compartments in each Region       - 96 Compartments
    Number of Federated Users                   - 82 Users
    Number of Resources audited in tenancy      - 1921 Resources
    
    {'region': 'ap-mumbai-1', 'resource_count': 827}
    {'region': 'eu-frankfurt-1', 'resource_count': 342}
    {'region': 'us-phoenix-1', 'resource_count': 752}
    
    Number of Audit events generated / day      - 1 Mio. + Events

![](https://cdn-images-1.medium.com/max/2000/1*UjFLMhVCDVqpqsMi01HbHw.png)

    Overall Cost/Month        $
    ------------------------------
    Oracle Health Checks  - 0.3 $
    Oracle API-Gateway    - 3.0 $
    Oracle Notifications  - 1.2 $
    Oracle Functions      - 3.0 $
    Oracle Streaming      - 2.0 $
    -------------------------------
    Overall Cost          ~ 10 $
    -------------------------------

## For the Impatient

Link to the source code and implementation tutorial for those who know what this means and just wants to get this working.
[vamsiramakrishnan/splunk-export-audit
\*For Integrated SecOps , the SIEM plays an important component and Splunk is a very popular SIEM solution. The setup…*github.com](https://github.com/vamsiramakrishnan/splunk-export-audit)

## For the others — What is a SIEM

SIEM Stands for

    (S)ecurity (I)nformation & (E)vent (M)anagement

> # Think of the SIEM as a single source of truth for all kinds of Security Events.

For table stakes, what a SIEM will have for sure are

    1) Event Ingestion
    ----------------
    Logs/ Events from multiple sources, Network - Subnets, Gateways, Load Balancers, Firewalls, WAFs, Identity Systems - Auth, Configuration Logs etc.
    
    2) Event Processing
    ----------------
    Event Processing is mostly log parsing & enriching log data into a searchable and indexable format.
    
    1) Event Indexing & Search
    ---------------------------
    A Combination of In-Memory, Relational, Document oriented data persistence and archiving layers to provide search functionality.
    
    1) Pattern Building for Correlation
    ------------------------------------
    All the components mentioned above are pre-requisites , this is where the SIEM actually provides benefits correlating between multiple events.
    
    1) Analytics
    -------------
    A Series of dashboards, reports ad-hoc and periodic reporting

— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — —

_This article focusses on getting OCI AuditEvents to that single source of truth for security as soon as possible, at the lowest cost, in a pay-per-use pattern and can scale massively._

— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — —

### SIEM Trivia — Security Experts please skip.

> # The SIEM was born out of a necessity to reduce the complexity of correlating logs from multiple Intrusion Detection & Prevention Systems — Firewall Appliances, Switches, Routers etc.

SIEMs as an initiative became mainstream at the majority of institutions started off as a compliance-driven initiative and then evolved to become a fully functional SOAR.

![Stages of SIEM Implementation](https://cdn-images-1.medium.com/max/2892/1*pWecLe9G2jGwrF_Er1ZKww.png)_Stages of SIEM Implementation_

## About OCI Audit Events

    1) Every CRUD Action on any Oracle Cloud Service is an API Request - Response.
    2) The Audit Store logs every Request-Response Interaction with additional metadata in a searchable Persistence Layer.
    3) OCI Abstracts this Audit Store as an API for it's customers to Consume. 

## Some Defining Principles

### Audit-API is regional

    The Audit Logs of us-ashburn-1 has to fetched from the Audit API End Point from us-ashburn-1 only!

### OCI IAM Constructs are Global653

    A Compartment/IAM Policies/Groups/Users when created in one-region is created in all-regions automatically.

### Audit Events from

    All Regions, All Compartments, Every (1min/5min/10min) etc, 

## The Push Model and Pull Model

The Push/Pull Nature of the architecture is determined by the initiator.

### Push Model

    The System that generates events pushes data to a listener on the SIEM Side.

### Pull Model

    The SIEM pulls data from a listener where the System publishes generated events

## The Protocol

The protocol for publishing is chosen based on the system that produces the event and most SIEM tools have predefined settings based on the source of data ( 500+ Sources ) and the kind of data it publishes

    STANDARDS- PUSH
    
    Syslog
    HTTP(S) Receiver/Collector
    SNMP
    
    
    STANDARDS- PULL
    
    JDBC
    FTP
    SFTP
    SCP
    Kafka

## Log Parsing Formats

The Log formats are usually standards-based but if the source has a custom log format one would configure, the parsing logic based on  RegEx, *WildCards, _Separators_ etc

    *
    STANDARD FORMATS 
    *
    LEEF
    _JSON
    TSV
    CSV
    RAW 
    SYSLOG

## The Data Pipeline

![The Big Picture](https://cdn-images-1.medium.com/max/2602/1*wiRCfb83UfG0yq4K57Ez-A.png)_The Big Picture_

## How is this implemented in OCI

![](https://cdn-images-1.medium.com/max/2820/1*chg_5NeYYh0DtrmQOgY-dQ.png)

## What is the role of Notifications

Notifications are a means to de-couple functions from one another even if they are a part of the same pipeline. Rather than invoking a function directly from another function we use notifications to trigger functions. This allows one function to terminate without waiting for the subsequent functions to complete execution.

    REGIONS AND COMPARTMENTS Fn
    *
    Case : 10 Regions in tenancy subscription, 10 Compartments/Region
    
    Logic:
    Fetch Compartment & Region IDs from 10 Regions x 10 Compartments
    Split the 100 - ( Region-x, Compartment-x, Start Time, End Time)
    Into batches of 25 , 10 /25 = 4 Batches
    
    Write to Stream in 4 Batches
    Publish 4 Notifications
    4 parallel copies of downstream function are Triggered.
    
    Info sent in Notifications:
    Start Offset of Batches, Size of Batch 

## What is the role of Streaming

Streaming allows us to publish messages in an append-only format using a distributed commit log. Since functions are stateless, OCI Streams allow us to store state reliably and preserve context as functions execute and die. The current example uses a single partition, but we could very well use multiple partitions if it exceeds the 1 Mb/Sec write limit and the 2Mb/Sec Read Limit per partition.

    FETCH AUDIT EVENTS Fn
    Case : Recieved a batch of 25 Region x Compartment Tuple to Query from the Notification Trigger
    
    Logic:
    Fetch Audit Events from 25 Region, Compartment Pair
    Assume, each Compartment in each region generates 10 events
    25 x 10 = 250 Events
    
    Split the 250- ( Audit event in json )
    Into batches of 25 , 250/25 = 10 Batches
    
    Write to Stream in 10 Batches
    Generate the Partition ID, Offset, Number of Records to Read 
    This is also known as Cursor Information

## What gets published in Notifications & what gets published in streaming

Streaming is where the actual audit events are written.

Notifications are leveraged to tell the next function where the events are written a.k.a offset, partition, number of records and

![](https://cdn-images-1.medium.com/max/2736/1*F1es6CslYolVG9qo1GwWgQ.png)

## Are functions mandatory here?

No, you could very well package the same code that interacts with the OCI API to fetch audit events and publish them to Splunk across all regions and compartments. The reason for using functions is that it is purely event driven and aligns well with the fact that audit events don’t get generated continuously and rather when users interact with the cloud API

> # The job of Functions can be done by a container running inside a private Kubernetes Cluster as well.

## What are the Design Goals

    1. Must require Zero maintenance
    2. Must be able to handle huge volumes of data 
    3. Must be able to handle changes in tenancy
    4. Must be low-cost
    5. Must be able to push data to Splunk as fast as possible

![Handling changes in tenancy](https://cdn-images-1.medium.com/max/2452/1*hW6Tr2ImbkS2tAuw1NsEnw.png)_Handling changes in tenancy_

## The Components Used and How much do they Cost?

* All Costs Chosen are from the Public Website and are subject to change as per Oracle’s policy.
* Approximations have been applied

![](https://cdn-images-1.medium.com/max/2270/1*PvVVVREgNvajIZv8kfatCQ.png)

    Salient Features
    -----------------
    * Helps schedule Functions at a low cost 
    * Also provides visibility into if the pipeline is running well.
    * Pay-per-use
    * Zero Maintenance
    
    Supported Intervals - 30s, 60s, 5min
    Cost/Endpoint* - *30 Cents/ Month*
    *Qty Reqd.* *1
    
    Overall Cost
    -------------
    0.30$ Per Month

![](https://cdn-images-1.medium.com/max/2000/1*vX9ixszvK5b6tC7w2eADnQ.png)

    Salient Features
    ----------------
    * Provides a Secure HTTPS Endpoint to Trigger Functions
    * Pay-per-use
    * Zero maintenance
    
    Cost/ Endpoint - 3$ per 1 Mio. API Calls per Month
    Qty Required - 1 Gateway , with 8928 API Calls / Month
    
    Calculation
    ------------
    * Schedule API Call to fetch audit events Once every 5 Min.
    * 12 API Calls / Hour
    * 744 x 12 API Calls / Month 
    * 8928 API Calls / Month
    
    Overall Cost
    -------------
    3$ Per Month

![](https://cdn-images-1.medium.com/max/2000/1*NIQphyJo-7jdgIScrw4S6A.png)

    Salient Features
    ----------------
    * Provides a Simple way to Trigger Downstream Functions
    * Can be called from Fns itself in an easy way
    * Allows for a good fire- and forget mechanism
    * Pay-per-use
    * Zero Maintenance
    
    Cost/ Endpoint - 0.60$ per 1 Mio. Deliveries per Month
    Qty Required - 
    
    Calculation
    ------------
    * For a tenancy that has 96 Compartments & 4 Regions
    
    List-Regions - Stage-1
    ----------------------
    * Every 5 Min, the list-regions function produces a list of
      96 x 4 = 384  Tuples
    * The list-region function Splits 384 into batches of 25
      384/25 = 16
    * Publishes 16 Notifications in a 5 Min Interval Window
    
    * 16 x 12 Notification Calls / Hour
    * 744 x 192 Notification Calls / Month  
    * 142,848 Notification Calls / Month
    
    Fetch-Regions - Stage-2
    ----------------------
    Assuming 10 Audit Events/ Compartment/ Region / 5 Min Window
    
    10 Audit Event x 96 compartments x 4 regions 
    3840 Audit Events / 5 Min Window
    
    * The fetch-audit-event function Splits 3840 into batches of 25
      3840/25 = 154 Batches
    * Publishes 154 Notifications in a 5 Min Interval Window
    
    * 154 x 12 Notification Calls / Hour
    * 744 x 1848 API Notification Calls / Month  
    * 1,374,912  Notification Calls / Month
    
    Overall Requirements
    ---------------------
    * Overall  = Stage-1 + Stage-2
    * 1,517,760 Notification Calls/ Month
    
    Overall Cost
    -------------
    1.2 $ / Month

![](https://cdn-images-1.medium.com/max/2642/1*zlQqzGhCPlN2OeuUeU7t8A.png)

    Salient Features
    ----------------
    * Keep Calm ! Write Code and Execute Code
    * Massively Parallel & Massively Scalable
    * Pay-per-use
    * Zero Maintenance
    
    Cost- 
    0.20$ per 1 Mio. Function Invocations per Month
    0.1471 for 10,000 MB Seconds of execution time
    
    Qty Required -
    
    Calculation
    ------------
    * For a tenancy that has 96 Compartments & 4 Regions
    * On an average of 130k Fn Invocations/ Per Day
    * On an average of Execution Time 1.48 x 10^7 MB_MS Per Day
    * 1 Day cost = 1.48 x10^7/10^9( MB_MS -> 10,000 GB_S)* 0.1417 *31
    * Monthly Cost =  ~ 3$/Month
    
    Overall Cost
    -------------
    3 $ / Month

![](https://cdn-images-1.medium.com/max/2022/1*Ldtubox4_CHlRztiAP_qaA.png)

    Salient Features
    ---------------
    * Ease of Use System of Record
    * Store Series of Events
    * Massively Parallel & Massively Scalable
    * Pay-per-use
    * Zero Maintenance
    
    Cost- 
    0.025 $ per GB of PUT/GET
    0.0002$ per GB per Hr STORAGE
    
    Qty Required -
    
    Calculation
    ------------
    * For a tenancy that has 96 Compartments & 4 Regions
    * On an average of 1GB Of Audit Logs/Day
    * 2 GB/Day x 0.025$/GB x 31 Days/Month = 1.8 $/Month 
    * 1 GB/Day * 24 Hrs/Day * 31 Days/Month * 0.0002$ /GB = .14$/ Month
    
    Overall Cost
    -------------
    2 $ / Month

![](https://cdn-images-1.medium.com/max/2000/1*UjFLMhVCDVqpqsMi01HbHw.png)

    Overall Cost/Month        $
    ------------------------------
    Oracle Health Checks  - 0.3 $
    Oracle API-Gateway    - 3.0 $
    Oracle Notifications  - 1.2 $
    Oracle Functions      - 3.0 $
    Oracle Streaming      - 2.0 $
    -------------------------------
    Overall Cost          ~ 10 $
    -------------------------------