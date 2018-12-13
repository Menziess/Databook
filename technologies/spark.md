---
description: Quick tutorial.
---

# Spark

## 1. Introduction

Spark is based on the Hadoop ecosystem, using Hadoops scalable, flexible, fault-tolerant and cost  effective storage and processing implementations while having its own cluster management solution. The intermediate results are also not stored on disk, but rather in distributed memory, making Spark computations a lot faster.

## 2. Installation

```bash
java -version

# If java 8 is not installed
sudo apt install --no-install-recommends openjdk-8-jre-headless -y

# Download spark from https://spark.apache.org/downloads.html
wget http://apache.40b.nl/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz
gunzip -c spark-2.4.0-bin-hadoop2.7.tgz | tar xvf -
rm spark-2.4.0-bin-hadoop2.7.tgz

# Install spark
sudo mv spark-2.4.0-bin-hadoop2.7/ /usr/local/spark
```

Add to PATH

```bash
echo "# For spark!" >> ~/.bashrc
echo "JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" >> ~/.bashrc
echo "export PATH=$PATH:/usr/local/spark/bin" >> ~/.bashrc
source ~/.bashrc
```

Verify the installation

```text
pyspark
```

## 3. Testing

[https://github.com/holdenk/spark-testing-base](https://github.com/holdenk/spark-testing-base)

## 4. Pyspark

#### 4.1 Setup

Import types and functions:

```python
from pyspark.sql import SparkSession
import pyspark.sql.functions as sf
import pyspark.sql.types as st
```

Start spark session:

```python
spark = SparkSession \
    .builder \
    .appName("Spark Aplication") \
    .getOrCreate()
```

Read data: 

```python
# 'csv', 'jdbc', 'json', 'orc', 'parquet', 'text'
df = spark.read \
    .format("csv") \             # How the data is stored
    .option("header", "true") \
    .option("inferSchema", "true") \
    .option("nanValue", "NA") \
    .csv("data/heroes.csv")      # How the data should be stored
```

Output:

```python
df.show(10, truncate=False)
df.collect()
df.head(10)
df.toPandas()
df.printSchema()
```

#### 4.2 Create Dataframe

Specify data and schema:

```python
data = [
    ("2015-05-14 03:53:00", "WARRANT ARREST"),
    ("2015-05-14 03:53:00", "TRAFFIC VIOLATION"),
    ("2015-05-14 03:33:00", "TRAFFIC VIOLATION")
]

test = spark.createDataFrame(data, ["Dates", "Description"])
```

Add column:

```python
test.withColumn('added_col', 
    sf.when(sf.col('Dates') > "2015-05-14 03:33:00")
)
```



## 5. Docker Image

{% code-tabs %}
{% code-tabs-item title="Pipfile" %}
```bash
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
pyspark = "*"

[dev-packages]
pyspark = "*"

[requires]
python_version = "3.6"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Dockerfile" %}
```bash
FROM python:3.6.7-slim-stretch

WORKDIR /app

COPY Pipfile /app
COPY Pipfile.lock /app
RUN pip install pipenv

RUN pipenv install --system

RUN apt update && \
  mkdir -p /usr/share/man/man1 && \
  apt install -y openjdk-8-jre-headless

ENTRYPOINT ["pyspark"]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

