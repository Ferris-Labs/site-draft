---
title: "salesforce"
linkTitle: "salesforce"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     salesforce Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.tableau_job_status"></a>

# sensors.tableau\_job\_status

<a id="operators"></a>

# operators

<a id="operators.tableau_refresh_workbook"></a>

# operators.tableau\_refresh\_workbook

<a id="operators.salesforce_apex_rest"></a>

# operators.salesforce\_apex\_rest

<a id="operators.salesforce_apex_rest.SalesforceApexRestOperator"></a>

## SalesforceApexRestOperator Objects

```python
class SalesforceApexRestOperator(BaseOperator)
```

Execute a APEX Rest API action

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SalesforceApexRestOperator`

**Arguments**:

- `endpoint`: The REST endpoint for the request.
- `method`: HTTP method for the request (default GET)
- `payload`: A dict of parameters to send in a POST / PUT request
- `salesforce_conn_id`: The :ref:`Salesforce Connection id <howto/connection:SalesforceHook>`.

<a id="operators.salesforce_apex_rest.SalesforceApexRestOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> dict
```

Makes an HTTP request to an APEX REST endpoint and pushes results to xcom.

**Arguments**:

- `context`: The task context during execution.

**Returns**:

`dict`: Apex response

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_salesforce_apex_rest"></a>

# example\_dags.example\_salesforce\_apex\_rest

<a id="hooks"></a>

# hooks

<a id="hooks.tableau"></a>

# hooks.tableau

<a id="hooks.salesforce"></a>

# hooks.salesforce

This module contains a Salesforce Hook which allows you to connect to your Salesforce instance,
retrieve data from it, and write that data to a file for other uses.

.. note:: this hook also relies on the simple_salesforce package:
      https://github.com/simple-salesforce/simple-salesforce

<a id="hooks.salesforce.SalesforceHook"></a>

## SalesforceHook Objects

```python
class SalesforceHook(BaseHook)
```

Creates new connection to Salesforce and allows you to pull data out of SFDC and save it to a file.

You can then use that file with other Airflow operators to move the data into another data source.

**Arguments**:

- `conn_id`: The name of the connection that has the parameters needed to connect to Salesforce.
The connection should be of type `Salesforce`.
- `session_id`: The access token for a given HTTP request session.
- `session`: A custom HTTP request session. This enables the use of requests Session features not
otherwise exposed by `simple_salesforce`.

.. note::
    A connection to Salesforce can be created via several authentication options:

    * Password: Provide Username, Password, and Security Token
    * Direct Session: Provide a `session_id` and either Instance or Instance URL
    * OAuth 2.0 JWT: Provide a Consumer Key and either a Private Key or Private Key File Path
    * IP Filtering: Provide Username, Password, and an Organization ID

    If in sandbox, enter a Domain value of 'test'.

<a id="hooks.salesforce.SalesforceHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="hooks.salesforce.SalesforceHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.salesforce.SalesforceHook.conn"></a>

#### conn

```python
@cached_property
def conn() -> api.Salesforce
```

Returns a Salesforce instance. (cached)

<a id="hooks.salesforce.SalesforceHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> api.Salesforce
```

Returns a Salesforce instance. (cached)

<a id="hooks.salesforce.SalesforceHook.make_query"></a>

#### make\_query

```python
def make_query(query: str,
               include_deleted: bool = False,
               query_params: Optional[dict] = None) -> dict
```

Make a query to Salesforce.

**Arguments**:

- `query`: The query to make to Salesforce.
- `include_deleted`: True if the query should include deleted records.
- `query_params`: Additional optional arguments

**Returns**:

`dict`: The query result.

<a id="hooks.salesforce.SalesforceHook.describe_object"></a>

#### describe\_object

```python
def describe_object(obj: str) -> dict
```

Get the description of an object from Salesforce.

This description is the object's schema and
some extra metadata that Salesforce stores for each object.

**Arguments**:

- `obj`: The name of the Salesforce object that we are getting a description of.

**Returns**:

`dict`: the description of the Salesforce object.

<a id="hooks.salesforce.SalesforceHook.get_available_fields"></a>

#### get\_available\_fields

```python
def get_available_fields(obj: str) -> List[str]
```

Get a list of all available fields for an object.

**Arguments**:

- `obj`: The name of the Salesforce object that we are getting a description of.

**Returns**:

`list(str)`: the names of the fields.

<a id="hooks.salesforce.SalesforceHook.get_object_from_salesforce"></a>

#### get\_object\_from\_salesforce

```python
def get_object_from_salesforce(obj: str, fields: Iterable[str]) -> dict
```

Get all instances of the `object` from Salesforce.

For each model, only get the fields specified in fields.

All we really do underneath the hood is run:
    SELECT <fields> FROM <obj>;

**Arguments**:

- `obj`: The object name to get from Salesforce.
- `fields`: The fields to get from the object.

**Returns**:

`dict`: all instances of the object from Salesforce.

<a id="hooks.salesforce.SalesforceHook.write_object_to_file"></a>

#### write\_object\_to\_file

```python
def write_object_to_file(query_results: List[dict],
                         filename: str,
                         fmt: str = "csv",
                         coerce_to_timestamp: bool = False,
                         record_time_added: bool = False) -> pd.DataFrame
```

Write query results to file.

Acceptable formats are:
    - csv:
        comma-separated-values file. This is the default format.
    - json:
        JSON array. Each element in the array is a different row.
    - ndjson:
        JSON array but each element is new-line delimited instead of comma delimited like in `json`

This requires a significant amount of cleanup.
Pandas doesn't handle output to CSV and json in a uniform way.
This is especially painful for datetime types.
Pandas wants to write them as strings in CSV, but as millisecond Unix timestamps.

By default, this function will try and leave all values as they are represented in Salesforce.
You use the `coerce_to_timestamp` flag to force all datetimes to become Unix timestamps (UTC).
This is can be greatly beneficial as it will make all of your datetime fields look the same,
and makes it easier to work with in other database environments

**Arguments**:

- `query_results`: the results from a SQL query
- `filename`: the name of the file where the data should be dumped to
- `fmt`: the format you want the output in. Default:  'csv'
- `coerce_to_timestamp`: True if you want all datetime fields to be converted into Unix timestamps.
False if you want them to be left in the same format as they were in Salesforce.
Leaving the value as False will result in datetimes being strings. Default: False
- `record_time_added`: True if you want to add a Unix timestamp field
to the resulting data that marks when the data was fetched from Salesforce. Default: False

**Returns**:

`pandas.Dataframe`: the dataframe that gets written to the file.

<a id="hooks.salesforce.SalesforceHook.object_to_df"></a>

#### object\_to\_df

```python
def object_to_df(query_results: List[dict],
                 coerce_to_timestamp: bool = False,
                 record_time_added: bool = False) -> pd.DataFrame
```

Export query results to dataframe.

By default, this function will try and leave all values as they are represented in Salesforce.
You use the `coerce_to_timestamp` flag to force all datetimes to become Unix timestamps (UTC).
This is can be greatly beneficial as it will make all of your datetime fields look the same,
and makes it easier to work with in other database environments

**Arguments**:

- `query_results`: the results from a SQL query
- `coerce_to_timestamp`: True if you want all datetime fields to be converted into Unix timestamps.
False if you want them to be left in the same format as they were in Salesforce.
Leaving the value as False will result in datetimes being strings. Default: False
- `record_time_added`: True if you want to add a Unix timestamp field
to the resulting data that marks when the data was fetched from Salesforce. Default: False

**Returns**:

`pandas.Dataframe`: the dataframe.

