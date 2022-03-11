---
title: "Ferris YAML file Template"
linkTitle: "Ferris YAML file Template"
tags: [YAML, template, quickstart] 
categories: ["YAML"]
weight: 100
description: >-
   Template file for generating detailed Ferris YAML files.
---

## ferris.yaml

YAML is a human-readable data-serialization language. It is commonly used for configuration files and in applications where data is being stored or transmitted with any programming language. YAML is a strict superset of JSON, another data serialization language. But because it's a strict superset, it can do everything that JSON can and more

Overview of how a sample YAML file is structured.

```yaml
---
# Insert the package-name from executions/packages, the name of the Service Provider and the description(service provider URL)
package-name: ferris-providers-aws-s3
name: AWS S3 Operator
description: |
    'Ferris Provider for manipulating with AWS S3 objects <https:////docs/adaptors/aws-s3operator///>`__

# Overview of the supported service_provider versions
versions:
  - 0.1.0

release:
  - 3.0.0

# Additional requirements are listed if existing
requirements:
  - ferris-cli>=2.4.0
  - boto3>=`>=1.15.0,<2.0.0

# Additional integrations with the service provider of choice
integrations:
  - integration-name: Amazon Simple Storage Service (S3)
    external-doc-url: https://aws.amazon.com/s3/
    how-to-guide:
      - /docs/adaptors/aws-s3createbucketoperator/
    tags: [aws]

# Additional integrations with the python modules of the Service Provider
operators:
  - integration-name: Amazon Simple Storage Service (S3)
    python-modules:
      - ferris.providers.aws.operators.s3_bucket
      - ferris.providers.aws.operators.s3_object

# Overview of the connection-types if existing
connection-parameters:
  - aws-secret: 
    aws-region: 
```

Please refer to FerrisLabs [DX Samples](https://github.com/Ferris-Labs/dx_samples "DX Samples") on GitHub for further usage and integration samples.