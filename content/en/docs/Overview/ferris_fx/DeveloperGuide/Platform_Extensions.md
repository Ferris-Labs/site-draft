---
title: "Extending the Platform"
linkTitle: "Extending the Platform"
tags: [ developer guide, guide, extensions, platform ]
categories: [ ]
description: >-
    Extending the Platform.
---

## Extending the Platform

The platform may be extended at 3 logical points within the event life cycle.

* **At Entry Point:**
    * They are respnsible for injecting external event streams into the platform. Primarily they mediate betweeen the
      external event stream and the internal CloudEvents based Kafka Topics. These run on separate containers within the
      platform. The following are the typical examples.
        * **Event Gateway**: are the primary mechanism. To build event gateways we provide templates. Please check this
          document on extension.
* **At Processing**
    * These are extensions that operate on internal event streams or are required by services that are created on the
      platform. The following are the types thereof.
        * **Configuration Adapters and UIs.** These are primarily used for connection setups and configurations which
          are applicable across the platform. Examples are the variety of connection set up UIs we provide. They are
          very easy to create. Use the the followinng guide to build your own.
        * **Python Libraries and Modules:** These are attached to the executor. It primarily involves extending the
          executor image with the required library. In order to add them to the platform use this guide.
        * **Event Processing Packages**: These are services that only modify event attributes normally convert one type
          of event to another. These can be implemented as services within the platform. Please see following guide to
          see how they are used and some typical scenarios.
        * **No Code Generators:** Generators combine UI based with templated code to allow No Code based approach to
          creating services. Please check this guide on how that works.
* **At Exit Point**
    * These are primarily modules that interact with external systems but operate across the entire example. They
      primarily operate on streams that originate from within the platform and communicate with the outside. These run
      on separate containers within the platform. The following are typical implementaions:
        * **Protocol Adapters** They adapt between the internal Kafka even streams and external protocols for example
          webhook adapter, Kafka to imbm mq adapter etc. Their primary purpose is to offload activity from the platform
          which may cause bottle necks or require long running services.
        * **Splitters and Filters:** These may operate on streams to split content or event infromation into derivative
          streams. Or feed data into supporting infrastructure. The Elasticsearch and Splunk adapters are typical
          examples. In order to build these use the following guide and related templates.



