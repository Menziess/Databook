# Cassandra

## 1. Introduction

Apache Cassandra is a Wide Column store, NoSQL DDBMS. It can handle heavy writes and allows for low latency reads. Every node in a Cassandra cluster has the same role, so there's no single point of failure. Data is distributed across the cluster so each node contains different data. 

Supports replication and multi data center replicationReplication strategies are configurable.[\[15\]](https://en.wikipedia.org/wiki/Apache_Cassandra#cite_note-15) Cassandra is designed as a distributed system, for deployment of large numbers of nodes across multiple data centers. Key features of Cassandra’s distributed architecture are specifically tailored for multiple-data center deployment, for redundancy, for failover and disaster recovery.ScalabilityDesigned to have read and write throughput both increase linearly as new machines are added, with the aim of no downtime or interruption to applications.Fault-tolerantData is automatically replicated to multiple nodes for [fault-tolerance](https://en.wikipedia.org/wiki/Fault-tolerance). [Replication](https://en.wikipedia.org/wiki/Replication_%28computer_science%29) across multiple data centers is supported. Failed nodes can be replaced with no downtime.Tunable consistencyCassandra is typically classified as an [AP system](https://en.wikipedia.org/wiki/CAP_theorem), meaning that availability and partition tolerance are generally considered to be more important than consistency in Cassandra[\[16\]](https://en.wikipedia.org/wiki/Apache_Cassandra#cite_note-16), Writes and reads offer a tunable level of [consistency](https://en.wikipedia.org/wiki/Consistency_%28database_systems%29), all the way from "writes never fail" to "block for all replicas to be readable", with the [quorum level](https://en.wikipedia.org/wiki/Quorum_%28distributed_computing%29) in the middle.[\[17\]](https://en.wikipedia.org/wiki/Apache_Cassandra#cite_note-tunable_consistency-17)MapReduce supportCassandra has [Hadoop](https://en.wikipedia.org/wiki/Hadoop) integration, with [MapReduce](https://en.wikipedia.org/wiki/MapReduce) support. There is support also for [Apache Pig](https://en.wikipedia.org/wiki/Pig_%28programming_tool%29) and [Apache Hive](https://en.wikipedia.org/wiki/Apache_Hive).[\[18\]](https://en.wikipedia.org/wiki/Apache_Cassandra#cite_note-hadoopsupport-18)Query languageCassandra introduced the [Cassandra Query Language](https://en.wikipedia.org/w/index.php?title=Cassandra_Query_Language&action=edit&redlink=1) \(CQL\). CQL is a simple interface for accessing Cassandra, as an alternative to the traditional [Structured Query Language](https://en.wikipedia.org/wiki/SQL)\(SQL\).  


tombstones

token-ring





