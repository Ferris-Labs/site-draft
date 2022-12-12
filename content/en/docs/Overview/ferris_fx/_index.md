---
title: "Ferris FX"
linkTitle: "Ferris FX"
weight: 1
description: >
  The following section provides a short overview of key features, concepts and architecture of Ferris FX.
---

## Overview

**FerrisFX** is a platform for building highly scalable, cross-network  sync or async microservices and agents.

The unique low learning curve approach significantly reduces the cost of deploying enterprise wide process and integration pipelines across disparate systems at a speed.  While at the same time creating a platform with practically unbound access and ease of integration.  

FX is a ground-up rethink of how both sync and async microservices are built in multi-cloud, highly volatile and fragmented software environments.

**On FX you are effectively writing large applications by connecting “blocks” of code (Services) through Events.** An approach that is highly intuitive and in line with iterative agile practices.

The following is a brief review of some of the benefits and features of FerrisFX. Upcoming features are shown in italics.

| Quality                                                    | Description                                                  |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| **Low Learning Curve**                                     | Developers can practically learn within an hour how to work with FX. |
| **Highly Scalable**                                        | Built from ground-up for scalability. The event messaging core is based on an Apache Kafka backbone we can transmit MILLIONs of jobs per day to any number of Services without break. |
| **Resource Efficient**                                     | FX Microservices are deployed in real time as Events comes in. There are not 100s of microservice containers running on your platform. Just 3 components. The Ferris Manager UI, The Event Router and any number Executors. |
| **Plug into anything. Practically Limitless Integrations** | Leverage the whole universe of Library capabilites of Python ( Java, DOTNET or GoLang coming soon) , no need to depend solely on paid pre-packaged modules based on a strict structure and complicated build procedures and vendor lock-in. No-Code or Low-Code take your pick. |
| **Combined Support for Sync and Async Microservices**      | *Manage both your Async and Sync Service Mesh in a single interface without any expensive and cumbersome 3rd party system.  Reduce the complexity of your infrastructure and the number of components.* |
| **Fully Containerised and Easy to Deploy**                 | *Pre-packaged Kubernetes Templates with minimal customisation requirements fit straight into your enterprise Kubernetes(and if you dont have one we will build you one). Run in 1 command and Scale as you wish*. |
| **All Ops Data in 1 Secure place**                         | We record all events, logs, alerts in Kafka and store them in daily index within Elasticsearch for easy search and loading it into other systems such as Splunk, DataDog, LogTrail etc. A single scalable fault tolerant system to transport events and operational data. |
| **Monitor Performance**                                    | All Service Executions are continuously tracked and recorded by FX allowing you to easily identify bottlenecks in your processing. Execution details can be viewed on the UI or within Kibana/Elasticsearch. |
| **Enterprise Friendly User and Project Management**        | FX can be easily plugged into your identity infrastructure whether OIDC or AD or SAML we support them all. Packages are organised by Projects enabling users to have specific roles and simplify oversight and governance of your platform. Further enhanced by tagging support promoting an enterprise wide shared semantics and Taxonomy of packages. |
| **Structured Service Documentation**                       | *Provide a readme.md file with your package to document it for users.  Provide an OpenAPI document to automatically expose the end point and document it for users.* *Provide a manifest JSON file for describing package.* |
| **Developer Friendly GIT integration**                     | Fits just straight into existing flow. Push to git to activate code. No more, No Less. |
| **Simple Standard and Powerful Event Format**              | Based on Cloud Events our event format is Simple JSON which developer already know how to work with. If you know how to read JSON you can build a Microservice. |
| **Simple Easy to understand and use conventions**          | A Microservice consists of a set of scripts run in sequence, receives events as JSON and sends events as JSON. Use a config.json to store configs, use a secrets.json to store secrets. Store files in /tmp. You can use any Python libraries and also deploy your won packages with each service. |
| **Selective Feature Support**                              | Our 'Everything is Optional' approach to the convetions support by services means that developers can incrementally improve the quality of their code as they get more familiar with the system. A base service is just a single script and then they can build up to support configurations, UI, reusable packages,  published interface packages or custom image execution. |
| **Support for Enterprise Specific Library Distributions**  | Package Enterprise Specific Libraries into the base executor for use by all executors within the enterprise. Saving Huge amounts of development time. |
| **Real Time Code Updates**                                 | Our near real time deploy means code changes are immediately active. |
| **Run AB Testing with Ease**                               | Plug different code versions to same event to measure differences. |
| **RUN Anything**                                           | *Our unique RUN ANYTHING architecture furthers breaks boundaries of running polyglot container systems. Simply tell the system on which image a code is to execute.* |
| **Activate or Deactivate Services in Realtime**            | Services can be activated when you need them.                |
| **Instant Scaling**                                        | Just increase the number of Router or Executor replicas to process faster (provided your underlying services can support it) |
| **View Logs in Realtime**                                  | *View the Logs of any executor in Realtime directly on the Management UI.* |
| **View Event Dependencies Easily**                         | Have an error? Trace easily the events which led to the Error with all the parameters used to run the event flow. |
| **UI Support for Microservices**                           | Drop in a metadata.json file to auto generate UIs for entering parameters for a specific package. |
| **Easy Aggregated Logging**                                | All services logs are aggregated and searchable and viewable in realtime. Developers can log easily. |
| **Adaptive Event Schema**                                  | FX is continuously scanning the incoming events to populate the event catalog and their schema. Making it easier for developers to write services which react to the platform events. Continuously updating you on the Events within your platform. |
| **Parallel Event Processing and Flows**                    | The same Event can be sent to multiple services for processing. Enabling multiple flows to be triggered. |
| **Anonymous and Published Interfaces**                     | *Services can easily standardise and publish their interfaces making them available in the 'No-Code' flows.* |
| **Event Mapping**                                          | *Easily map parameters of one event to another event. Allowing you to easily link event flows together.* |
| **Event Tagging**                                          | Tag events. Enabling you to organise event groups by domain. |
| **Execution Prioritisation and Cancellation**              | *Granular queue management to prioritise or cancel specific executions if there is a backlog.* |
| **Modular Easily Extendible UI**                           | Add modular custom UIs to the management interface using FX extensions to the Flask App Builder for creating a custom Management UI. |
