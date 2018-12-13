---
description: Quick tutorial.
---

# Kafka

## 1. Introduction

Linkedin 2011

Decouples applications 

Messaging system

Kafka runs on a cluster with one or multiple datacenters

Stores stream of records in categories called topic

Each record consists of a key, value, timestamp. Key mod nr clusters, partitions by key.

### 1.1 Why Kafka Is Fast

Persists all data to disk, utilizes cache for high performance read/writes. Writes go to page cache directly, and reads transfer data from page cache to socket using Linux sendFile\(\) system call

### 1.2 

## 2. Messages

**Topic:** local group f records. Producers store their data in particular topic via brokers. Consumers read data from that particular topic via brokers. Data stored in topic split into partitions and replicated.

**Partition:** Ordered and immutable sequence of message/records. Each new record is appended to a partition. Partitions in Kafka don't particularly determine max number of consumers.

**Replica:** Number of replica's of a **Topic**.

**Offset:** the records in the partitions are each assigned a sequential id number called the offset or index, that uniquely identifies each record within the partition. Each consumer tracks their own offset and can go back in the history by changing the offset to an earlier message order. E.g Consumer A has offset=9 and Consumer B has offset=5.

**Producer:** Kafka client that produces messages as single or batch messages to **Topics**. Single messages may improve speed, but reduce throughput. 

**Consumer:** Kafka client reads data from **Topics**. It can read from multiple topics at the same time. Each consumer is assigned one or more partitions and its consumer's responsibility to keep track of offsets. A consumer can browse through the history of messages by changing offset. When a new consumer comes in, a partition may block old consumers for re-balancing, this may cause the order of the messages to change for the old consumers.

**Broker:** each node in Kafka Cluster is called Broker. AKA Kafka Server or Kafka Node. Topics are distributed across Brokers. A single broker hosts topic partition of one or more topics. Controllers are special kind of brokers. Each Kafka cluster has one and only one controller.

## 3. Use Cases

* Messaging
* Website tracking
* Metrics
* Log aggregation
* Stream processing
* Event sourcing
* Commit log

## 4. Group ID

Consumers with the same group ID will 

**Queue:** each message is only processed by a single consumer

**Topic:** each message is processed by all consumers

