---
description: Quick tutorial
---

# Hadoop

## 1. Introduction

Hadoop is a scalable, open source, distributed, data-intensive, fault-tolerant computing framework, capable of handling thousands of nodes and petabytes of data. It comprises of three main subprojects:

* Hadoop Common: common utilities package
* HDFS: Hadoop Distributed File System
* MapReduce: A software framework for distributed processing

## 2. Nodes

Master- and slave nodes organize the Hadoop cluster. Either node type may take on several roles. For example, the master node contains:

* Job tracker node \(MapReduce layer\)
* Task tracker node \(MapReduce layer\)
* Name node \(HDFS layer\)
* Data node \(HDFS layer\)

While a slave node may contain:

* Task tracker node \(MapReduce layer\)
* Data node \(HDFS layer\)

## 3. Installation



```text
FROM kovarn/python-java

# Set environmental variables
ENV HADOOP_HOME /localhadoop/hadoop-2.9.2
ENV JAVA_HOME=/usr/lib/jvm/jdk1.8.0_111/
ENV PATH ${HADOOP_HOME}/bin:${PATH}

# Downloading hadoop and installing config file
RUN wget http://apache.40b.nl/hadoop/common/hadoop-2.9.2/hadoop-2.9.2.tar.gz &&   tar xzf hadoop-2.9.2.tar.gz && \
  rm -rf hadoop-2.9.2.tar.gz

# Create localhadoop folder
RUN mkdir localhadoop && \
  mv -v /hadoop-2.9.2 /localhadoop/hadoop-2.9.2

# Create config folder
RUN mkdir localhadoop/conf && \
  cp -R ${HADOOP_HOME}/etc/hadoop/* localhadoop/conf && \
  wget https://gist.githubusercontent.com/Menziess/52f1064f3b77b4b0b3655ca270a38b6b/raw/cba6dcd237f89538d5a03c57b27278eb15b6d314/hdfs-site.xml -O localhadoop/conf/hdfs-site.xml

RUN hdfs dfs -mkdir localhdfs
```

