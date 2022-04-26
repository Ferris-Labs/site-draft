---

title: "AWS S3 Bucket Operator"
linkTitle: "AWS S3 Bucket Operator"
tags: [adaptor, aws] 
categories: ["adaptors"]
weight: 100
description: >-
     This operator creates an S3 bucket.
---

### Description

This operator creates and uses a S3 bucket. For more information on AWS S3 Bucket creation, deletion and configurations, visit [Boto3AWSBucket](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/s3.html#bucket "Boto3AWSBucket").



**Release:** 3.0.0

**Date:** 26.02.2022



### Installation

Install the following supporting libraries to the Excutor image.

```python
pip install boto3
pip install --upgrade jsonpath-ng
pip install pandas
pip install redshift_connector
pip install sqlalchemy-redshift
pip install watchtower
```

Import the module into your execution package file and instantiate it with your desired parameters.

```python
import boto3
from aws_session import session
```

Please refer to FerrisLabs DX Samples on GitHub [AWS Integration](https://github.com/Ferris-Labs/dx_samples/tree/main/integration_aws) for further usage and integration samples.

### PIP Requirements

| PIP PACKAGE | VERSION REQUIRED |
| :------------- | :--- |
| [`boto3`](https://pypi.org/project/boto3/ "Boto3") | `>=1.15.0,<2.0.0` |
| [`jsonpath_ng`](https://pypi.org/project/jsonpath-ng/ "JSONPath") | `>=1.5.3` |
| [`pandas`](https://pypi.org/project/pandas/ 'pandas') | `>=0.17.1, <1.4` |
| [`redshift_connector`](https://pypi.org/project/redshift-connector/ "RedShift Connector") | `~=2.0.888` |
| [`sqlalchemy_redshift`](https://pypi.org/project/sqlalchemy-redshift/ "SQLAlchemy RedShift") | `~=0.8.6` |
| [`watchtower`](https://pypi.org/project/watchtower/ "WatchTower") | `~=2.0.1` |



### Parameters

- **bucket_name:** This is bucket name you want to create
- **aws_conn_id:** The Ferris connection used for AWS credentials. If this is None or empty then the default boto3 behaviour is used. If running Ferris in a distributed manner and aws_conn_id is None or empty, then default boto3 configuration would be used (and must be maintained on each worker node).
- **region_name:** AWS region_name. If not specified fetched from connection.
