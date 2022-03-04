---

title: "GCP ComputeEngineHook"
linkTitle: "GCP ComputeEngineHook"
tags: [adaptor, gcp] 
categories: ["adaptors"]
weight: 100
description: >-
     Apache Airflow hook for Google Compute Engine APIs.
---

### Description

Hook for Google Compute Engine APIs. All the methods in the hook where project_id is used must be called with keyword arguments rather than positional.



**Release:** 6.4.0

**Date:** 20.01.2022

### Content

- ...



### Installation

Install the Google provider package into your Airflow environment.

```
`pip install apache-airflow-providers-google`
```

Import the module into your DAG file and instantiate it with your desired params.

```
`from airflow.providers.google.cloud.hooks.compute import ComputeEngineHook`
```



### PIP Requirements

| PIP PACKAGE | VERSION REQUIRED |
| :------------- | :--- |
| n/a | n/a |
|  |  |



### Prerequisites

None



### Changelog

**6.4.0**

**Features**

- ...
