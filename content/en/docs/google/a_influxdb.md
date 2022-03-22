---
title: "influxdb"
linkTitle: "influxdb"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     influxdb Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.influxdb"></a>

# operators.influxdb

<a id="operators.influxdb.InfluxDBOperator"></a>

## InfluxDBOperator Objects

```python
class InfluxDBOperator(BaseOperator)
```

Executes sql code in a specific InfluxDB database

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:InfluxDBOperator`

**Arguments**:

- `sql`: the sql code to be executed. Can receive a str representing a
sql statement
- `influxdb_conn_id`: Reference to :ref:`Influxdb connection id <howto/connection:influxdb>`.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_influxdb_query"></a>

# example\_dags.example\_influxdb\_query

<a id="example_dags.example_influxdb"></a>

# example\_dags.example\_influxdb

<a id="hooks"></a>

# hooks

<a id="hooks.influxdb"></a>

# hooks.influxdb

This module allows to connect to a InfluxDB database.

.. spelling::

    FluxTable

<a id="hooks.influxdb.InfluxDBHook"></a>

## InfluxDBHook Objects

```python
class InfluxDBHook(BaseHook)
```

Interact with InfluxDB.

Performs a connection to InfluxDB and retrieves client.

**Arguments**:

- `influxdb_conn_id`: Reference to :ref:`Influxdb connection id <howto/connection:influxdb>`.

<a id="hooks.influxdb.InfluxDBHook.get_uri"></a>

#### get\_uri

```python
def get_uri(conn: Connection)
```

Function to add additional parameters to the URI
based on SSL or other InfluxDB host requirements

<a id="hooks.influxdb.InfluxDBHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> InfluxDBClient
```

Function that initiates a new InfluxDB connection
with token and organization name

<a id="hooks.influxdb.InfluxDBHook.query"></a>

#### query

```python
def query(query) -> List[FluxTable]
```

Function to to run the query.

Note: The bucket name
should be included in the query

**Arguments**:

- `query`: InfluxDB query

**Returns**:

List

<a id="hooks.influxdb.InfluxDBHook.query_to_df"></a>

#### query\_to\_df

```python
def query_to_df(query) -> pd.DataFrame
```

Function to run the query and

return a pandas dataframe
Note: The bucket name
should be included in the query

**Arguments**:

- `query`: InfluxDB query

**Returns**:

pd.DataFrame

<a id="hooks.influxdb.InfluxDBHook.write"></a>

#### write

```python
def write(bucket_name,
          point_name,
          tag_name,
          tag_value,
          field_name,
          field_value,
          synchronous=False)
```

Writes a Point to the bucket specified.
Example: Point("my_measurement").tag("location", "Prague").field("temperature", 25.3)

<a id="hooks.influxdb.InfluxDBHook.create_organization"></a>

#### create\_organization

```python
def create_organization(name)
```

Function to create a new organization

<a id="hooks.influxdb.InfluxDBHook.delete_organization"></a>

#### delete\_organization

```python
def delete_organization(org_id)
```

Function to delete organization by organization id

<a id="hooks.influxdb.InfluxDBHook.create_bucket"></a>

#### create\_bucket

```python
def create_bucket(bucket_name, description, org_id, retention_rules=None)
```

Function to create a bucket for an organization

<a id="hooks.influxdb.InfluxDBHook.find_bucket_id_by_name"></a>

#### find\_bucket\_id\_by\_name

```python
def find_bucket_id_by_name(bucket_name)
```

Function to get bucket id by name.

<a id="hooks.influxdb.InfluxDBHook.delete_bucket"></a>

#### delete\_bucket

```python
def delete_bucket(bucket_name)
```

Function to delete bucket by bucket name.

