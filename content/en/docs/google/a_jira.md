---
title: "jira"
linkTitle: "jira"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     jira Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.jira"></a>

# sensors.jira

<a id="sensors.jira.JiraSensor"></a>

## JiraSensor Objects

```python
class JiraSensor(BaseSensorOperator)
```

Monitors a jira ticket for any change.

**Arguments**:

- `jira_conn_id`: reference to a pre-defined Jira Connection
- `method_name`: method name from jira-python-sdk to be execute
- `method_params`: parameters for the method method_name
- `result_processor`: function that return boolean and act as a sensor response

<a id="sensors.jira.JiraTicketSensor"></a>

## JiraTicketSensor Objects

```python
class JiraTicketSensor(JiraSensor)
```

Monitors a jira ticket for given change in terms of function.

**Arguments**:

- `jira_conn_id`: reference to a pre-defined Jira Connection
- `ticket_id`: id of the ticket to be monitored
- `field`: field of the ticket to be monitored
- `expected_value`: expected value of the field
- `result_processor`: function that return boolean and act as a sensor response

<a id="sensors.jira.JiraTicketSensor.issue_field_checker"></a>

#### issue\_field\_checker

```python
def issue_field_checker(issue: Issue) -> Optional[bool]
```

Check issue using different conditions to prepare to evaluate sensor.

<a id="operators"></a>

# operators

<a id="operators.jira"></a>

# operators.jira

<a id="operators.jira.JiraOperator"></a>

## JiraOperator Objects

```python
class JiraOperator(BaseOperator)
```

JiraOperator to interact and perform action on Jira issue tracking system.

This operator is designed to use Jira Python SDK: http://jira.readthedocs.io

**Arguments**:

- `jira_conn_id`: reference to a pre-defined Jira Connection
- `jira_method`: method name from Jira Python SDK to be called
- `jira_method_args`: required method parameters for the jira_method. (templated)
- `result_processor`: function to further process the response from Jira
- `get_jira_resource_method`: function or operator to get jira resource
on which the provided jira_method will be executed

<a id="hooks"></a>

# hooks

<a id="hooks.jira"></a>

# hooks.jira

Hook for JIRA

<a id="hooks.jira.JiraHook"></a>

## JiraHook Objects

```python
class JiraHook(BaseHook)
```

Jira interaction hook, a Wrapper around JIRA Python SDK.

**Arguments**:

- `jira_conn_id`: reference to a pre-defined Jira Connection

