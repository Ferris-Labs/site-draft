---
title: "vertica"
linkTitle: "vertica"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     vertica Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.vertica"></a>

# operators.vertica

<a id="operators.vertica.VerticaOperator"></a>

## VerticaOperator Objects

```python
class VerticaOperator(BaseOperator)
```

Executes sql code in a specific Vertica database.

**Arguments**:

- `vertica_conn_id`: reference to a specific Vertica database
- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
Template references are recognized by str ending in '.sql'

<a id="hooks"></a>

# hooks

<a id="hooks.vertica"></a>

# hooks.vertica

<a id="hooks.vertica.VerticaHook"></a>

## VerticaHook Objects

```python
class VerticaHook(DbApiHook)
```

Interact with Vertica.

<a id="hooks.vertica.VerticaHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> connect
```

Return verticaql connection object

