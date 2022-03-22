---
title: "datadog"
linkTitle: "datadog"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     datadog Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.datadog"></a>

# sensors.datadog

<a id="sensors.datadog.DatadogSensor"></a>

## DatadogSensor Objects

```python
class DatadogSensor(BaseSensorOperator)
```

A sensor to listen, with a filter, to datadog event streams and determine

if some event was emitted.

Depends on the datadog API, which has to be deployed on the same server where
Airflow runs.

**Arguments**:

- `datadog_conn_id`: The connection to datadog, containing metadata for api keys.
- `from_seconds_ago`: POSIX timestamp start (default 3600).
- `up_to_seconds_from_now`: POSIX timestamp end (default 0).
- `priority`: Priority of your events, either low or normal.
- `sources`: A comma separated list indicating what tags, if any,
should be used to filter the list of monitors by scope
- `tags`: Get datadog events from specific sources.
- `response_check`: A check against the ‘requests’ response object. The callable takes
the response object as the first positional argument and optionally any number of
keyword arguments available in the context dictionary. It should return True for
‘pass’ and False otherwise.
- `response_check`: Optional[Callable[[Dict[str, Any]], bool]]

<a id="hooks"></a>

# hooks

<a id="hooks.datadog"></a>

# hooks.datadog

<a id="hooks.datadog.DatadogHook"></a>

## DatadogHook Objects

```python
class DatadogHook(BaseHook, LoggingMixin)
```

Uses datadog API to send metrics of practically anything measurable,

so it's possible to track # of db records inserted/deleted, records read
from file and many other useful metrics.

Depends on the datadog API, which has to be deployed on the same server where
Airflow runs.

**Arguments**:

- `datadog_conn_id`: The connection to datadog, containing metadata for api keys.

<a id="hooks.datadog.DatadogHook.validate_response"></a>

#### validate\_response

```python
def validate_response(response: Dict[str, Any]) -> None
```

Validate Datadog response

<a id="hooks.datadog.DatadogHook.send_metric"></a>

#### send\_metric

```python
def send_metric(metric_name: str,
                datapoint: Union[float, int],
                tags: Optional[List[str]] = None,
                type_: Optional[str] = None,
                interval: Optional[int] = None) -> Dict[str, Any]
```

Sends a single datapoint metric to DataDog

**Arguments**:

- `metric_name`: The name of the metric
- `datapoint`: A single integer or float related to the metric
- `tags`: A list of tags associated with the metric
- `type_`: Type of your metric: gauge, rate, or count
- `interval`: If the type of the metric is rate or count, define the corresponding interval

<a id="hooks.datadog.DatadogHook.query_metric"></a>

#### query\_metric

```python
def query_metric(query: str, from_seconds_ago: int,
                 to_seconds_ago: int) -> Dict[str, Any]
```

Queries datadog for a specific metric, potentially with some

function applied to it and returns the results.

**Arguments**:

- `query`: The datadog query to execute (see datadog docs)
- `from_seconds_ago`: How many seconds ago to start querying for.
- `to_seconds_ago`: Up to how many seconds ago to query for.

<a id="hooks.datadog.DatadogHook.post_event"></a>

#### post\_event

```python
def post_event(title: str,
               text: str,
               aggregation_key: Optional[str] = None,
               alert_type: Optional[str] = None,
               date_happened: Optional[int] = None,
               handle: Optional[str] = None,
               priority: Optional[str] = None,
               related_event_id: Optional[int] = None,
               tags: Optional[List[str]] = None,
               device_name: Optional[List[str]] = None) -> Dict[str, Any]
```

Posts an event to datadog (processing finished, potentially alerts, other issues)

Think about this as a means to maintain persistence of alerts, rather than
alerting itself.

**Arguments**:

- `title`: The title of the event
- `text`: The body of the event (more information)
- `aggregation_key`: Key that can be used to aggregate this event in a stream
- `alert_type`: The alert type for the event, one of
["error", "warning", "info", "success"]
- `date_happened`: POSIX timestamp of the event; defaults to now
- `handle`: str
- `priority`: Priority to post the event as. ("normal" or "low", defaults to "normal")
- `related_event_id`: Post event as a child of the given event
- `tags`: List of tags to apply to the event
- `device_name`: device_name to post the event with

