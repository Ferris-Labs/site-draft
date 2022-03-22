---
title: "opsgenie"
linkTitle: "opsgenie"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     opsgenie Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.opsgenie_alert"></a>

# operators.opsgenie\_alert

This module is deprecated. Please use :mod:`airflow.providers.opsgenie.operators.opsgenie`.

<a id="operators.opsgenie_alert.OpsgenieAlertOperator"></a>

## OpsgenieAlertOperator Objects

```python
class OpsgenieAlertOperator(OpsgenieCreateAlertOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.opsgenie.operators.opsgenie.OpsgenieCreateAlertOperator`.

<a id="operators.opsgenie"></a>

# operators.opsgenie

<a id="operators.opsgenie.OpsgenieCreateAlertOperator"></a>

## OpsgenieCreateAlertOperator Objects

```python
class OpsgenieCreateAlertOperator(BaseOperator)
```

This operator allows you to post alerts to Opsgenie.

Accepts a connection that has an Opsgenie API key as the connection's password.
This operator sets the domain to conn_id.host, and if not set will default
to ``https://api.opsgenie.com``.

Each Opsgenie API key can be pre-configured to a team integration.
You can override these defaults in this operator.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:OpsgenieCreateAlertOperator`

**Arguments**:

- `opsgenie_conn_id`: The name of the Opsgenie connection to use
- `message`: The Message of the Opsgenie alert (templated)
- `alias`: Client-defined identifier of the alert (templated)
- `description`: Description field of the alert (templated)
- `responders`: Teams, users, escalations and schedules that
the alert will be routed to send notifications.
- `visible_to`: Teams and users that the alert will become visible
to without sending any notification.
- `actions`: Custom actions that will be available for the alert.
- `tags`: Tags of the alert.
- `details`: Map of key-value pairs to use as custom properties of the alert.
- `entity`: Entity field of the alert that is
generally used to specify which domain alert is related to. (templated)
- `source`: Source field of the alert. Default value is
IP address of the incoming request.
- `priority`: Priority level of the alert. Default value is P3. (templated)
- `user`: Display name of the request owner.
- `note`: Additional note that will be added while creating the alert. (templated)

<a id="operators.opsgenie.OpsgenieCreateAlertOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Call the OpsgenieAlertHook to post message

<a id="operators.opsgenie.OpsgenieCloseAlertOperator"></a>

## OpsgenieCloseAlertOperator Objects

```python
class OpsgenieCloseAlertOperator(BaseOperator)
```

This operator allows you to close alerts to Opsgenie.

Accepts a connection that has an Opsgenie API key as the connection's password.
This operator sets the domain to conn_id.host, and if not set will default
to ``https://api.opsgenie.com``.

Each Opsgenie API key can be pre-configured to a team integration.
You can override these defaults in this operator.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:OpsgenieCloseAlertOperator`

**Arguments**:

- `opsgenie_conn_id`: The name of the Opsgenie connection to use
- `identifier`: Identifier of alert which could be alert id, tiny id or alert alias
- `identifier_type`: Type of the identifier that is provided as an in-line parameter.
Possible values are 'id', 'alias' or 'tiny'
- `user`: display name of the request owner
- `note`: additional note that will be added while creating the alert
- `source`: source field of the alert. Default value is IP address of the incoming request
- `close_alert_kwargs`: additional params to pass

<a id="operators.opsgenie.OpsgenieCloseAlertOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Call the OpsgenieAlertHook to close alert

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_opsgenie_alert"></a>

# example\_dags.example\_opsgenie\_alert

<a id="hooks"></a>

# hooks

<a id="hooks.opsgenie_alert"></a>

# hooks.opsgenie\_alert

This module is deprecated. Please use :mod:`airflow.providers.opsgenie.hooks.opsgenie`.

<a id="hooks.opsgenie"></a>

# hooks.opsgenie

<a id="hooks.opsgenie.OpsgenieAlertHook"></a>

## OpsgenieAlertHook Objects

```python
class OpsgenieAlertHook(BaseHook)
```

This hook allows you to post alerts to Opsgenie.

Accepts a connection that has an Opsgenie API key as the connection's password.
This hook sets the domain to conn_id.host, and if not set will default
to ``https://api.opsgenie.com``.

Each Opsgenie API key can be pre-configured to a team integration.
You can override these defaults in this hook.

**Arguments**:

- `opsgenie_conn_id`: The name of the Opsgenie connection to use

<a id="hooks.opsgenie.OpsgenieAlertHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> AlertApi
```

Get the underlying AlertApi client

**Returns**:

`opsgenie_sdk.AlertApi`: AlertApi client

<a id="hooks.opsgenie.OpsgenieAlertHook.create_alert"></a>

#### create\_alert

```python
def create_alert(payload: Optional[dict] = None) -> SuccessResponse
```

Create an alert on Opsgenie

**Arguments**:

- `payload`: Opsgenie API Create Alert payload values
See https://docs.opsgenie.com/docs/alert-api#section-create-alert

**Returns**:

`opsgenie_sdk.SuccessResponse`: api response

<a id="hooks.opsgenie.OpsgenieAlertHook.close_alert"></a>

#### close\_alert

```python
def close_alert(identifier: str,
                identifier_type: Optional[str] = 'id',
                payload: Optional[dict] = None,
                kwargs: Optional[dict] = None) -> SuccessResponse
```

Close an alert in Opsgenie

**Arguments**:

- `identifier`: Identifier of alert which could be alert id, tiny id or alert alias
- `identifier_type`: Type of the identifier that is provided as an in-line parameter.
Possible values are 'id', 'alias' or 'tiny'
- `payload`: Request payload of closing alert action.
see https://github.com/opsgenie/opsgenie-python-sdk/blob/master/docs/AlertApi.md#close_alert
- `kwargs`: params to pass to the function

**Returns**:

`opsgenie_sdk.SuccessResponse`: SuccessResponse
If the method is called asynchronously,
returns the request thread.

