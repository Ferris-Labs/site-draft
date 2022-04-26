---
title: "presto"
linkTitle: "presto"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     presto Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="transfers"></a>

# transfers

<a id="transfers.gcs_to_presto"></a>

# transfers.gcs\_to\_presto

This module contains Google Cloud Storage to Presto operator.

<a id="transfers.gcs_to_presto.GCSToPrestoOperator"></a>

## GCSToPrestoOperator Objects

```python
class GCSToPrestoOperator(BaseOperator)
```

Loads a csv file from Google Cloud Storage into a Presto table.

Assumptions:
1. CSV file should not have headers
2. Presto table with requisite columns is already created
3. Optionally, a separate JSON file with headers or list of headers can be provided

**Arguments**:

- `source_bucket`: Source GCS bucket that contains the csv
- `source_object`: csv file including the path
- `presto_table`: presto table to upload the data
- `presto_conn_id`: destination presto connection
- `gcp_conn_id`: (Optional) The connection ID used to connect to Google Cloud and
interact with the Google Cloud Storage service.
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

<a id="example_dags.example_gcs_to_presto"></a>

# example\_dags.example\_gcs\_to\_presto

Example DAG using GCSToPrestoOperator.

<a id="hooks"></a>

# hooks

<a id="hooks.presto"></a>

# hooks.presto

<a id="hooks.presto.PrestoException"></a>

## PrestoException Objects

```python
class PrestoException(Exception)
```

Presto exception

<a id="hooks.presto.PrestoHook"></a>

## PrestoHook Objects

```python
class PrestoHook(DbApiHook)
```

Interact with Presto through prestodb.

>>> ph = PrestoHook()
>>> sql = "SELECT count(1) AS num FROM airflow.static_babynames"
>>> ph.get_records(sql)
[[340698]]

<a id="hooks.presto.PrestoHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Connection
```

Returns a connection object

<a id="hooks.presto.PrestoHook.get_isolation_level"></a>

#### get\_isolation\_level

```python
def get_isolation_level() -> Any
```

Returns an isolation level

<a id="hooks.presto.PrestoHook.get_records"></a>

#### get\_records

```python
@overload
def get_records(sql: str = "", parameters: Optional[dict] = None)
```

Get a set of records from Presto

**Arguments**:

- `sql`: SQL statement to be executed.
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.presto.PrestoHook.get_records"></a>

#### get\_records

```python
@overload
def get_records(sql: str = "",
                parameters: Optional[dict] = None,
                hql: str = "")
```

:sphinx-autoapi-skip:

<a id="hooks.presto.PrestoHook.get_records"></a>

#### get\_records

```python
def get_records(sql: str = "",
                parameters: Optional[dict] = None,
                hql: str = "")
```

:sphinx-autoapi-skip:

<a id="hooks.presto.PrestoHook.get_first"></a>

#### get\_first

```python
@overload
def get_first(sql: str = "", parameters: Optional[dict] = None) -> Any
```

Returns only the first row, regardless of how many rows the query returns.

**Arguments**:

- `sql`: SQL statement to be executed.
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.presto.PrestoHook.get_first"></a>

#### get\_first

```python
@overload
def get_first(sql: str = "",
              parameters: Optional[dict] = None,
              hql: str = "") -> Any
```

:sphinx-autoapi-skip:

<a id="hooks.presto.PrestoHook.get_first"></a>

#### get\_first

```python
def get_first(sql: str = "",
              parameters: Optional[dict] = None,
              hql: str = "") -> Any
```

:sphinx-autoapi-skip:

<a id="hooks.presto.PrestoHook.get_pandas_df"></a>

#### get\_pandas\_df

```python
@overload
def get_pandas_df(sql: str = "", parameters=None, **kwargs)
```

Get a pandas dataframe from a sql query.

**Arguments**:

- `sql`: SQL statement to be executed.
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.presto.PrestoHook.get_pandas_df"></a>

#### get\_pandas\_df

```python
@overload
def get_pandas_df(sql: str = "", parameters=None, hql: str = "", **kwargs)
```

:sphinx-autoapi-skip:

<a id="hooks.presto.PrestoHook.get_pandas_df"></a>

#### get\_pandas\_df

```python
def get_pandas_df(sql: str = "", parameters=None, hql: str = "", **kwargs)
```

:sphinx-autoapi-skip:

<a id="hooks.presto.PrestoHook.run"></a>

#### run

```python
@overload
def run(sql: str = "",
        autocommit: bool = False,
        parameters: Optional[dict] = None,
        handler: Optional[Callable] = None) -> None
```

Execute the statement against Presto. Can be used to create views.

<a id="hooks.presto.PrestoHook.run"></a>

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

<a id="hooks.presto.PrestoHook.run"></a>

#### run

```python
def run(sql: str = "",
        autocommit: bool = False,
        parameters: Optional[dict] = None,
        handler: Optional[Callable] = None,
        hql: str = "") -> None
```

:sphinx-autoapi-skip:

<a id="hooks.presto.PrestoHook.insert_rows"></a>

#### insert\_rows

