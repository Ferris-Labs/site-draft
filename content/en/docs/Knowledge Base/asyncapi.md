---
title: "async check"
linkTitle: "async check"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     async check
---

# Transfer Service 1.0.0 documentation

This service accepts something

## Table of Contents

* [Operations](#operations)
  * [SUB ferris.events.transfers.S32RedShift](#sub-ferriseventstransferss32redshift-operation)
  * [SUB ferris.events.transfers.S32DynamoDB](#sub-ferriseventstransferss32dynamodb-operation)
  * [SUB ferris.events.transfers.S32BigQuery](#sub-ferriseventstransferss32bigquery-operation)

## Operations

### SUB `ferris.events.transfers.S32RedShift` Operation

#### Message `S32RedShift`

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | - | - | - | **additional properties are allowed** |
| source_filename | string | source_filename | - | - | - |
| target_table | string | Target table | - | format (`string`) | - |

> Examples of payload _(generated)_

```json
{
  "source_filename": "string",
  "target_table": "string"
}
```



### SUB `ferris.events.transfers.S32DynamoDB` Operation

#### Message `S32DynamoDB`

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | - | - | - | **additional properties are allowed** |
| source_filename | string | source_filename | - | - | - |
| target_table | string | Target table | - | format (`string`) | - |

> Examples of payload _(generated)_

```json
{
  "source_filename": "string",
  "target_table": "string"
}
```



### SUB `ferris.events.transfers.S32BigQuery` Operation

#### Message `S32BigQuery`

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | - | - | - | **additional properties are allowed** |
| source_filename | string | source_filename | - | - | - |
| target_table | string | Target table | - | format (`string`) | - |

> Examples of payload _(generated)_

```json
{
  "source_filename": "string",
  "target_table": "string"
}
```



