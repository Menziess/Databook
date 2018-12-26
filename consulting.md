---
description: Being able to provide professional or expert advice.
---

# Consulting

A consultant is a professional who provides expert advice in a particular area. A Data Engineer 🔢 👨‍🔧 may provide expert advice in implementing new solutions from the ground up, or improving existing solutions. I both cases, it is valuable to translate business requirements into a high level architectural blueprint.

## 1. Basics

Does the system have to be real-time? What's the minimal required response time? What kind of language is the team using? Is performance more important than readability? Should data be available and highly consistent? Is there enough time, or enough money? 

| Advice | Elucidation |
| :--- | :--- |
| **There is always a trade-off** | The trade-offs are sometimes hard to find, and balancing occurs while developing a system. There are no silver bullets. Don't give answers you don't have. Research pros and cons, make an informed decision. |
| **Take maturity into account** | Mature technologies are often more stable, and easier to implement because of greater adoption among adjacent technologies |
| **Make services as isolated as possible** |  |
| **Avoid premature optimizations** | It is considered as breaking [YAGNI](vocabulary.md). Choosing Parquet over CSV for example, just because it is performing better. You can always make this choice later. |
| **Write tests before refactoring** | This way you can safely modify code, and verify that the output is still exactly the same. |
| **Avoid single points of failure** |  |
| **Start stateless** |  |

## 2. Technologies

The number of possible combinations between different technologies is vast. Take a look at the following lists of technologies, while we leave out the implementation details for now. Now, if you give a **piece of advice** that turned out to be **wrong**, you lose all credibility. So how do you go about making crucial decisions?

* [Databases](https://github.com/igorbarinov/awesome-data-engineering#databases)
* [Data Ingestion](https://github.com/igorbarinov/awesome-data-engineering#data-ingestion)
* [File System](https://github.com/igorbarinov/awesome-data-engineering#file-system)
* [Serialization Format](https://github.com/igorbarinov/awesome-data-engineering#serialization-format)\*\*\*\*
* [Stream Processing](https://github.com/igorbarinov/awesome-data-engineering#stream-processing)
* [Batch Processing](https://github.com/igorbarinov/awesome-data-engineering#batch-processing)
* [Charts and Dashboards](https://github.com/igorbarinov/awesome-data-engineering#charts-and-dashboards)
* [Workflow](https://github.com/igorbarinov/awesome-data-engineering#workflow)
* [Monitoring](https://github.com/igorbarinov/awesome-data-engineering#monitoring)

## 3. Databases

A Data Engineer must be aware of the physical limitations with respect to data. For example, it is physically impossible to read a couple of records with top consistency from a distributed database under 150 microseconds.

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

Then there is **ACID**:

* **Atomicity:** guarantees that each transaction is handled as a single unit. A transaction consisting of multiple statements either succeeds completely \(a change\), or fails completely \(no change\).
* **Consistency:** ensures validity of database with constraints, cascades, and triggers.
* **Isolation:** ensures concurrent transactions to leave the database state as if they were executed sequentially.
* **Durability:** guarantees that once a transaction has been committed, it will remain committed even in case of a system failure.

@todo:

* **Relational**
  * small data
  * schema and relations defined up front
* **Document**
  * writing data without validation
* **Key-Value Store**
* **Wide-Column Store**
  * schema changes
* **Graph**
  * can store reference in node to external database
  * discover relationships afterward
  * path analysis
  * facebook same relations

## 4. Data Ingestion

## 5. File System

## 6. Serialization Format

* **CSV:** easy for humans
* **Avro:** serializing messaging, more like a dictionary, schema changes. Json doesn't have this
* **Parquet:** performance
* **JSON:** can't change the schema, can attach Entity if al desired properties \(or more\) are present as JSON fields

## 7. Stream Processing

## 8. Batch Processing

## 9. Charts and Dashboards

## 10. Workflow

## 11. Monitoring

