---
title: "trino"
linkTitle: "trino"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     trino Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="transfers"></a>

# transfers

<a id="transfers.gcs_to_trino"></a>

# transfers.gcs\_to\_trino

This module contains Google Cloud Storage to Trino operator.

<a id="transfers.gcs_to_trino.GCSToTrinoOperator"></a>

## GCSToTrinoOperator Objects

```python
class GCSToTrinoOperator(BaseOperator)
```

Loads a csv file from Google Cloud Storage into a Trino table.

Assumptions:
1. CSV file should not have headers
2. Trino table with requisite columns is already created
3. Optionally, a separate JSON file with headers can be provided

**Arguments**:

- `source_bucket`: Source GCS bucket that contains the csv
- `source_object`: csv file including the path
- `trino_table`: trino table to upload the data
- `trino_conn_id`: destination trino connection
- `gcp_conn_id`: (Optional) The connection ID used to connect to Google Cloud and
interact with the Google Cloud Storage service.
- `schema_fields`: The names of the columns to fill in the table. If schema_fields is
provided, any path provided in the schema object will be
- `schema_object`: JSON file with schema fields
- `delegate_to`: The account to impersonate using domain-wide delegation of authority,
if any. For this to work, the service account making the request must have
domain-wide delegation enabled.
- `impersonation_chain`: Optional service account to impersonate using short-term
credentials, or chained list of accounts required to get the access_token
of the last account in the list, which will be impersonated in the request.
If set as a string, the account must grant the originating account
the Service Account Token Creator IAM role.
If set as a sequence, the identities from the list must grant
Service Account Token Creator IAM role to the directly preceding identity, with first
account from the list granting this role to the originating account.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_gcs_to_trino"></a>

# example\_dags.example\_gcs\_to\_trino

Example DAG using GCSToTrinoOperator.

<a id="hooks"></a>

# hooks

<a id="hooks.trino"></a>

# hooks.trino

<a id="hooks.trino.TrinoException"></a>

## TrinoException Objects

```python
class TrinoException(Exception)
```

Trino exception

<a id="hooks.trino.TrinoHook"></a>

## TrinoHook Objects

```python
class TrinoHook(DbApiHook)
```

Interact with Trino through trino package.

>>> ph = TrinoHook()
>>> sql = "SELECT count(1) AS num FROM airflow.static_babynames"
>>> ph.get_records(sql)
[[340698]]

<a id="hooks.trino.TrinoHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Connection
```

Returns a connection object

<a id="hooks.trino.TrinoHook.get_isolation_level"></a>

#### get\_isolation\_level

```python
def get_isolation_level() -> Any
```

Returns an isolation level

<a id="hooks.trino.TrinoHook.get_records"></a>

#### get\_records

```python
@overload
def get_records(sql: str = "", parameters: Optional[dict] = None)
```

Get a set of records from Trino

**Arguments**:

- `sql`: SQL statement to be executed.
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.trino.TrinoHook.get_records"></a>

#### get\_records

```python
@overload
def get_records(sql: str = "",
                parameters: Optional[dict] = None,
                hql: str = "")
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.get_records"></a>

#### get\_records

```python
def get_records(sql: str = "",
                parameters: Optional[dict] = None,
                hql: str = "")
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.get_first"></a>

#### get\_first

```python
@overload
def get_first(sql: str = "", parameters: Optional[dict] = None) -> Any
```

Returns only the first row, regardless of how many rows the query returns.

**Arguments**:

- `sql`: SQL statement to be executed.
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.trino.TrinoHook.get_first"></a>

#### get\_first

```python
@overload
def get_first(sql: str = "",
              parameters: Optional[dict] = None,
              hql: str = "") -> Any
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.get_first"></a>

#### get\_first

```python
def get_first(sql: str = "",
              parameters: Optional[dict] = None,
              hql: str = "") -> Any
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.get_pandas_df"></a>

#### get\_pandas\_df

```python
@overload
def get_pandas_df(sql: str = "", parameters: Optional[dict] = None, **kwargs)
```

Get a pandas dataframe from a sql query.

**Arguments**:

- `sql`: SQL statement to be executed.
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.trino.TrinoHook.get_pandas_df"></a>

#### get\_pandas\_df

```python
@overload
def get_pandas_df(sql: str = "",
                  parameters: Optional[dict] = None,
                  hql: str = "",
                  **kwargs)
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.get_pandas_df"></a>

#### get\_pandas\_df

```python
def get_pandas_df(sql: str = "",
                  parameters: Optional[dict] = None,
                  hql: str = "",
                  **kwargs)
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.run"></a>

#### run

```python
@overload
def run(sql: str = "",
        autocommit: bool = False,
        parameters: Optional[dict] = None,
        handler: Optional[Callable] = None) -> None
```

Execute the statement against Trino. Can be used to create views.

<a id="hooks.trino.TrinoHook.run"></a>

#### run

```python
@overload
def run(sql: str = "",
        autocommit: bool = False,
        parameters: Optional[dict] = None,
        handler: Optional[Callable] = None,
        hql: str = "") -> None
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.run"></a>

#### run

```python
def run(sql: str = "",
        autocommit: bool = False,
        parameters: Optional[dict] = None,
        handler: Optional[Callable] = None,
        hql: str = "") -> None
```

:sphinx-autoapi-skip:

<a id="hooks.trino.TrinoHook.insert_rows"></a>

#### insert\_rows

