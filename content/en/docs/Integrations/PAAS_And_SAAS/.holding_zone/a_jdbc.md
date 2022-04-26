---
title: "jdbc"
linkTitle: "jdbc"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     jdbc Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.jdbc"></a>

# operators.jdbc

<a id="operators.jdbc.JdbcOperator"></a>

## JdbcOperator Objects

```python
class JdbcOperator(BaseOperator)
```

Executes sql code in a database using jdbc driver.

Requires jaydebeapi.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:JdbcOperator`

**Arguments**:

- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
Template references are recognized by str ending in '.sql'
- `jdbc_conn_id`: reference to a predefined database
- `autocommit`: if True, each command is automatically committed.
(default value: False)
- `parameters`: (optional) the parameters to render the SQL query with.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_jdbc_queries"></a>

# example\_dags.example\_jdbc\_queries

Example DAG demonstrating the usage of the JdbcOperator.

<a id="hooks"></a>

# hooks

<a id="hooks.jdbc"></a>

# hooks.jdbc

<a id="hooks.jdbc.JdbcHook"></a>

## JdbcHook Objects

```python
class JdbcHook(DbApiHook)
```

General hook for jdbc db access.

JDBC URL, username and password will be taken from the predefined connection.
Note that the whole JDBC URL must be specified in the "host" field in the DB.
Raises an airflow error if the given connection id doesn't exist.

<a id="hooks.jdbc.JdbcHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="hooks.jdbc.JdbcHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.jdbc.JdbcHook.set_autocommit"></a>

#### set\_autocommit

```python
def set_autocommit(conn: jaydebeapi.Connection, autocommit: bool) -> None
```

Enable or disable autocommit for the given connection.

**Arguments**:

- `conn`: The connection.
- `autocommit`: The connection's autocommit setting.

<a id="hooks.jdbc.JdbcHook.get_autocommit"></a>

#### get\_autocommit

```python
def get_autocommit(conn: jaydebeapi.Connection) -> bool
```

Get autocommit setting for the provided connection.

Return True if conn.autocommit is set to True.
Return False if conn.autocommit is not set or set to False

**Arguments**:

- `conn`: The connection.

**Returns**:

`bool`: connection autocommit setting.

