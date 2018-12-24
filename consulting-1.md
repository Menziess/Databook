---
description: Being able to provide professional or expert advice.
---

# Consulting

## 

## 3. Architecture

* There is always a trade off, 
* Avoid single points of failure
* Make services as isolated as possible
* Start stateless

Requirements

Drilling down to the core of the problem

Balancing trade-offs of different technologies

Propose solution with SMART comparison against functional and non-functional requirements 

## 4. Technologies

### Services

* **Airflow**
* **Saga**

### Databases

* **Relational**
  * small data
  * schema and relations defined up front
* **Document**
  * writing data without validation
* **Key-Value Store**
  * 
* **Wide-Column Store**
  * schema changes
* **Graph**
  * can store reference in node to external database
  * discover relationships afterward
  * path analysis
  * facebook same relations

### Messaging

* **Kafka**
  * message queue 1 source multiple sources
  * topic queue 1 source ...
  * programs reading from kafka can be taken down, data is not lost for a predefined while
* Kinesis
* Event bus

### Storage Formats

* **CSV:** easy for humans
* **Avro:** serializing messaging, more like a dictionary, schema changes. Json doesn't have this
* **Parquet:** performance
* **JSON:** can't change the schema, can attach Entity if al desired properties \(or more\) are present as JSON fields

hyper lop lop

redis distributed cache

Data consolidation \(google analytics tracker id is shared across session\)

