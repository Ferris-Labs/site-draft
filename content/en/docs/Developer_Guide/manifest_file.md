---
title: "The Manifest File of an FX Service"
linkTitle: "The Manifest File"
weight: 203
description: >-
     Manifest File Definition
---
The manifest.json file is used to provide information about your application to the DX Platform as well as to other users and developers.

The following is a sample manifest.json file.


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
| description     | Description of the service                                                                                                   |
| entrypoint      | Script that will be executed on service execution                                                                          |                                                                         |
| execution_order | Sequence in which scripts will be executed. If both `entrypoint` and `execution_order` are defined `entrypoint` will be used. 
|tags| An array of tags for service                                                                                                   |
|trigger_events| Array of events that will trigger service execution                                                                         |
|schedule| Optional. Cron like definition of service scheduled executions                                                                       |
|allow_manual_triggering| Indicates whether service can be triggered manally or not|
|active| Indicates service is active or inactive|
