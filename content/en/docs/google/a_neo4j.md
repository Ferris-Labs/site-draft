---
title: "neo4j"
linkTitle: "neo4j"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     neo4j Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.neo4j"></a>

# operators.neo4j

<a id="operators.neo4j.Neo4jOperator"></a>

## Neo4jOperator Objects

```python
class Neo4jOperator(BaseOperator)
```

Executes sql code in a specific Neo4j database

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:Neo4jOperator`

**Arguments**:

- `sql`: the sql code to be executed. Can receive a str representing a
sql statement
- `neo4j_conn_id`: Reference to :ref:`Neo4j connection id <howto/connection:neo4j>`.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_neo4j"></a>

# example\_dags.example\_neo4j

Example use of Neo4j related operators.

<a id="hooks"></a>

# hooks

<a id="hooks.neo4j"></a>

# hooks.neo4j

This module allows to connect to a Neo4j database.

<a id="hooks.neo4j.Neo4jHook"></a>

## Neo4jHook Objects

```python
class Neo4jHook(BaseHook)
```

Interact with Neo4j.

Performs a connection to Neo4j and runs the query.

**Arguments**:

- `neo4j_conn_id`: Reference to :ref:`Neo4j connection id <howto/connection:neo4j>`.

<a id="hooks.neo4j.Neo4jHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Neo4jDriver
```

Function that initiates a new Neo4j connection
with username, password and database schema.

<a id="hooks.neo4j.Neo4jHook.get_uri"></a>

#### get\_uri

```python
def get_uri(conn: Connection) -> str
```

Build the uri based on extras

- Default - uses bolt scheme(bolt://)
- neo4j_scheme - neo4j://
- certs_self_signed - neo4j+ssc://
- certs_trusted_ca - neo4j+s://

**Arguments**:

- `conn`: connection object.

**Returns**:

uri

<a id="hooks.neo4j.Neo4jHook.run"></a>

#### run

```python
def run(query) -> Result
```

Function to create a neo4j session

and execute the query in the session.

**Arguments**:

- `query`: Neo4j query

**Returns**:

Result

