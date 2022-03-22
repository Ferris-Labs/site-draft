---
title: "sqlite"
linkTitle: "sqlite"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     sqlite Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.sqlite"></a>

# operators.sqlite

<a id="operators.sqlite.SqliteOperator"></a>

## SqliteOperator Objects

```python
class SqliteOperator(BaseOperator)
```

Executes sql code in a specific Sqlite database

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SqliteOperator`

**Arguments**:

- `sql`: the sql code to be executed. Can receive a str representing a
sql statement, a list of str (sql statements), or reference to a template file.
Template reference are recognized by str ending in '.sql'
(templated)
- `sqlite_conn_id`: reference to a specific sqlite database
- `parameters`: (optional) the parameters to render the SQL query with.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_sqlite"></a>

# example\_dags.example\_sqlite

This is an example DAG for the use of the SqliteOperator.
In this example, we create two tasks that execute in sequence.
The first task calls an sql command, defined in the SQLite operator,
which when triggered, is performed on the connected sqlite database.
The second task is similar but instead calls the SQL command from an external file.

<a id="hooks"></a>

# hooks

<a id="hooks.sqlite"></a>

# hooks.sqlite

<a id="hooks.sqlite.SqliteHook"></a>

## SqliteHook Objects

```python
class SqliteHook(DbApiHook)
```

Interact with SQLite.

<a id="hooks.sqlite.SqliteHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> sqlite3.dbapi2.Connection
```

Returns a sqlite connection object

