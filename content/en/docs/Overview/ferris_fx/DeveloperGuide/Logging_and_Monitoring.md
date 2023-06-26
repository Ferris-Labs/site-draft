---
title: "Logging and Monitoring"
linkTitle: "Logging and Monitoring"
description: >-
    Development Lifecycle of an FX Service.
---

Ferris FX aggregates all operational data into Elasticsearch. Most operational data and events are transported through
Kafka from which it is placed in Elasticsearch by Elasticsearch Sink containers.

## Logs

Contains Logs from all applications.

## Events

All events that are transported through the `ferris.events` topic are loaded into Elasticsearch Index.

## Checking Logs

Ferris Logs are in logstash format. The logs can be aggregated from the application by using the ferris_cli library.

Logs are identified by the app_name attribute which provides you with an indication of the application from which it was
generated.

To Filter Application Logs use the following: `app_name

## Checking Events

Events are in form of cloud events. The data section of an event is schema less i.e. the data provided in the attributes
may vary from event type to event type. If you require custom extractions for specific event types the best is to tap
into the event namespace.


