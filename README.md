---
description: Everything about data engineering.
---

# Introduction

The high demand for Data Engineers 🔢 👨‍🔧 👨‍🔧 may motivate software-savvy people to venture into the world of data. There is so much to learn, so little time. That is why concise summaries and code examples can be a useful mean to ease the strain on human's inherently limited memory.

**Tip:** look up unfamiliar words in the [vocabulary](vocabulary.md).

## 1. Introduction of the Introduction

Data Scientist 👨‍🔧 and Data Scientist 👩‍🔬 are new job titles, where Data Analyst, BI Developer, and Software Engineer are well known titles. 

* **Data Analyst:** has the understanding of intermediate statistics, data mining tools, SQL, and data visualizations.
* **BI Developer:** works closely with stakeholders to design and build reporting dashboards, integrating data from different sources, aggregating data with SQL, but not performing data analysis.
* **Data Scientists:** turns raw data into pure insights using advanced statistics, math, and machine learning, cooperating with Data Engineers as some machine learning techniques require big and fast data.
* **Software Engineer:** designs, writes, and aims to improve quality characteristics of software for computers or other electronic devices.
* **Data Engineers:** a Software Engineer that writes programs to automate data aggregation, [batch](https://www.quora.com/What-are-the-differences-between-batch-processing-and-stream-processing-systems) processing, [streaming](https://www.quora.com/What-are-the-differences-between-batch-processing-and-stream-processing-systems) fast data processing, and helps to deploy and scale machine learning models into production.

## 2. Love-Hate Relationship 👨‍🔧 💔 👩‍🔬

Data science and data engineering go hand in hand. A Data Engineer may aggregate batches of data overnight, so that the Data Scientist may train a machine learning model with it in a [jupyter notebook](https://jupyter.org/), after which the 👨‍🔧 and 👩‍🔬 sit around the table to extract and refactor the useful bits of the code to forge a contract and automate the process of deploying the model. Let's specify this process:

* **Data Discovery:** automatically discover data needed to train machine learning models.
* **Data Ingestion \(ETL\):** the act of moving \(and transforming\) data - especially unstructured data - from where it is originated, into a system where it can be stored and analyzed such as [Hadoop](technologies/hadoop.md).
* **Data Exploration:** visualizing the relationships of interest within the source data.
* **Data Preprocessing:** encoding categorical variables, imputing missing variables, executing other corrections and augmentations.
* **Feature Engineering:** deciding what features to create and check whether features work for a ML model. 
* **Algorithm Selection:** selecting the most optimal algorithm for a given feature set.
* **Training:** training the ML model \(may sometimes take a long time\)
* **Evaluation:** determine whether the model's accuracy, efficiency is sufficient.
* **Hyperparameter Tuning:** choosing the set of optimal [hyperparameters](https://en.wikipedia.org/wiki/Hyperparameter_%28machine_learning%29) using methods such as:
  * Grid search
  * Random search
  * Bayesian optimization
  * Evolutionary optimization
  * Gradient-based optimization
* **Testing:** writing tests to determine whether functionalities such as cleaning, encoding, test-train splitting, serializing, training, etc still work as intended.
* **Refactoring:** transforming jupyter notebooks / scripts to a sound code project that can handle the data volume and velocity of the production environment.
* **Deployment:** 
  * create a REST API that exposes a model over http
  * dockerizing the project so that it can scale and run in isolation
  * applying continuous integration to automate collaboration
  * apply continuous deployment so that new versions of the project are tested, built and deployed automatically
  * exposing the model to the systems that need it
* **Provisioning:** using [Kubernetes](technologies/kubernetes.md) or [Docker Swarm](technologies/docker.md#2-2-scale-service-multiple-containers-single-node) to automatically scale up or down the service.

It is understood that 👨‍🔧 are often critical of the code quality and scalability of the piece of code delivered by 👩‍🔬, which in return are unhappily surprised when they have to adjust their code only because the 👨‍🔧 is overly critical, all the while the data provided by the 👨‍🔧 wasn't all that well prepared. But despite the hate, there exists love when they work as a team, and get that model deployed successfully!

## 3. Defying Gravity

A Data Engineer must be aware of the physical limitations with respect to data. For example, while I am writing this chapter, it is physically impossible to read a couple of records with top consistency from a distributed database under 150 microseconds. 

Consider the order of magnitudes between different operations displayed here:

{% code-tabs %}
{% code-tabs-item title="http://norvig.com/21-days.html\#answers" %}
```swift
           0.5 ns - CPU L1 dCACHE reference
           1   ns - speed-of-light (a photon) travel a 1 ft (30.5cm) distance
           5   ns - CPU L1 iCACHE Branch mispredict
           7   ns - CPU L2  CACHE reference
          71   ns - CPU cross-QPI/NUMA best  case on XEON E5-46*
         100   ns - MUTEX lock/unlock
         100   ns - own DDR MEMORY reference
         135   ns - CPU cross-QPI/NUMA best  case on XEON E7-*
         202   ns - CPU cross-QPI/NUMA worst case on XEON E7-*
         325   ns - CPU cross-QPI/NUMA worst case on XEON E5-46*
      10,000   ns - Compress 1K bytes with Zippy PROCESS
      20,000   ns - Send 2K bytes over 1 Gbps NETWORK
     250,000   ns - Read 1 MB sequentially from MEMORY
     500,000   ns - Round trip within a same DataCenter
  10,000,000   ns - DISK seek
  10,000,000   ns - Read 1 MB sequentially from NETWORK
  30,000,000   ns - Read 1 MB sequentially from DISK
 150,000,000   ns - Send a NETWORK packet California -> Netherlands
|   |   |   |
|   |   | ns|
|   | us|
| ms|
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The CAP theorem states that **networked shared-data systems** can only guarantee/strongly support two of the following three properties:

* **Consistency:** every read receives the most recent write or an error
* **Availability:** every request receives a reasonable response within a reasonable amount of time
* **Partition Tolerant:** the system will continue to function when network partitions occur

Because networks are not reliable, we must tolerate partitions in a distributed system. So we are left with the following two choices:

* **CP:** wait for a response from the partitioned node which could result in a timeout error. The system can also choose to return an error, depending on the scenario you desire. \(Choose Consistency over Availability when your business requirements dictate atomic reads and writes\)
* **AP:** return the most recent version of the data you have, which could be stale. This system state will also accept writes that can be processed later when the partition is resolved. \(Choose when consistency is not crucial\)

## 4. Big Data

Where Data Analysts and BI Developers dealt with Data Warehouses with static structured Terabytes of data, Data Engineers deal with Big Data:

* **Volume:** petabytes of data
* **Variety:** structured and unstructured data of any type and format
* **Velocity:** flowing streams of fast data

Organizations grow into Big Data as they become experienced with processing data into valuable information, from left to right:

![](https://lh4.googleusercontent.com/4SIn1Kh5mpbg4c4fdGjpcJOwYBsgYhaoF-wkX_a6QTNkumFEXUH2djqptKn3ItFnlC1gNc04cUd6Wef5hdQp7jxxl_u6FIes-zYfcyd11lqivhM5q_toIqGbmpy-RbzcGfkW3QcZ)

* [Big Data](https://github.com/onurakpolat/awesome-bigdata#readme)
* [Public Datasets](https://github.com/awesomedata/awesome-public-datasets#readme)
* [Hadoop](https://github.com/youngwookim/awesome-hadoop#readme) - Framework for distributed storage and processing of very large data sets.
* [Data Engineering](https://github.com/igorbarinov/awesome-data-engineering#readme)
* [Streaming](https://github.com/manuzhang/awesome-streaming#readme)
* [Apache Spark](https://github.com/awesome-spark/awesome-spark#readme) - Unified engine for large-scale data processing.

## 4. Databases

ACID

* **Atomicity:** guarantees that each transaction is handled as a single unit. A transaction consisting of multiple statements either succeeds completely \(a change\), or fails completely \(no change\).
* **Consistency:** ensures validity of database with constraints, cascades, and triggers.
* **Isolation:** ensures concurrent transactions to leave the database state as if they were executed sequentially.
* **Durability:** guarantees that once a transaction has been committed, it will remain committed even in case of a system failure.



* [Database](https://github.com/numetriclabz/awesome-db#readme)
* [MySQL](https://github.com/shlomi-noach/awesome-mysql/blob/gh-pages/index.md)
* [SQLAlchemy](https://github.com/dahlia/awesome-sqlalchemy#readme)
* [InfluxDB](https://github.com/mark-rushakoff/awesome-influxdb#readme)
* [Neo4j](https://github.com/neueda/awesome-neo4j#readme)
* [MongoDB](https://github.com/ramnes/awesome-mongodb#readme) - NoSQL database.
* [RethinkDB](https://github.com/d3viant0ne/awesome-rethinkdb#readme)
* [TinkerPop](https://github.com/mohataher/awesome-tinkerpop#readme) - Graph computing framework.
* [PostgreSQL](https://github.com/dhamaniasad/awesome-postgres#readme) - Object-relational database.
* [CouchDB](https://github.com/quangv/awesome-couchdb#readme) - Document-oriented NoSQL database.
* [HBase](https://github.com/rayokota/awesome-hbase#readme) - Distributed, scalable, big data store.

