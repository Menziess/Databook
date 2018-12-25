---
description: Quick tutorial.
---

# Azure

## 1. Introduction

Azure is a cloud computing platform that offers PaaS, IaaS and SaaS, supporting many languages and frameworks. 

* **On Premise:** 
* **PaaS \(Cloud Native\):** Platform as a Service
* **IaaS:** Infrastructure as a Service
* **SaaS:** Software as a Service

![](../.gitbook/assets/image%20%288%29.png)

Services / Resources:

* [**Compute:**](https://www.tutorialspoint.com/microsoft_azure/microsoft_azure_compute_module.htm) ****Web Apps, VM's, Mobile Service, Cloud Service, Batch Service
* \*\*\*\*[**Storage:**](https://docs.microsoft.com/en-us/azure/storage/) Blob Container, Tabular \(Cassandra\), Queue, File Share, Data Lake
* **Network:** 
* **Processing Big Data:** 
* **Messaging:** 
* **Caching:** 
* **Identity and Access:** 
* **Mobile:** 
* **Backup:** 

## 2. Installation

Create free account and install azure-cli: 

{% code-tabs %}
{% code-tabs-item title="https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest\#install" %}
```bash
sudo apt install apt-transport-https lsb-release software-properties-common -y

AZ_REPO=$(lsb_release -cs)

echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```bash
sudo apt-key --keyring /etc/apt/trusted.gpg.d/Microsoft.gpg adv --keyserver packages.microsoft.com --recv-keys BC528686B50D79E339D3721CEB3E94ADBE1229CF
```

```bash
sudo apt-get update 
sudo apt-get install azure-cli
```

Login:

```bash
az login -u <username> -p <password>
```

## 3. Managing Resources

A clear hierarchical structure simplifies management of resources. A tenant is a representation of an organization, a dedicated instance of [Azure Active Directory](https://azure.microsoft.com/en-us/trial/get-started-active-directory/) that registers and manages apps, and the users and systems that have access to them. A company may have multiple subscriptions to separate concerns. Each subscription \(department\) can have multiple resource groups \(systems\), that hold multiple resources \(services\), which again can have subresources: 

#### Tenant [➙](https://www.toptal.com/designers/htmlarrows/arrows/heavy-right-arrow/) Subscriptions [➙](https://www.toptal.com/designers/htmlarrows/arrows/heavy-right-arrow/) Resource Groups [➙](https://www.toptal.com/designers/htmlarrows/arrows/heavy-right-arrow/) Resources [➙](https://www.toptal.com/designers/htmlarrows/arrows/heavy-right-arrow/) Subresources

### 3.1 ARM Azure Resource Manager

The infrastructure of an application is typically made up of many different components, which should ideally be deployed, managed and monitored as a group. ARM provides a secure way to manage resources using a template, the portal, or the Azure CLI.

It is important to know that CLI tools use REST requests to the Azure portal in the background. The portal generates the templates that deploy extra resources.

**Tip:** An important concept in every deployment request is [idempotence](../vocabulary.md).

### 3.2 ARM Template

Templates offer a way to describe resource deployment in a declarative way. Templates are idempotent.

### 3.3 Portal

The [portal](https://portal.azure.com/) makes an http request to the ARM API in the background, which is idempotent.

### 3.4 Azure CLI

The CLI tool makes https requests to the ARM API in the background, so it's also idempotent.

### 3.5 SDK's C\#, Python, Java, etc...

Resources can be created with language-specific SDK's.

## 4. ARM Templates

### 4.1 Modes

Specifying the `--mode` flag: 

* **Incremental:** Resources not specified will be left untouched 
* **Complete:** Resources not specified will be destroyed

### 4.2 Generic structural template:

```text
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for all resources."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "location": "[parameters('location')]",
      "apiVersion": "2018-07-01",
      "sku": {
        "name": "[parameters('storageAccountType')]"
      },
      "kind": "StorageV2",
      "properties": {}
    }
  ],
  "outputs": {
    "storageAccountName": {
      "type": "string",
      "value": "[variables('storageAccountName')]"
    }
  }
}


```

Deploy the template:

```bash
az group deployment create --name test -g MyResourceGroup --template-file azuredeploy.json
```

### 4.3 Parameters template:

```text
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "value": "Standard_GRS"
    },
    "name": {
      "value": "stefanschenkresource"
    }
  }
}
```

Deploy using command:

```bash
az group deployment create --name test -g MyResourceGroup --template-file azuredeploy.json --parameters azuredeploy.parameters.json
```

## 5. Azure CLI

Login and create resource group:

```bash
az login -u <username> -p <password>

az account list --output table

az account set -s <id>

az group create --location westeurope --name <groupname>
```

Create Storage Account:

```bash
az storage account create -n <storageaccountname> -g <resourcegroupname> -l <datacenterlocation>
```

## 6. Data Factory

A data factory is an automated [pipeline](https://docs.microsoft.com/en-us/azure/data-factory/v1/data-factory-create-pipelines) where activities such as ingestion, processing and publishing can be [scheduled](https://docs.microsoft.com/en-us/azure/data-factory/v1/data-factory-scheduling-and-execution).

![A Data Factory Pipeline](../.gitbook/assets/image%20%284%29.png)

**Tip:** follow along with a [tutorial](https://docs.microsoft.com/en-us/azure/data-factory/quickstart-create-data-factory-portal) to set up a pipeline.

First, a storage account is required within a resource group to have a place to ingest the data:

1. Create a new blob container
2. Upload a text file named "emp.txt" in the advanced tab, to the folder called "input", containing:
3. `John, Doe  Jane, Doe`

We have a blob container containinig a txt file. Now we need a data factory:

1. Open a new browser tab with the Azure portal
2. Create a new resource, under Analytics select Data Factory
3. Enter a name and click create
4. When it's created, click on Author and Monitor

Create a linked service:

1. In the newly opened tab, click Author
2. In the left bottom under Connections, create a new Linked Service
3. Select Azure Blob Storage, enter subscription etc, and press Test Connection, and Finish

Create datasets:

1. Create a new Dataset
2. Choose Azure Blob Storage
3. Enter "InputDataset" as name
4. Under Connection select the linked service and click browse to select the emp.txt file
5. Repeat the steps to create the output dataset

Create a pipeline:

1. Create a pipeline
2. Give it a name, then pick Copy Data under Move & Transform
3. Select the source and sink \(InputDataset and OutputDataset\)

Debugging the pipeline:

1. Click debug in the pipeline tab
2. In the first browser tab \(that you held open hopefully\), verify that the output file has been created

Publishing, triggering and monitoring the pipeline:

1. Instead of debug, click trigger
2. Monitor the pipeline by clicking the monitor tab in the left sidebar

This has been a simple copy operation, but it can easily be expanded to be a more complex process. The tutorial goes on to describe scheduling as well.

## 7. Additional 

There are many tools and information with respect to solutions that Azure offers, for example:

{% embed url="https://azure.microsoft.com/en-us/services/hdinsight/" %}

{% embed url="https://www.terraform.io/" %}

{% embed url="https://azure.microsoft.com/nl-nl/features/storage-explorer/" %}



