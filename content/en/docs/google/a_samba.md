---
title: "samba"
linkTitle: "samba"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     samba Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="hooks"></a>

# hooks

<a id="hooks.samba"></a>

# hooks.samba

<a id="hooks.samba.SambaHook"></a>

## SambaHook Objects

```python
class SambaHook(BaseHook)
```

Allows for interaction with a Samba server.

The hook should be used as a context manager in order to correctly
set up a session and disconnect open connections upon exit.

**Arguments**:

- `samba_conn_id`: The connection id reference.
- `share`: An optional share name. If this is unset then the "schema" field of
the connection is used in its place.

<a id="hooks.samba.SambaHook.push_from_local"></a>

#### push\_from\_local

```python
def push_from_local(destination_filepath: str, local_filepath: str)
```

Push local file to samba server

