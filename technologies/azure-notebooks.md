---
description: Quick tutorial
---

# Azure Notebooks

## 1. Introduction

Jupyter Notebooks running R, Python, F\#, online. Create an account, a project and a notebook to load data, generate a ML model, and deploy it as a web service.

**Tip:** Look at [these examples](https://notebooks.azure.com/Microsoft/projects).

## 2. Installation

1. [Login or create an account.](https://notebooks.azure.com/account/signin#)
2. [Create a new project.](https://notebooks.azure.com/home)
3. Create a new Python notebook.

## 3. Accessing Data

The methods presented in Azure Notebook include:

1. [Use curl to retrieve a file from GitHub](https://2018dataaccess-menziess.notebooks.azure.com/j/notebooks/Access%20your%20data%20in%20Azure%20Notebooks.ipynb#curl)
2. [Use a REST API to retrieve online data](https://2018dataaccess-menziess.notebooks.azure.com/j/notebooks/Access%20your%20data%20in%20Azure%20Notebooks.ipynb#restapi)
3. [Query an Azure SQL database](https://2018dataaccess-menziess.notebooks.azure.com/j/notebooks/Access%20your%20data%20in%20Azure%20Notebooks.ipynb#azuresql)
4. [Access Azure Table Storage](https://2018dataaccess-menziess.notebooks.azure.com/j/notebooks/Access%20your%20data%20in%20Azure%20Notebooks.ipynb#tablestorage)
5. [Access Azure Blobs](https://2018dataaccess-menziess.notebooks.azure.com/j/notebooks/Access%20your%20data%20in%20Azure%20Notebooks.ipynb#blobs)

   [Share access to Azure Storage through Shared Access Signatures](https://2018dataaccess-menziess.notebooks.azure.com/j/notebooks/Access%20your%20data%20in%20Azure%20Notebooks.ipynb#sharedaccess)

**Tip:** bonus Azure databases.

### 3.1 Downloading File

Download a file using curl:

```bash
!curl https://raw.githubusercontent.com/petroleum101/figures/db46e7f48b8aab67a0dfe31696f6071fb7a84f1e/oil_price/oil_price.csv -o ../oil_price_temp.csv
```

Read in the data using pandas:

```python
import pandas
dataframe_file = pandas.read_csv('../oil_price_temp.csv')
dataframe_file.head()
```

### 3.2 Http Requests



### 3.3 Azure SQL Databases



### 3.4 Azure Table Storage



### 3.5 Azure Blobs

## 4. Running ML Models

## 5. Deploy Web Service

