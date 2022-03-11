---

title: "Azure Base Hook"
linkTitle: "Azure Base Hook"
tags: [adaptor, azure] 
categories: ["adaptors"]
weight: 100
description: >-
     Ferris base hook for Azure services.
---

### Description

This hook acts as a base hook for azure services. It offers several authentication mechanisms to authenticate the client library used for upstream azure hooks.



**Release:** 3.6.0

**Date:** 09.02.2022



### Installation

Install the following supporting libraries to the Excutor image.

```python
pip install azure-batch
pip install azure-cosmos
pip install azure-datalake-store
pip install azure-identity
pip install azure-keyvault
pip install azure-kusto-data
pip install azure-mgmt-containerinstance
pip install azure-mgmt-datafactory
pip install azure-mgmt-datalake-store
pip install azure-mgmt-resource
pip install azure-storage-blob
pip install azure-storage-common
pip install azure-storage-file
```

Import the module into your execution package file and instantiate it with your desired parameters.

```
TBD
```

Please refer to FerrisLabs DX Samples on GitHub **TBD** for further usage and integration samples.

### PIP Requirements

| PIP PACKAGE | VERSION REQUIRED |
| :------------- | :--- |
| [`azure-batch`](https://pypi.org/project/azure-batch/ "Azure Batch") | `>=8.0.0`          |
| [`azure-cosmos`](https://pypi.org/project/azure-cosmos/ "Azure Cosmos") | `>=4.0.0,<5`       |
| [`azure-datalake-store`](https://pypi.org/project/azure-datalake-store/ "Azure Data Lake Store") | `>=0.0.45`         |
| [`azure-identity`](https://pypi.org/project/azure-identity/ "Azure Identity") | `>=1.3.1`          |
| [`azure-keyvault`](https://pypi.org/project/azure-keyvault/ "Azure KeyVault") | `>=4.1.0`          |
| [`azure-kusto-data`](pip install azure-kusto-data "Azure Kusto Data") | `>=0.0.43,<0.1`    |
| [`azure-mgmt-containerinstance`](https://pypi.org/project/azure-mgmt-containerinstance/ "Azure Mgmt Container Instance") | `>=1.5.0,<2.0`     |
| [`azure-mgmt-datafactory`](https://pypi.org/project/azure-mgmt-datafactory/ "Azure Mgmt Data Factory") | `>=1.0.0,<2.0`     |
| [`azure-mgmt-datalake-store`](https://pypi.org/project/azure-mgmt-datalake-store/ "Azure Mgmt Data Lake Store") | `>=0.5.0`          |
| [`azure-mgmt-resource`](https://pypi.org/project/azure-mgmt-resource/ "Azure Mgmt Resource") | `>=2.2.0`          |
| [`azure-storage-blob`](https://pypi.org/project/azure-storage-blob/ "Azure Storage Blob") | `>=12.7.0,<12.9.0` |
| [`azure-storage-common`](https://pypi.org/project/azure-storage-common/ "Azure Storage Common") | `>=2.1.0`          |
| [`azure-storage-file`](https://pypi.org/project/azure-storage-file/ "Azure Storage File") | `>=2.1.0`          |



### Parameters

- **sdk_client**: The SDKClient to use
- **conn_id**: The Azure connection id which refers to the information to connect to the service.
