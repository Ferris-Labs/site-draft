---

title: "Azure AzureBaseHook"
linkTitle: "AzureBaseHook"
tags: [adaptor, azure] 
categories: ["adaptors"]
weight: 100
description: >-
     Apache Airflow base hook for Azure services.
---

### Description

This hook acts as a base hook for azure services. It offers several authentication mechanisms to authenticate the client library used for upstream azure hooks.



**Release:** 3.6.0

**Date:** 09.02.2022

### Content

- ...



### Installation

Install the Microsoft Azure provider package into your Airflow environment.

```
`pip install apache-airflow-providers-microsoft-azure`
```

Import the module into your DAG file and instantiate it with your desired params.

```
`from airflow.providers.microsoft.azure.hooks.base_azure import AzureBaseHook`
```



### PIP Requirements

| PIP PACKAGE | VERSION REQUIRED |
| :------------- | :--- |
| n/a | n/a |
|  |  |



### Parameters

- **sdk_client**: The SDKClient to use
- **conn_id**: The Azure connection id which refers to the information to connect to the service.



### Changelog

**3.6.0**

**Features**

- ...
