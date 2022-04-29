---
title: "The Manifest File of an FX Service"
linkTitle: "Manifest File"
description: >-
     Manifest File Definition
---


`manifest.json` example:

```json
{
  "description": "Service with manifest file",
  "entrypoint": "app.py",
  "execution_order": ["app_1.py", "app.py"],
  "tags": ["devops"],
  "trigger_events": ["ferris.apps.minio.file_uploaded"],
  "schedule": "54 * * * *",
  "allow_manual_triggering": true,
  "active": true
}
```


| parameter       | description                                                                                                                |
|-----------------|----------------------------------------------------------------------------------------------------------------------------|
| description     | description of a service                                                                                                   |
| entrypoint      | script that will be executed on service execution                                                                          |                                                                         |
| execution_order | Order in which scripts will be executed. If both `entrypoint` and `execution_order` are defined `entrypoint` will be used. 
|tags| list of tags for service                                                                                                   |
|trigger_events| list of events that will trigger service execution                                                                         |
|schedule| cron like definition of service scheduled executions                                                                       |
|allow_manual_triggering|whether service can be triggered manally or not|
|active| whether service is active or not|
