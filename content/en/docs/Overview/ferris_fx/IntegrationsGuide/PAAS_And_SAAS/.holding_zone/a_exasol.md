---
title: "exasol"
linkTitle: "exasol"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     exasol Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.exasol"></a>

# operators.exasol

<a id="operators.exasol.ExasolOperator"></a>

## ExasolOperator Objects

```python
class ExasolOperator(BaseOperator)
```

Executes sql code in a specific Exasol database

**Arguments**:

- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
template references are recognized by str ending in '.sql'
- `exasol_conn_id`: reference to a specific Exasol database
- `autocommit`: if True, each command is automatically committed.
(default value: False)
- `parameters`: (optional) the parameters to render the SQL query with.
- `schema`: (optional) name of the schema which overwrite defined one in connection

<a id="hooks"></a>

# hooks

<a id="hooks.exasol"></a>

# hooks.exasol

<a id="hooks.exasol.ExasolHook"></a>

## ExasolHook Objects

```python
class ExasolHook(DbApiHook)
```

Interact with Exasol.
You can specify the pyexasol ``compression``, ``encryption``, ``json_lib``
and ``client_name``  parameters in the extra field of your connection
as ``{"compression": True, "json_lib": "rapidjson", etc}``.
See `pyexasol reference
<https://github.com/badoo/pyexasol/blob/master/docs/REFERENCE.md#connect>`_
for more details.

<a id="hooks.exasol.ExasolHook.get_pandas_df"></a>

#### get\_pandas\_df

```python
def get_pandas_df(sql: Union[str, list],
                  parameters: Optional[dict] = None,
                  **kwargs) -> pd.DataFrame
```

Executes the sql and returns a pandas dataframe

**Arguments**:

- `sql`: the sql statement to be executed (str) or a list of
sql statements to execute
- `parameters`: The parameters to render the SQL query with.
- `kwargs`: (optional) passed into pyexasol.ExaConnection.export_to_pandas method

<a id="hooks.exasol.ExasolHook.get_records"></a>

#### get\_records

```python
def get_records(
        sql: Union[str, list],
        parameters: Optional[dict] = None
) -> List[Union[dict, Tuple[Any, ...]]]
```

Executes the sql and returns a set of records.

**Arguments**:

- `sql`: the sql statement to be executed (str) or a list of
sql statements to execute
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.exasol.ExasolHook.get_first"></a>

#### get\_first

```python
def get_first(sql: Union[str, list],
              parameters: Optional[dict] = None) -> Optional[Any]
```

Executes the sql and returns the first resulting row.

**Arguments**:

- `sql`: the sql statement to be executed (str) or a list of
sql statements to execute
- `parameters`: The parameters to render the SQL query with.

<a id="hooks.exasol.ExasolHook.export_to_file"></a>

#### export\_to\_file

```python
def export_to_file(filename: str,
                   query_or_table: str,
                   query_params: Optional[Dict] = None,
                   export_params: Optional[Dict] = None) -> None
```

Exports data to a file.

**Arguments**:

- `filename`: Path to the file to which the data has to be exported
- `query_or_table`: the sql statement to be executed or table name to export
- `query_params`: Query parameters passed to underlying ``export_to_file``
method of :class:`~pyexasol.connection.ExaConnection`.
- `export_params`: Extra parameters passed to underlying ``export_to_file``
method of :class:`~pyexasol.connection.ExaConnection`.

<a id="hooks.exasol.ExasolHook.run"></a>

#### run

```python
def run(sql: Union[str, list],
        autocommit: bool = False,
        parameters: Optional[dict] = None,
        handler=None) -> None
```

Runs a command or a list of commands. Pass a list of sql

statements to the sql parameter to get them to execute
sequentially

**Arguments**:

- `sql`: the sql statement to be executed (str) or a list of
sql statements to execute
- `autocommit`: What to set the connection's autocommit setting to
before executing the query.
- `parameters`: The parameters to render the SQL query with.
- `handler`: The result handler which is called with the result of each statement.

<a id="hooks.exasol.ExasolHook.set_autocommit"></a>

#### set\_autocommit

```python
def set_autocommit(conn, autocommit: bool) -> None
```

Sets the autocommit flag on the connection

**Arguments**:

- `conn`: Connection to set autocommit setting to.
- `autocommit`: The autocommit setting to set.

<a id="hooks.exasol.ExasolHook.get_autocommit"></a>

#### get\_autocommit

```python
def get_autocommit(conn) -> bool
```

Get autocommit setting for the provided connection.

Return True if autocommit is set.
Return False if autocommit is not set or set to False or conn
does not support autocommit.

**Arguments**:

- `conn`: Connection to get autocommit setting from.

**Returns**:

`bool`: connection autocommit setting.

