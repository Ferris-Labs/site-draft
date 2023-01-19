---
title: "Architecture"
linkTitle: "Architecture"
weight: 6
description: >
  Ferris SX Architecture.
---

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
