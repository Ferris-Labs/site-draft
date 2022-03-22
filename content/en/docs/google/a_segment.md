---
title: "segment"
linkTitle: "segment"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     segment Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.segment_track_event"></a>

# operators.segment\_track\_event

<a id="operators.segment_track_event.SegmentTrackEventOperator"></a>

## SegmentTrackEventOperator Objects

```python
class SegmentTrackEventOperator(BaseOperator)
```

Send Track Event to Segment for a specified user_id and event

**Arguments**:

- `user_id`: The ID for this user in your database. (templated)
- `event`: The name of the event you're tracking. (templated)
- `properties`: A dictionary of properties for the event. (templated)
- `segment_conn_id`: The connection ID to use when connecting to Segment.
- `segment_debug_mode`: Determines whether Segment should run in debug mode.
Defaults to False

<a id="hooks"></a>

# hooks

<a id="hooks.segment"></a>

# hooks.segment

This module contains a Segment Hook
which allows you to connect to your Segment account,
retrieve data from it or write to that file.

NOTE:   this hook also relies on the Segment analytics package:
        https://github.com/segmentio/analytics-python

<a id="hooks.segment.SegmentHook"></a>

## SegmentHook Objects

```python
class SegmentHook(BaseHook)
```

Create new connection to Segment

and allows you to pull data out of Segment or write to it.

You can then use that file with other
Airflow operators to move the data around or interact with segment.

**Arguments**:

- `segment_conn_id`: the name of the connection that has the parameters
we need to connect to Segment. The connection should be type `json` and include a
write_key security token in the `Extras` field.
- `segment_debug_mode`: Determines whether Segment should run in debug mode.
Defaults to False

.. note::
    You must include a JSON structure in the `Extras` field.
    We need a user's security token to connect to Segment.
    So we define it in the `Extras` field as:
    `{"write_key":"YOUR_SECURITY_TOKEN"}`

<a id="hooks.segment.SegmentHook.on_error"></a>

#### on\_error

```python
def on_error(error: str, items: str) -> None
```

Handles error callbacks when using Segment with segment_debug_mode set to True

