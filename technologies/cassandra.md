# Cassandra

## 1. Introduction

Apache Cassandra is a typical **AP** Wide Column store, NoSQL DDBMS. It can handle heavy writes and allows for low latency reads. Every node in a Cassandra cluster has the same role, so there's no single point of failure. Data is distributed across the cluster so each node contains different data. Apple uses more than 100.000 Cassandra nodes! 

Cassandra has:

* Distributed nodes
* Replication
* Scalability
* Fault-tolerance
* Tunable consistency
* MapReduce support
* Query language \(CQL\)

## 2. CQL

A KEYSPACE is similar to a SCHEMA or DATABASE. A COLUMNFAMILY is comparable to a TABLE.

```sql
CREATE KEYSPACE MyKeySpace
  WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };

USE MyKeySpace;

CREATE COLUMNFAMILY MyColumns (id text, Last text, First text, PRIMARY KEY(id));

INSERT INTO MyColumns (id, Last, First) VALUES ('1', 'Doe', 'John');

SELECT * FROM MyColumns;
```

  


tombstones

token-ring





