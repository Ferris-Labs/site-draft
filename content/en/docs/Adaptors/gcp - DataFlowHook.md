---

title: "GCP DataFlowHook"
linkTitle: "GCP DataFlowHook"
tags: [adaptor, gcp] 
categories: ["adaptors"]
weight: 100
description: >-
     Apache Airflow hook for Google Dataflow.
---

### Description

Hook for Google Dataflow. All the methods in the hook where project_id is used must be called with keyword arguments rather than positional.



**Release:** 6.4.0

**Date:** 13.02.2022

### Content

- ...



### Installation

Install the Google provider package into your Airflow environment.

```
`pip install apache-airflow-providers-google`
```

Import the module into your DAG file and instantiate it with your desired params.

```
`from airflow.providers.google.cloud.hooks.dataflow import DataflowHook`
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
