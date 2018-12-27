---
description: Being able to provide professional or expert advice.
---

# Consulting

A consultant is a professional who provides expert advice in a particular area. A Data Engineer 🔢 👨‍🔧 may provide expert advice in implementing new solutions from the ground up, or improving existing solutions. I both cases, it is valuable to translate business requirements into a high level architectural blueprint.

## 1. Basics

Does the system have to be real-time? What's the minimal required response time? What kind of skills does the team poses? Is performance more important than readability? Should data be available and highly consistent? Is there enough time, or enough money? Is the selected solution robust, flexible, secure?

| Advice | Elucidation |
| :--- | :--- |
| **There is always a trade-off** | The trade-offs are sometimes hard to find, and balancing occurs while developing a system. There are no silver bullets. Don't give answers you don't have. Research pros and cons, make an informed decision. |
| **Take maturity into account** | Mature technologies are often more stable, and easier to implement because of greater adoption among adjacent technologies |
| **Make services as isolated as possible** |  |
| **Avoid premature optimizations** | It is considered as breaking [YAGNI](jargon.md). Choosing Parquet over CSV for example, just because it is performing better. You can always make this choice later. |
| **Write tests before refactoring** | This way you can safely modify code, and verify that the output is still exactly the same. |
| **Avoid single points of failure** |  |
| **Start stateless** |  |

## 2. Technologies

The number of possible combinations between different technologies is vast. Take a look at the following **technologies** within each **subject**:

* [Databases](https://github.com/igorbarinov/awesome-data-engineering#databases)
* [Data Ingestion](https://github.com/igorbarinov/awesome-data-engineering#data-ingestion)
* [File System](https://github.com/igorbarinov/awesome-data-engineering#file-system)
* [Serialization Format](https://github.com/igorbarinov/awesome-data-engineering#serialization-format)\*\*\*\*
* [Stream Processing](https://github.com/igorbarinov/awesome-data-engineering#stream-processing)
* [Batch Processing](https://github.com/igorbarinov/awesome-data-engineering#batch-processing)
* [Charts and Dashboards](https://github.com/igorbarinov/awesome-data-engineering#charts-and-dashboards)
* [Workflow](https://github.com/igorbarinov/awesome-data-engineering#workflow)
* [Monitoring](https://github.com/igorbarinov/awesome-data-engineering#monitoring)

Now, if you give a **piece of advice** that turned out to be **wrong**, you lose all credibility. So how do you go about making crucial architectural decisions? First, you should be aware that these **subjects** exist, second you should know some advantages and disadvantages of some **technologies** of each subject.

You can do this by reading the rest of this chapter!

## 3. Databases

A Data Engineer must be aware of the physical limitations with respect to data. For example, it is physically impossible to read a couple of records with top consistency from a **distributed database** under 150 microseconds.

### Relational VS Non Relational

There are some big differences between relational and non relational databases, although it heavily relies on the DB implementation:

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left">Relational</th>
      <th style="text-align:left">Non Relational</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Storage</td>
      <td style="text-align:left">Tables and rows</td>
      <td style="text-align:left">JSON documents</td>
    </tr>
    <tr>
      <td style="text-align:left">Language</td>
      <td style="text-align:left">SQL</td>
      <td style="text-align:left">depends on implementation</td>
    </tr>
    <tr>
      <td style="text-align:left">Consistency</td>
      <td style="text-align:left">Consistent</td>
      <td style="text-align:left">Eventually Consistent</td>
    </tr>
    <tr>
      <td style="text-align:left">Structure</td>
      <td style="text-align:left">Structured Normalized (foreign keys and indexes), rigid data model</td>
      <td
      style="text-align:left">Semi-Structured Denormalized (related data stored in same document), no
        schema model</td>
    </tr>
    <tr>
      <td style="text-align:left">Advantages</td>
      <td style="text-align:left">
        <ul>
          <li>Complicated querying</li>
          <li>Reliable ACID transactions</li>
          <li>Operations are treated as transactions automatically</li>
          <li>Query routine analysis</li>
          <li>Referential integrity (cascading)</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Information that belongs together is stored together</li>
          <li>No SQL injection</li>
          <li>Easy sharding</li>
          <li>No schema validation allows for experimenting</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Disadvantages</td>
      <td style="text-align:left">
        <ul>
          <li>Doesn't scale that well</li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li>No joins (mostly)</li>
          <li>Manually handle transactions</li>
          <li>Nested documents are hard to keep consistent</li>
          <li>No schema validation may leave DB in invalid state</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Schema</td>
      <td style="text-align:left">Predefined</td>
      <td style="text-align:left">Programmatically</td>
    </tr>
    <tr>
      <td style="text-align:left">Scaling</td>
      <td style="text-align:left">Mostly vertical (improving machine), high cost, and a limitation to the
        level of scaling</td>
      <td style="text-align:left">
        <p>Horizontal (adding more machines), low cost, can handle high number of
          operations</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Maintenance</td>
      <td style="text-align:left">Expensive, requires trained workforce</td>
      <td style="text-align:left">Cheap, automatic repair and easier distribution</td>
    </tr>
    <tr>
      <td style="text-align:left">Caching</td>
      <td style="text-align:left">Separate hardware</td>
      <td style="text-align:left">Integrated</td>
    </tr>
  </tbody>
</table>You generally choose a relational database when ACID compliance must be ensured, and when your data is structured and unchanging. But, most importantly, it is not Big Data.

If there's little structure, and the DB must handle large VVV data, a NoSQL database is a better choice. Also, the lack of schema and migrations allows for quick development. To choose which NoSQL DB is best suited for your use case, this interesting decision tree may be useful:

![Felix Gessert: https://medium.baqend.com/nosql-databases-a-survey-and-decision-guidance-ea7823a822d](.gitbook/assets/image%20%288%29.png)

### CAP

A distributed database that continues to operate when network partitions occur is considered to be partition tolerant. As a consequence, data that is read from one partition may differ from the other, meaning that consistency isn't guaranteed, but the database is available. Not unless you are talking about "eventual consistency", which implies that it takes some time to synchronize. Consider the order of magnitudes between different network operations here:

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

For this reason, the CAP theorem states that **networked shared-data systems** can only guarantee/strongly support two of the following three properties:

* **Consistency:** every read receives the most recent write or an error
* **Availability:** every request receives a reasonable response within a reasonable amount of time
* **Partition Tolerance:** the system will continue to function when network partitions occur

Because networks are not reliable, and eventual consistency is never instant, we must tolerate partitions in a distributed system. So we are left with the following two choices:

* **CP:** wait for a response from the partitioned node which could result in a timeout error. The system can also choose to return an error, depending on the scenario you desire. \(Choose Consistency over Availability when your business requirements dictate atomic reads and writes\)
* **AP:** return the most recent version of the data you have, which could be stale. This system state will also accept writes that can be processed later when the partition is resolved. \(Choose when consistency is not crucial\)
* **CA:** highly available and consistent, but not partition tolerant \(Choose for \)

### Transactions, ACID and BASE

ACID is an acronym that describes database transaction properties \(pessimistic replication model\):

* **Atomicity:** guarantees that each transaction is handled as a single unit. A transaction consisting of multiple statements either succeeds completely \(a change\), or fails completely \(no change\).
* **Consistency:** ensures validity of database with constraints, cascades, and triggers.
* **Isolation:** ensures concurrent transactions to leave the database state as if they were executed sequentially.
* **Durability:** guarantees that once a transaction has been committed, it will remain committed even in case of a system failure.

BASE is an acronym that describes eventually consistent services \(optimistic replication model\):

* **Basically Available:** means that any data request should receive a response, but that the response may indicate a failure instead of the requested data.
* **Soft State:** given eventual consistency, the system may be in a changing state until consistency is reached
* **Eventual Consistency:** describes the situation where a DDBS achieves high availability while loosely guaranteeing that data, in the absence of updates, will eventually reflect the last updated value across the system, and therefore the data may vary in value until the system reaches a consistent state.

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

