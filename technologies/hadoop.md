# Hadoop

## 1. Introduction

Hadoop is a scalable, open source, distributed, data-intensive, fault-tolerant computing framework, capable of handling thousands of nodes and petabytes of data. It comprises of three main subprojects:

* Hadoop Common: common utilities package
* HDFS: Hadoop Distributed File System
* MapReduce: A software framework for distributed processing

When people talk about Hadoop, they often refer to the [Hadoop Ecosystem](hadoop.md#6-ecosystem), which includes various components of the Apache Hadoop software library, as well as accessories and tools provided by the Apache Software Foundation.

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

Here is a very crude example of how you can install an Hadoop distribution:

```bash
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

## 4. HDFS

There are two shells to interact with the file system. That is, the local and distributed file system. The following line would list local files, including distributed files that happen to be stored at that particular location.

```bash
hdfs fs ls
```

Then we can also use the following line to print out files stored in a distributed fashion. 

```bash
hdfs dfs ls
```

One would typically get a file onto the system in some way, by downloading it for example. After that one would put the file onto hdfs:

```bash
cd ~/Downloads
wget http://files.grouplens.org/datasets/movielens/ml-latest-small.zip
unzip ml-latest-small.zip

hdfs dfs -mkdir ~/localhdfs/movies
hdfs dfs -put ~/Downloads/ml-latest-small/movies.csv ~/localhdfs/movies/
```

Notice that we specify a folder, instead of a filename when we put the file onto hdfs. Now that it's there, we can inspect its contents using `-cat` or `-tail`:

```bash
hdfs dfs -cat ~/localhdfs/movies/movies.csv | head
hdfs dfs -tail ~/localhdfs/movies/movies.csv
```

## 5. MapReduce

Before the rise of abstractions such as Hive, Pig, and Impala, one would typically write a MapReduce JAR program that contained the map and reduce code and the configuration to run a Hadoop job.

```bash
examples_jar="${HADOOP_HOME}/share/hadoop/mapreduce/hadoop-mapreduce-examples-<hadoop version>.jar"
```

This location contains some examples which you can as such:

```bash
hadoop jar {examples_jar} wordcount movies output
hdfs dfs -ls output
```

After the job finishes, the output will contain a `_SUCCESS` flag to indicate that the processing was successful. If something appears to be going wrong, you can stop a running job as such:

```bash
mapred job -list
mapred job -kill <jobid>
```

## 6. Hadoop Ecosystem 

Some components that comprise the ecosystem are:

* HBase is a non-relational 
* Oozie: workflow scheduler
* Sqoop
* Gobblin
* Hive
* Impala
* Pig

## 7. Hive, Impala, Pig, 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Technology</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Hive</td>
      <td style="text-align:left">Data Warehouse Infrastructure on Hadoop</td>
      <td style="text-align:left">
        <p>Generates query at compile time</p>
        <p>Cold start problem</p>
        <p>More universal pluggable language</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Impala</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Runtime code generation</p>
        <p>Always ready</p>
        <p>Brute processing for fast analytic results</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Pig</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>