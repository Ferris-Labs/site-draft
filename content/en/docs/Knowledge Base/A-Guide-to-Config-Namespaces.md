---
title: "A Guide to Config Namespaces"
linkTitle: "Config Namespaces"
weight: -10
description: >-
  A Guide to Config Namespaces.
---

## Key Concepts
Ensuring easy and consequent configuration management is very important for platforms such as DX which must integrate with a number of systems. Further each integration or connection may require to be specific to a technical service account. 

We therefor have adopted a simple yet powerful mechanism for configuration management which may already be familiar to you.

There are 2 types of configurations

- Plain Text Configurations
- Secrets

As the names suggest the plain text configurations may be viewd as plain text whereas the secrets cannot be viewed in the management UI once they are loaded to the platform. Secrets can be updated by updating the values of a named secret, they can be created and deleted but not viewed.

The storage of the configs are handled in the backend by the Key-Value store Consul. 

- The Values are held as JSON. 
- While the keys themselves have a reasonbale level of flexibility we nonetheless specify certain key spaces which are reserved/pre-defined. These keyspaces normally hold configurations which are specific to pre-built adapters or packages which are distributed with Ferris.

The following are the key namespaces.

ferris.apps.* 

ferris.packages.*

ferris.adapters.*

ferris.env

ferris



