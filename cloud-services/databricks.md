---
description: Quick tutorial.
---

# Databricks

## 1. Introduction

Databricks is a company founded by the creators of Apache Spark. It may also refer to the Unified Analytics Platform, a web-based Spark platform that automates cluster management and IPython-style notebooks.

* Interactive user interface
* Cluster sharing
* Security features
* Collaboration in the same notebooks, revision control, IDE / Github integration
* Data management, ability to connect different data sources

![Unified Analytics Platform on Azure](../.gitbook/assets/image%20%283%29.png)

It improves collaboration between Data Scientists, Data Engineers, and Business Analysts.

## 2. Installation

* [Free Databricks](https://databricks.com/try-databricks)
* [Free Databricks on Azure](https://azure.microsoft.com/en-us/services/databricks/)
* [Free Databricks on AWS](https://databricks.com/aws)

## 3. Clusters

It's trivially easy to scale and manage computation resources. There are two cluster modes:

**Standard Clusters**

* Supports Scala notebook cells
* Has some ML-ready runtimes

**High Concurrency Clusters**

* Does not support Scala notebook cells
* Has some ML-ready runtimes
* Allows fair sharing of resources between users through "task preemption"
* Fault isolation, creating an isolated environment for each notebook

The Databricks runtime defines the Spark and Scala versions.

## 4. Data

Data can be uploaded trough the UI, or imported from a range of data sources into **DBFS \(Databricks File System\)**, or processed in memory and stored back into a data source. In the Data menu, you can generate a notebook for each option, that demonstrates how to import and convert the data to a table. Options may vary between Azure and AWS platforms.

## 5. Notebooks

After generating a notebook, you may have to specify sensitive information such as passwords or secrets. As you can collaborate in Databricks notebooks, other users may see you paste passwords before you remove them. You can instead create a secret scope, to store and secrets in a hidden way, and access them using **dbutils**:

```python
dbutils.secrets.get('<scope>', '<secret-key>')
```

This tool allows you to:

* **dbutils.notebook** execute notebooks as scripts, passing arguments and receiving a return value
* **dbutils.secrets** use secret scopes and keys, but not show or modify them
* **dbutils.library** install python libraries
* **dbutils.widgets** create and read html inputs placed above the notebook
* **dbutils.fs** access **DBFS**, crud folders and files

You can also access **DBFS** through the magic command `%fs` that you can put on top of a notebook cell:

```text
%fs ls /FileStore/tables
```

This command achieves the same as:

```text
%sh ls /dbfs/FileStore/tables
```

As you can see we can execute shell commands. You can only specify one magic command per cell:

* **python:** Python, may be set as default
* **scala:** Scala, may be set as default
* **sql:** SQL
* **r:** R
* **run:** Run other notebook
* **md:** Markdown
* **sh:** Execute shell
* **bash:** Execute bash
* **fs:** File System through **dbutils** 

Besides the **dbutils** tool that is accessible in notebook cells, there is also a **display** function that allows you to display DataFrames as tables, and create **visualizations**.

## 6. Jobs

Finally there are jobs, allowing you to run a [notebook](https://docs.databricks.com/user-guide/notebooks/index.html) or JAR either immediately or on a scheduled basis. You can create and run jobs using the UI, the CLI, and by invoking the Jobs API. Similarly, you can monitor job run results in the UI, using the CLI, by querying the API, and through email alerts.

