---
title: "Architecture"
linkTitle: "Architecture"
weight: 6
description: >
  Ferris SX Architecture.
---

## Ferris SX Architecture Principles

Stream processing is a technique for processing large volumes of data
in real-time as it is generated or received. One way to implement a
stream processing architecture is to use Docker containers for
individual workflow steps and Apache Kafka for the data pipeline.

Docker is a platform for creating, deploying, and running containers,
which are lightweight and portable units of software that can be run
on any system with a compatible container runtime. By using Docker
containers for each step in the stream processing workflow, developers
can easily package and deploy their code, along with any dependencies,
in a consistent and reproducible way. This can help to improve the
reliability and scalability of the stream processing system.

Apache Kafka is a distributed streaming platform that can be used to
build real-time data pipelines and streaming applications. It provides
a publish-subscribe model for sending and receiving messages, and can
handle very high throughput and low latency. By using Kafka as the
backbone of the data pipeline, developers can easily scale their
stream processing system to handle large volumes of data and handle
failover scenarios.

Overall, by using Docker containers for the individual workflow steps
and Apache Kafka for the data pipeline, developers can create a stream
processing architecture that is both scalable and reliable. This
architecture can be used for a wide range of use cases, including
real-time analytics, event-driven architectures, and data integration.

Below is the high-level architecture diagram of Ferris SX:

![ferris_sx_architecture](/images/ferris_sx_architecture.png)


## Required Infrastructure

The following are the infrastructure components required for a FerrisSX installation

| Component         | Description                                                                                                                                                         |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Apache Kafka      | Apache Kafka serves as the backbone to pass events and operational data within a FerrisSX Installation.                                                             |
| PostgreSQL        | Postgres is used as the database for the FerrisSX Management Application.                                                                                           |
| Consul            | Consul is the configuration store used by the FerrisSX platform. It is also used by the services to store their configurations.                                     |
| MinIO             | Minio provides the platform internal storage for scripts and assets used by the Services.                                                                           |
| Elasticsearch     | Elasticsearch is used as a central store for all operational data. Thereby making the data easiliy searchable.                                                      |
| Kibana            | Kibana is used to view and query the data stored in Elasticsearch.                                                                                                  |
| FerrisSX-Manager  | FerrisSX Manager is the main UI used for all activities on the FerrisFX platform.                                                                                   |
| FerrisFX-Router   | The Route container is responsible for listening to events flowing through the system and forwarding the events to the appropriate micro-services that you create. |
| FerrisFX-Executor | The executor container(s) is where the code gets executed.                                                                                                          |
