---
title: "dingding"
linkTitle: "dingding"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     dingding Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.dingding"></a>

# operators.dingding

<a id="operators.dingding.DingdingOperator"></a>

## DingdingOperator Objects

```python
class DingdingOperator(BaseOperator)
```

This operator allows you send Dingding message using Dingding custom bot.

Get Dingding token from conn_id.password. And prefer set domain to
conn_id.host, if not will use default ``https://oapi.dingtalk.com``.

For more detail message in
`Dingding custom bot <https://open-doc.dingtalk.com/microapp/serverapi2/qf2nxq>`_

**Arguments**:

- `dingding_conn_id`: The name of the Dingding connection to use
- `message_type`: Message type you want to send to Dingding, support five type so far
including text, link, markdown, actionCard, feedCard
- `message`: The message send to Dingding chat group
- `at_mobiles`: Remind specific users with this message
- `at_all`: Remind all people in group or not. If True, will overwrite ``at_mobiles``

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_dingding"></a>

# example\_dags.example\_dingding

This is an example dag for using the DingdingOperator.

<a id="example_dags.example_dingding.failure_callback"></a>

#### failure\_callback

```python
def failure_callback(context)
```

The function that will be executed on failure.

**Arguments**:

- `context`: The context of the executed task.

<a id="hooks"></a>

# hooks

<a id="hooks.dingding"></a>

# hooks.dingding

<a id="hooks.dingding.DingdingHook"></a>

## DingdingHook Objects

```python
class DingdingHook(HttpHook)
```

This hook allows you send Dingding message using Dingding custom bot.

Get Dingding token from conn_id.password. And prefer set domain to
conn_id.host, if not will use default ``https://oapi.dingtalk.com``.

For more detail message in
`Dingding custom bot <https://open-doc.dingtalk.com/microapp/serverapi2/qf2nxq>`_

**Arguments**:

- `dingding_conn_id`: The name of the Dingding connection to use
- `message_type`: Message type you want to send to Dingding, support five type so far
including text, link, markdown, actionCard, feedCard
- `message`: The message send to Dingding chat group
- `at_mobiles`: Remind specific users with this message
- `at_all`: Remind all people in group or not. If True, will overwrite ``at_mobiles``

<a id="hooks.dingding.DingdingHook.get_conn"></a>

#### get\_conn

```python
def get_conn(headers: Optional[dict] = None) -> Session
```

Overwrite HttpHook get_conn because just need base_url and headers and

not don't need generic params

**Arguments**:

- `headers`: additional headers to be passed through as a dictionary

<a id="hooks.dingding.DingdingHook.send"></a>

#### send

```python
def send() -> None
```

Send Dingding message

