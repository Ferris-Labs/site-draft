---

title: "AWS S3CreateBucketOperator"
linkTitle: "AWS S3CreateBucketOperator"
tags: [adaptor, aws] 
categories: ["adaptors"]
weight: 100
description: >-
     This operator creates an S3 bucket.
---

### Description

This operator creates an S3 bucket. For more information on how to use this operator, take a look at the guide: [Create and Delete Amazon S3 Buckets](https://airflow.apache.org/docs/apache-airflow-providers-amazon/stable/operators/s3.html#howto-operator-s3createbucketoperator)



**Release:** 3.0.0

**Date:** 26.02.2022

### Content

- ...



### Installation

Install the Amazon provider package into your Airflow environment.

```
`pip install apache-airflow-providers-amazon`
```

Import the module into your DAG file and instantiate it with your desired params.

```
`from airflow.providers.amazon.aws.operators.s3 import S3CreateBucketOperator`
```



### PIP Requirements

| PIP PACKAGE | VERSION REQUIRED |
| :------------- | :--- |
| n/a | n/a |
|  |  |



### Parameters

- **bucket_name:** This is bucket name you want to create
- **aws_conn_id:** The Airflow connection used for AWS credentials. If this is None or empty then the default boto3 behaviour is used. If running Airflow in a distributed manner and aws_conn_id is None or empty, then default boto3 configuration would be used (and must be maintained on each worker node).
- **region_name:** AWS region_name. If not specified fetched from connection.



### Changelog

**3.0.0**

**Features**

- ...
