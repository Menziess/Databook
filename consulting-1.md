---
description: Being able to provide professional or expert advice.
---

# Consulting

A consultant is a professional who provides expert advice in a particular area. A Data Engineer 🔢 👨‍🔧 may provide expert advice in implementing new solutions from the ground up, or improving existing solutions. I both cases, it is valuable to translate business requirements into a high level architectural blueprint.

## 1. Basics

Where to start when implementing a new solution, or solving a problem within an existing solution?

A whiteboard, or a piece of paper!

Don't let yourself get intimidated by business jargon, project management procedures, or other stress factors. Identify the person who owns the problem, or the one who represents the user's best interest.

Determine whether a piece of software needs to be built, or that a service must be maintained and improved.

## 2. Architecture

There are some things that are important when it comes to architecting complex systems:

* There is always a trade off
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

