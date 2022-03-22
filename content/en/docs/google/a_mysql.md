---
title: "mysql"
linkTitle: "mysql"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     mysql Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.mysql"></a>

# operators.mysql

<a id="operators.mysql.MySqlOperator"></a>

## MySqlOperator Objects

```python
class MySqlOperator(BaseOperator)
```

Executes sql code in a specific MySQL database

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:MySqlOperator`

**Arguments**:

- `sql`: the sql code to be executed. Can receive a str representing a
sql statement, a list of str (sql statements), or reference to a template file.
Template reference are recognized by str ending in '.sql'
(templated)
- `mysql_conn_id`: Reference to :ref:`mysql connection id <howto/connection:mysql>`.
- `parameters`: (optional) the parameters to render the SQL query with.
Template reference are recognized by str ending in '.json'
(templated)
- `autocommit`: if True, each command is automatically committed.
(default value: False)
- `database`: name of database which overwrite defined one in connection

<a id="operators.mysql.MySqlOperator.prepare_template"></a>

#### prepare\_template

```python
def prepare_template() -> None
```

Parse template file for attribute parameters.

<a id="transfers"></a>

# transfers

<a id="transfers.trino_to_mysql"></a>

# transfers.trino\_to\_mysql

<a id="transfers.trino_to_mysql.TrinoToMySqlOperator"></a>

## TrinoToMySqlOperator Objects

```python
class TrinoToMySqlOperator(BaseOperator)
```

Moves data from Trino to MySQL, note that for now the data is loaded

into memory before being pushed to MySQL, so this operator should
be used for smallish amount of data.

**Arguments**:

- `sql`: SQL query to execute against Trino. (templated)
- `mysql_table`: target MySQL table, use dot notation to target a
specific database. (templated)
- `mysql_conn_id`: Reference to :ref:`mysql connection id <howto/connection:mysql>`.
- `trino_conn_id`: source trino connection
- `mysql_preoperator`: sql statement to run against mysql prior to
import, typically use to truncate of delete in place
of the data coming in, allowing the task to be idempotent (running
the task twice won't double load data). (templated)

<a id="transfers.s3_to_mysql"></a>

# transfers.s3\_to\_mysql

<a id="transfers.s3_to_mysql.S3ToMySqlOperator"></a>

## S3ToMySqlOperator Objects

```python
class S3ToMySqlOperator(BaseOperator)
```

Loads a file from S3 into a MySQL table.

**Arguments**:

- `s3_source_key`: The path to the file (S3 key) that will be loaded into MySQL.
- `mysql_table`: The MySQL table into where the data will be sent.
- `mysql_duplicate_key_handling`: Specify what should happen to duplicate data.
You can choose either `IGNORE` or `REPLACE`.

.. seealso::
    https://dev.mysql.com/doc/refman/8.0/en/load-data.html#load-data-duplicate-key-handling
- `mysql_extra_options`: MySQL options to specify exactly how to load the data.
- `aws_conn_id`: The S3 connection that contains the credentials to the S3 Bucket.
- `mysql_conn_id`: Reference to :ref:`mysql connection id <howto/connection:mysql>`.

<a id="transfers.s3_to_mysql.S3ToMySqlOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Executes the transfer operation from S3 to MySQL.

**Arguments**:

- `context`: The context that is being provided when executing.

<a id="transfers.presto_to_mysql"></a>

# transfers.presto\_to\_mysql

<a id="transfers.presto_to_mysql.PrestoToMySqlOperator"></a>

## PrestoToMySqlOperator Objects

```python
class PrestoToMySqlOperator(BaseOperator)
```

Moves data from Presto to MySQL, note that for now the data is loaded

into memory before being pushed to MySQL, so this operator should
be used for smallish amount of data.

**Arguments**:

- `sql`: SQL query to execute against Presto. (templated)
- `mysql_table`: target MySQL table, use dot notation to target a
specific database. (templated)
- `mysql_conn_id`: Reference to :ref:`mysql connection id <howto/connection:mysql>`.
- `presto_conn_id`: source presto connection
- `mysql_preoperator`: sql statement to run against mysql prior to
import, typically use to truncate of delete in place
of the data coming in, allowing the task to be idempotent (running
the task twice won't double load data). (templated)

<a id="transfers.vertica_to_mysql"></a>

# transfers.vertica\_to\_mysql

<a id="transfers.vertica_to_mysql.VerticaToMySqlOperator"></a>

## VerticaToMySqlOperator Objects

```python
class VerticaToMySqlOperator(BaseOperator)
```

Moves data from Vertica to MySQL.

**Arguments**:

- `sql`: SQL query to execute against the Vertica database. (templated)
- `vertica_conn_id`: source Vertica connection
- `mysql_table`: target MySQL table, use dot notation to target a
specific database. (templated)
- `mysql_conn_id`: Reference to :ref:`mysql connection id <howto/connection:mysql>`.
- `mysql_preoperator`: sql statement to run against MySQL prior to
import, typically use to truncate of delete in place of the data
coming in, allowing the task to be idempotent (running the task
twice won't double load data). (templated)
- `mysql_postoperator`: sql statement to run against MySQL after the
import, typically used to move data from staging to production
and issue cleanup commands. (templated)
- `bulk_load`: flag to use bulk_load option.  This loads MySQL directly
from a tab-delimited text file using the LOAD DATA LOCAL INFILE command.
This option requires an extra connection parameter for the
destination MySQL connection: {'local_infile': true}.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_mysql"></a>

# example\_dags.example\_mysql

Example use of MySql related operators.

<a id="hooks"></a>

# hooks

<a id="hooks.mysql"></a>

# hooks.mysql

This module allows to connect to a MySQL database.

<a id="hooks.mysql.MySqlHook"></a>

## MySqlHook Objects

```python
class MySqlHook(DbApiHook)
```

Interact with MySQL.

You can specify charset in the extra field of your connection
as ``{"charset": "utf8"}``. Also you can choose cursor as
``{"cursor": "SSCursor"}``. Refer to the MySQLdb.cursors for more details.

Note: For AWS IAM authentication, use iam in the extra connection parameters
and set it to true. Leave the password field empty. This will use the
"aws_default" connection to get the temporary token unless you override
in extras.
extras example: ``{"iam":true, "aws_conn_id":"my_aws_conn"}``

**Arguments**:

- `schema`: The MySQL database schema to connect to.
- `connection`: The :ref:`MySQL connection id <howto/connection:mysql>` used for MySQL credentials.

<a id="hooks.mysql.MySqlHook.set_autocommit"></a>

#### set\_autocommit

```python
def set_autocommit(conn: MySQLConnectionTypes, autocommit: bool) -> None
```

The MySQLdb (mysqlclient) client uses an `autocommit` method rather

than an `autocommit` property to set the autocommit setting

**Arguments**:

- `conn`: connection to set autocommit setting
- `autocommit`: autocommit setting

<a id="hooks.mysql.MySqlHook.get_autocommit"></a>

#### get\_autocommit

```python
def get_autocommit(conn: MySQLConnectionTypes) -> bool
```

The MySQLdb (mysqlclient) client uses a `get_autocommit` method

rather than an `autocommit` property to get the autocommit setting

**Arguments**:

- `conn`: connection to get autocommit setting from.

**Returns**:

`bool`: connection autocommit setting

<a id="hooks.mysql.MySqlHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> MySQLConnectionTypes
```

Establishes a connection to a mysql database

by extracting the connection configuration from the Airflow connection.

.. note:: By default it connects to the database via the mysqlclient library.
    But you can also choose the mysql-connector-python library which lets you connect through ssl
    without any further ssl parameters required.

**Returns**:

a mysql connection object

<a id="hooks.mysql.MySqlHook.bulk_load"></a>

#### bulk\_load

```python
def bulk_load(table: str, tmp_file: str) -> None
```

Loads a tab-delimited file into a database table

<a id="hooks.mysql.MySqlHook.bulk_dump"></a>

#### bulk\_dump

```python
def bulk_dump(table: str, tmp_file: str) -> None
```

Dumps a database table into a tab-delimited file

<a id="hooks.mysql.MySqlHook.get_iam_token"></a>

#### get\_iam\_token

```python
def get_iam_token(conn: Connection) -> Tuple[str, int]
```

Uses AWSHook to retrieve a temporary password to connect to MySQL
Port is required. If none is provided, default 3306 is used

<a id="hooks.mysql.MySqlHook.bulk_load_custom"></a>

#### bulk\_load\_custom

```python
def bulk_load_custom(table: str,
                     tmp_file: str,
                     duplicate_key_handling: str = 'IGNORE',
                     extra_options: str = '') -> None
```

A more configurable way to load local data from a file into the database.

.. warning:: According to the mysql docs using this function is a
    `security risk <https://dev.mysql.com/doc/refman/8.0/en/load-data-local.html>`_.
    If you want to use it anyway you can do so by setting a client-side + server-side option.
    This depends on the mysql client library used.

**Arguments**:

- `table`: The table were the file will be loaded into.
- `tmp_file`: The file (name) that contains the data.
- `duplicate_key_handling`: Specify what should happen to duplicate data.
You can choose either `IGNORE` or `REPLACE`.

.. seealso::
    https://dev.mysql.com/doc/refman/8.0/en/load-data.html#load-data-duplicate-key-handling
- `extra_options`: More sql options to specify exactly how to load the data.
.. seealso:: https://dev.mysql.com/doc/refman/8.0/en/load-data.html

