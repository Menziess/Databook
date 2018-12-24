---
description: Providing professional or expert advice.
---

# Consulting

Requirements

Drilling down to the core of the problem

Balancing trade-offs of different technologies

Propose solution with SMART comparison against functional and non-functional requirements 

## 1. Agile / Lean

### Scrum

* A lightweight framework for iterative delivery optimizing value
* Predefined roles
* Changes not allowed \(during sprint\)
* Measures team velocity
* Based on **Empiricism \(**believing that knowledge comes from experience\), having pillars: transparency, inspection, adaptation
* Values: commitment, courage, focus, openness, respect
* Developers may sacrifice quality because of deadlines

### Kanban

* A management method designed to continuously improve service delivery
* No predefined roles
* Changes allowed
* Measures cycle time
* Work in progress forces collaboration

## 2. Communication Skills

There's a universal language of behavior called the **DISC** Personality System. Research has shown that behavioral characteristics can be grouped together in four major groups:

* **D = Dominant, Driver:** Someone who's assertive, to the point, and wants the bottom line. 
* **I = Influencing, Inspiring:** Someone who's a great communicator, friendly to everyone.
* **S = Steady, Stable:** Someone who's a great listener, and a great team player.
* **C = Correct, Compliant:** Someone who enjoys gathering facts and details, who is thorough in all activities.

To communicate effectively with each style:

* **D:** Don't ramble or waste time, stay on task, be clear and specific, and to the point, don't chitchat or try to build a personal relationship, come prepared and organized, present facts logically, provide alternatives and choices, and if you disagree focus on the facts.
* **I:** Talk and ask about their ideas and goals, allow time for relating and socializing, don't drive to facts and alternatives, help them get organized, provide ideas, don't leave decisions in the air, provide testimonials from people they see as important, offer incentives for their willingness to take risks.
* **S:** Don't rush, show interest in them as people, 

Human personality is comprised of varying intensities of these four behavioral styles, and are expressed differently depending on the environment and self perception:

* **Public self:** Everyone acts according to how they think other people expect them to act. This behavior is the public self, the person projected to others. Sometimes, there is no difference between the true person and their public self. However, the public self can be very different from the "real" person; it is a mask.
* **Private self:** Everyone has learned responses from the past: consequently, these are behaviors which the person accepts about him/herself. Under pressure or tension, these learned behaviors become prominent. This is the graph which is the least likely to change because these are natural and ingrained responses.
* **Perceived self:** Everyone envisions him/her self in a particular way, a mental picture that one has of him/her self, the self image or self identity. Change in one's perception can occur, but it is usually gradual and based on the changing demands of one's environment.

Opposed to your personality, you can change some skills to be a more effective communicator:

## 3. Architecture

* There is always a trade off, 
* Avoid single points of failure
* Make services as isolated as possible
* Start stateless

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

### 

### 

