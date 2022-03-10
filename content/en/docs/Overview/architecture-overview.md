---
title: "Architecture Overview"
linkTitle: "Architecture"
weight: -10
description: >-
     An overview of the architecture of FerrisFX.
---

## Concepts

FerrisFX is based on 2 simple concepts - **Services** and **Events**

**On FX you are effectively writing large applications by connecting “blocks” of code through Events.** 

![image-20211024081829495](/images/image-20211024081829495.png)

Each Service is a self contained piece of functionality such as loading a file, running a database view rebuild or launching a container. You can link and re-link the blocks of code at anytime you like. The source code can be as big or as tiny as you like. 

Each Service is triggered by an Event. Each Service also emits Events thereby allowing other Services to be triggered following (or during) the execution of a Service.

A Service can respond to multiple Event types, and a single Event Type may trigger multiple Services - Thereby allowing you to also extend your Application(s) on the fly with ease.

![image-20211024080659941](/images/image-20211024080659941.png)

You are not required to think in terms of pre-defined DAGS and can rapidly and iteratively build, test and deploy your applications. 

{{< blocks/lead color="primary" >}}
<div class="col">
 <p class="lead mt-1">Ferris is a platform for building highly scalable, cross-network sync or async microservices and agents. The unique low learning curve approach significantly reduces the cost of deploying enterprise wide process and integration pipelines across disparate systems at a speed. While at the same time creating a platform with practically unbound access and ease of integration.</p>
<p class="lead mt-2">On Ferris you are effectively writing large applications by connecting “blocks” of code (Services) through Events.</p>
</div>
 {{< /blocks/lead >}}

### Services

**SERVICES** are collections of scripts and modules which are executed in sequence by the **FX Executor**. 

Services are triggered by **EVENTS**, which are JSON messages which carry a header and payload. A Service can be Linked to one or more events.

Each script is provided with the Payload of the Event that triggered it. It is the job of the **FX Router** to send Events to the appropriate Service.

The following is a basic Service which parses the event sent to it and prints the payload.

```python
import sys
import json

def hello_world(payload):
  print(payload)

payload = json.loads(sys.arg[1])

hello_world(payload)
```

### Events

Events are messages passed through the platform which are generated either by Services or by the Ferris Manager(in the case of manually triggered runs and scheduled runs).

Events are in the form of JSON formatted messages which adhere to the CloudEvents format. 

Events carry a Header which indicates the event type and a Payload (or Data section) which contain information about the event. 

The following is a sample Event.

```json
{
    "specversion" : "1.0",
    "type" : "com.example.someevent", // The Event Type
    "source" : "/mycontext",
    "subject": null,
    "id" : "C234-1234-1234",
    "time" : "2018-04-05T17:31:00Z",
    "datacontenttype" : "application/json",
    "data" : {                       // The event payload as JSON
        "appinfoA" : "abc",
        "appinfoB" : 123,
        "appinfoC" : true
    }
}
```

### Service Triggering

Services can be triggered in the following ways:

- Manually: By clicking the 'Run' button on the FerrisFX Management Server.
- On Schedule: As a cron job whereas the Cron expression is added on the UI.
- On Event: Where a package is configured to be triggered bt the FX Router when a specific type of event is observed on the platform.

Irrespective of how a Service is triggered it is always triggered by an Event. In the case of Manual and Scheduled triggering it is the FX platform that generates the trigger event.

### Late Linking

One of the most important features of the FX Platform is that you are not required to link the Service to an Event during the course of development. And you can also change the Trigger Event(s) post-deployment. 

This approach gives you a great flexibility to: 

* not having to think of pre-defined flows but to build the Flow as well as the Services iteratively.
* maintain and test multiple versions of the same Service in parallel.



## The FerrisFX Flow

At the core of the FX Platform messages (Events) are passed through **Apache Kafka**. These 'events' are JSON formatted messages which adhere to the CloudEvents format. 

![image-20211024083411584](/images/image-20211024083411584.png)

Each **Event** consists of what may be simplified as Headers and Payload. The headers indicate the type of event and other attributes. Whereas the payload are the attributes or parameters that are sent out by Services in order to either provide information about their state or for usage by downstream Services.

The **FX Router(s)** is listening on the stream of Events passing through Kafka. Based on the configuration of the platform which is managed in the **Ferris Manager UI** the Router decides if a Service requires to be executed based on the Event contents. On finding a configured Handler the gateway sends a message to the Executor and informs it of which packages or scripts are required to be run.

The **FX Executor(s)** downloads the Service from the **Minio** storage and executes the **Service**. The Service may use any Python module that is embedded in the Executor and also use **Consul** for storing its configurations. The Executor sends a series of Events on Service execution. These are once again processed by the FX Router.

![image-20211024084807506](/images/image-20211024084807506.png)

The FX Executor provides infrastructure which tracks logs, maintains record of service metrics and operational data. The Operational information is first sent to appropriate Kafka Topics from where they are picked up by Ops-Data Sinks whose role it is to store data within **Elasticsearch** and in some cases also filter the data for the purpose of alerting or anomaly tracking. All operational data may be viewed and queried through tools such as **Kibana** and is also viewable on the **FX Manager UI**.



## Required Infrastructure

The following are the infrastructure components required for a FerrisFX installation

| Component         | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| Apache Kafka      | Apache Kafka serves as the backbone to pass events and operational data within a FerrisFX Installation. |
| PostgreSQL        | Postgres is used as the database for the FerrisFX Manager Application. |
| Consul            | Consul is the configuration store used by the FerrisFX platform. It is also used by the services to store their configurations. |
| MinIO             | Minio provides the platform internal storage for scripts and assets used by the Services. |
| Elasticsearch     | Elasticsearch is used as a central store for all operational data. Thereby making the data easiliy searchable. |
| Kibana            | Kibana is used to view and query the data stored in Elasticsearch. |
| FerrisFX-Manager  | FerrisFX Manager is the main UI used for all activities on the FerrisFX platform. |
| FerrisFX-Router   | The Route container is responsible for listenting to events flowing through the system and forwarding the events to the appropriate micro-services that you create. |
| FerrisFX-Executor | The executor container(s) is where the code gets executed.   |

