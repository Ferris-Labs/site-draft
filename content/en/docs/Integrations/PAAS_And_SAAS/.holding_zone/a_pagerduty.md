---
title: "pagerduty"
linkTitle: "pagerduty"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     pagerduty Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="hooks"></a>

# hooks

<a id="hooks.pagerduty_events"></a>

# hooks.pagerduty\_events

Hook for sending or receiving data from PagerDuty as well as creating PagerDuty incidents.

<a id="hooks.pagerduty_events.PagerdutyEventsHook"></a>

## PagerdutyEventsHook Objects

```python
class PagerdutyEventsHook(BaseHook)
```

This class can be used to interact with the Pagerduty Events API.

It takes both an Events API token and a PagerDuty connection with the Events API token
 (i.e. Integration key) as the password/Pagerduty API token. If both supplied, the token will be used.

**Arguments**:

- `integration_key`: PagerDuty Events API token
- `pagerduty_conn_id`: connection that has PagerDuty integration key in the Pagerduty API token field

<a id="hooks.pagerduty_events.PagerdutyEventsHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.pagerduty_events.PagerdutyEventsHook.create_event"></a>

#### create\_event

```python
def create_event(summary: str,
                 severity: str,
                 source: str = 'airflow',
                 action: str = 'trigger',
                 dedup_key: Optional[str] = None,
                 custom_details: Optional[Any] = None,
                 group: Optional[str] = None,
                 component: Optional[str] = None,
                 class_type: Optional[str] = None,
                 images: Optional[List[Any]] = None,
                 links: Optional[List[Any]] = None) -> Dict
```

Create event for service integration.

**Arguments**:

- `summary`: Summary for the event
- `severity`: Severity for the event, needs to be one of: info, warning, error, critical
- `source`: Specific human-readable unique identifier, such as a
hostname, for the system having the problem.
- `action`: Event action, needs to be one of: trigger, acknowledge,
resolve. Default to trigger if not specified.
- `dedup_key`: A string which identifies the alert triggered for the given event.
Required for the actions acknowledge and resolve.
- `custom_details`: Free-form details from the event. Can be a dictionary or a string.
If a dictionary is passed it will show up in PagerDuty as a table.
- `group`: A cluster or grouping of sources. For example, sources
“prod-datapipe-02” and “prod-datapipe-03” might both be part of “prod-datapipe”
- `component`: The part or component of the affected system that is broken.
- `class_type`: The class/type of the event.
- `images`: List of images to include. Each dictionary in the list accepts the following keys:
`src`: The source (URL) of the image being attached to the incident. This image must be served via
HTTPS.
`href`: [Optional] URL to make the image a clickable link.
`alt`: [Optional] Alternative text for the image.
- `links`: List of links to include. Each dictionary in the list accepts the following keys:
`href`: URL of the link to be attached.
`text`: [Optional] Plain text that describes the purpose of the link, and can be used as the
link's text.

**Returns**:

`dict`: PagerDuty Events API v2 response.

<a id="hooks.pagerduty"></a>

# hooks.pagerduty

Hook for sending or receiving data from PagerDuty as well as creating PagerDuty incidents.

<a id="hooks.pagerduty.PagerdutyHook"></a>

## PagerdutyHook Objects

```python
class PagerdutyHook(BaseHook)
```

The PagerdutyHook can be used to interact with both the PagerDuty API and the PagerDuty Events API.

Takes both PagerDuty API token directly and connection that has PagerDuty API token.
If both supplied, PagerDuty API token will be used.
In these cases, the PagerDuty API token refers to an account token:
https://support.pagerduty.com/docs/generating-api-keys#generating-a-general-access-rest-api-key
https://support.pagerduty.com/docs/generating-api-keys#generating-a-personal-rest-api-key

In order to send events (with the Pagerduty Events API), you will also need to specify the
routing_key (or Integration key) in the ``extra`` field

**Arguments**:

- `token`: PagerDuty API token
- `pagerduty_conn_id`: connection that has PagerDuty API token in the password field

<a id="hooks.pagerduty.PagerdutyHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.pagerduty.PagerdutyHook.get_session"></a>

#### get\_session

```python
def get_session() -> pdpyras.APISession
```

Returns `pdpyras.APISession` for use with sending or receiving data through the PagerDuty REST API.

The `pdpyras` library supplies a class `pdpyras.APISession` extending `requests.Session` from the
Requests HTTP library.

Documentation on how to use the `APISession` class can be found at:
https://pagerduty.github.io/pdpyras/`data`-access-abstraction

<a id="hooks.pagerduty.PagerdutyHook.create_event"></a>

#### create\_event

```python
def create_event(summary: str,
                 severity: str,
                 source: str = "airflow",
                 action: str = "trigger",
                 routing_key: Optional[str] = None,
                 dedup_key: Optional[str] = None,
                 custom_details: Optional[Any] = None,
                 group: Optional[str] = None,
                 component: Optional[str] = None,
                 class_type: Optional[str] = None,
                 images: Optional[List[Any]] = None,
                 links: Optional[List[Any]] = None) -> Dict
```

Create event for service integration.

**Arguments**:

- `summary`: Summary for the event
- `severity`: Severity for the event, needs to be one of: info, warning, error, critical
- `source`: Specific human-readable unique identifier, such as a
hostname, for the system having the problem.
- `action`: Event action, needs to be one of: trigger, acknowledge,
resolve. Default to trigger if not specified.
- `routing_key`: Integration key. If not specified, will try to read
from connection's extra json blob.
- `dedup_key`: A string which identifies the alert triggered for the given event.
Required for the actions acknowledge and resolve.
- `custom_details`: Free-form details from the event. Can be a dictionary or a string.
If a dictionary is passed it will show up in PagerDuty as a table.
- `group`: A cluster or grouping of sources. For example, sources
“prod-datapipe-02” and “prod-datapipe-03” might both be part of “prod-datapipe”
- `component`: The part or component of the affected system that is broken.
- `class_type`: The class/type of the event.
- `images`: List of images to include. Each dictionary in the list accepts the following keys:
`src`: The source (URL) of the image being attached to the incident. This image must be served via
HTTPS.
`href`: [Optional] URL to make the image a clickable link.
`alt`: [Optional] Alternative text for the image.
- `links`: List of links to include. Each dictionary in the list accepts the following keys:
`href`: URL of the link to be attached.
`text`: [Optional] Plain text that describes the purpose of the link, and can be used as the
link's text.

**Returns**:

`dict`: PagerDuty Events API v2 response.

