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
package-name: "ferris-providers-service_provider"
name: "Service_Provider"
description: |
    `ServiceProvider <https://serviceprovider.com/>`__

# Overview of the supported service_provider versions
versions:
  - 2.0.2
  - 2.0.1
  - 2.0.0
  - 1.0.3
  - 1.0.2
  - 1.0.2
  - 1.0.1
  - 1.0.0

# Additional dependecies are listed if existing
additional-dependencies:
  "- ferris docker image verion>=3.0.3

# Additional integrations with the service provider of choice
integrations:
  - integration-name: "Service Provider"
    external-doc-url: "https://serviceprovider.com/""
    how-to-guide:
     "- /docs/adaptors/aws-s3createbucketoperator/
     "- /docs/adaptors/azure-azurebasehook1/
    logo: "/integration-logos/serviceprovider/Serviceprovider.png"
    tags: [service]
  - integration-name: "Service_Provider SQL"
    external-doc-url: "https://serviceprovider.com/product/serviceprovider-sql
    how-to-guide:
      "- /docs/adaptors/aws-s3createbucketoperator/
      "- /docs/adaptors/azure-azurebasehook1/
    logo: "/integration-logos/serviceprovider/serviceprovider.png"
    tags: [service]

# Additional integrations with the python modules of the Service Provider
operators:
  - integration-name: "Service_Provider"
    python-modules:
      "- ferris.providers.serviceprovider.operators.serviceprovider.py
  - integration-name: "ServiceProvider SQL"
    python-modules:
      "- ferris.providers.serviceprovider.operators.serviceprovider_sql

# Hook integration with the Service Provider of choice
hooks:
  - integration-name: "ServiceProvider"
    python-modules:
      "- ferris.providers.serviceprovider.hooks.serviceprovider
      "- ferris.providers.serviceprovider.hooks.serviceprovider_base
  - integration-name: "ServiceProvider SQL"
    python-modules:
      "- ferris.providers.serviceprovider.hooks.serviceprovider_sql

# Hook class names if existing
hook-class-names:
  "- ferris.providers.serviceprovider.hooks.serviceprovider.ServiceproviderHook

# Overview of the connection-types if existing
connection-types:
  - hook-class-name: "ferris.providers.serviceprovider.hooks.serviceprovider.ServiceproviderHook"
    connection-type: "serviceprovider"
  - hook-class-name: "serviceprovider.providers.serviceprovider.hooks.serviceprovider_sql.ServiceproviderSqlHook"
    connection-type: "serviceprovider"
```

Please refer to FerrisLabs [DX Samples](https://github.com/Ferris-Labs/dx_samples "DX Samples") on GitHub for further usage and integration samples.