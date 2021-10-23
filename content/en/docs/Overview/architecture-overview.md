---
title: "Architecture Overview"
linkTitle: "Architecture Overview"
weight: 100
description: >-
     An Overview of the architecture of FerrisFX.
---

## FerrisFX Architecture Overview

The following provides an in-depth overvew of the FerrisFX Architecture

## Required Infrastructure

The following are the infrastructure components required for a FerrisFX installation

| Component                  | Descriptio                                                   |
| -------------------------- | ------------------------------------------------------------ |
| Apache Kafka and Zookeeper | Apache Kafka serves as the backbone to pass events and operational data within a FerrisFX Installation. |
| PostgresSQL                | Postgres is used as the database for the Ferris Webserver Application. |
| Consul                     | Consul is the configuration store used by the FerrisFX installation. It is also used by the services to store their configurations. |
| Elasticsearch              | Elasticsearch is used as a central store for all operational data. Thereby making the data easiliy searchable. |
| Kibana                     | Kibana is used to view and query the data stored in Elasticsearch. |
| FerrisFX-Management-Server | FerrisFX management Server is the main UI used for all activities on the FerrisFX platform. |
| FerrisFX-Gateway           | The Gateway container is responsible for listenting to events flowing through the system and forwarding the events to the appropriate micro-services that you create. |
| FerrisFX-Executor          | The executor container(s) is where the code gets executed.   |

## Understanding the FerrisFX Flow

The FerrisFX platform is intended as an Async platform and therefore at the core of the system messages are passed through the Kafka Message Bus. These 'events' are JSON formatted messages which adhere to the CloudEvents format. 

![image-20211023085329814](/images/diagram_1.png)

Each message consists of what may be simplified as Headers and Payload. The headers indicate the type of event and other attributes. Whereas the payload are the attributes or parameters that are sent out by Services in order to either provide information about their state or for usage by downstream Services.

The FX gateway is listening on the stream ofEvents passing through Kafka. Based on the configuration of the platform the gateway decides if a Service requires to be executed based on the Event contents. On finding a configured Handler the gateway sends a message to the Executor and informs it of which packages or scripts required to be run.

The Executor downloads the package from the Minio storage and executes the package. The Execuor sends a series of messages on package execution and maintains track of the state of teh execution and the metrics. These are once again processed by the gateway and stored either in Postgres or in Elasticsearch based on the tyep of message and the contents.
