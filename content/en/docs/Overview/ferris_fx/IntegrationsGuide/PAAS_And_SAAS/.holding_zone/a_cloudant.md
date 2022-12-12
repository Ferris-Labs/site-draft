---
title: "cloudant"
linkTitle: "cloudant"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     cloudant Plugin.
---

---
title: "IBM Cloudant"
linkTitle: "CLoudant"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     Cloudant Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="hooks"></a>

# hooks

<a id="hooks.cloudant"></a>

# hooks.cloudant

Hook for Cloudant

<a id="hooks.cloudant.CloudantHook"></a>

## CloudantHook Objects

```python
class CloudantHook(BaseHook)
```

Interact with Cloudant. This class is a thin wrapper around the cloudant python library.

.. seealso:: the latest documentation `here <https://python-cloudant.readthedocs.io/en/latest/>`_.

**Arguments**:

- `cloudant_conn_id`: The connection id to authenticate and get a session object from cloudant.

<a id="hooks.cloudant.CloudantHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.cloudant.CloudantHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> cloudant
```

Opens a connection to the cloudant service and closes it automatically if used as context manager.

.. note::
    In the connection form:
    - 'host' equals the 'Account' (optional)
    - 'login' equals the 'Username (or API Key)' (required)
    - 'password' equals the 'Password' (required)

**Returns**:

`cloudant`: an authorized cloudant session context manager object.

