---
title: "oracle"
linkTitle: "oracle"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     oracle Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.oracle"></a>

# operators.oracle

<a id="operators.oracle.OracleOperator"></a>

## OracleOperator Objects

```python
class OracleOperator(BaseOperator)
```

Executes sql code in a specific Oracle database.

**Arguments**:

- `sql`: the sql code to be executed. Can receive a str representing a sql statement,
a list of str (sql statements), or reference to a template file.
Template reference are recognized by str ending in '.sql'
(templated)
- `oracle_conn_id`: The :ref:`Oracle connection id <howto/connection:oracle>`
reference to a specific Oracle database.
- `parameters`: (optional) the parameters to render the SQL query with.
- `autocommit`: if True, each command is automatically committed.
(default value: False)

<a id="operators.oracle.OracleStoredProcedureOperator"></a>

## OracleStoredProcedureOperator Objects

```python
class OracleStoredProcedureOperator(BaseOperator)
```

Executes stored procedure in a specific Oracle database.

**Arguments**:

- `procedure`: name of stored procedure to call (templated)
- `oracle_conn_id`: The :ref:`Oracle connection id <howto/connection:oracle>`
reference to a specific Oracle database.
- `parameters`: (optional) the parameters provided in the call

<a id="transfers"></a>

# transfers

<a id="transfers.oracle_to_oracle"></a>

# transfers.oracle\_to\_oracle

<a id="transfers.oracle_to_oracle.OracleToOracleOperator"></a>

## OracleToOracleOperator Objects

```python
class OracleToOracleOperator(BaseOperator)
```

Moves data from Oracle to Oracle.

**Arguments**:

- `oracle_destination_conn_id`: destination Oracle connection.
- `destination_table`: destination table to insert rows.
- `oracle_source_conn_id`: :ref:`Source Oracle connection <howto/connection:oracle>`.
- `source_sql`: SQL query to execute against the source Oracle
database. (templated)
- `source_sql_params`: Parameters to use in sql query. (templated)
- `rows_chunk`: number of rows per chunk to commit.

<a id="hooks"></a>

# hooks

<a id="hooks.oracle"></a>

# hooks.oracle

<a id="hooks.oracle.OracleHook"></a>

## OracleHook Objects

```python
class OracleHook(DbApiHook)
```

Interact with Oracle SQL.

**Arguments**:

- `oracle_conn_id`: The :ref:`Oracle connection id <howto/connection:oracle>`
used for Oracle credentials.

<a id="hooks.oracle.OracleHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> 'OracleHook'
```

Returns a oracle connection object

Optional parameters for using a custom DSN connection
(instead of using a server alias from tnsnames.ora)
The dsn (data source name) is the TNS entry
(from the Oracle names server or tnsnames.ora file)
or is a string like the one returned from makedsn().

**Arguments**:

- `dsn`: the data source name for the Oracle server
- `service_name`: the db_unique_name of the database
that you are connecting to (CONNECT_DATA part of TNS)
- `sid`: Oracle System ID that identifies a particular
database on a system

You can set these parameters in the extra fields of your connection
as in

.. code-block:: python

   {
       "dsn": (
           "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)"
           "(HOST=host)(PORT=1521))(CONNECT_DATA=(SID=sid)))"
       )
   }

see more param detail in
`cx_Oracle.connect <https://cx-oracle.readthedocs.io/en/latest/module.html#cx_Oracle.connect>`_

<a id="hooks.oracle.OracleHook.insert_rows"></a>

#### insert\_rows

