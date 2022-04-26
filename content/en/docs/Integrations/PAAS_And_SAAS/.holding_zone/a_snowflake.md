---
title: "snowflake"
linkTitle: "snowflake"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     snowflake Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.snowflake"></a>

# operators.snowflake

<a id="operators.snowflake.get_db_hook"></a>

#### get\_db\_hook

```python
def get_db_hook(self) -> SnowflakeHook
```

Create and return SnowflakeHook.

**Returns**:

`SnowflakeHook`: a SnowflakeHook instance.

<a id="operators.snowflake.SnowflakeOperator"></a>

## SnowflakeOperator Objects

```python
class SnowflakeOperator(BaseOperator)
```

Executes SQL code in a Snowflake database

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SnowflakeOperator`

**Arguments**:

- `snowflake_conn_id`: Reference to
:ref:`Snowflake connection id<howto/connection:snowflake>`
- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
Template references are recognized by str ending in '.sql'
- `autocommit`: if True, each command is automatically committed.
(default value: True)
- `parameters`: (optional) the parameters to render the SQL query with.
- `warehouse`: name of warehouse (will overwrite any warehouse
defined in the connection's extra JSON)
- `database`: name of database (will overwrite database defined
in connection)
- `schema`: name of schema (will overwrite schema defined in
connection)
- `role`: name of role (will overwrite any role defined in
connection's extra JSON)
- `authenticator`: authenticator for Snowflake.
'snowflake' (default) to use the internal Snowflake authenticator
'externalbrowser' to authenticate using your web browser and
Okta, ADFS or any other SAML 2.0-compliant identify provider
(IdP) that has been defined for your account
'https://<your_okta_account_name>.okta.com' to authenticate
through native Okta.
- `session_parameters`: You can set session-level parameters at
the time you connect to Snowflake

<a id="operators.snowflake.SnowflakeOperator.execute"></a>

#### execute

```python
def execute(context: Any) -> None
```

Run query on snowflake

<a id="operators.snowflake.SnowflakeCheckOperator"></a>

## SnowflakeCheckOperator Objects

```python
class SnowflakeCheckOperator(SQLCheckOperator)
```

Performs a check against Snowflake. The ``SnowflakeCheckOperator`` expects

a sql query that will return a single row. Each value on that
first row is evaluated using python ``bool`` casting. If any of the
values return ``False`` the check is failed and errors out.

Note that Python bool casting evals the following as ``False``:

* ``False``
* ``0``
* Empty string (``""``)
* Empty list (``[]``)
* Empty dictionary or set (``{}``)

Given a query like ``SELECT COUNT(*) FROM foo``, it will fail only if
the count ``== 0``. You can craft much more complex query that could,
for instance, check that the table has the same number of rows as
the source table upstream, or that the count of today's partition is
greater than yesterday's partition, or that a set of metrics are less
than 3 standard deviation for the 7 day average.

This operator can be used as a data quality check in your pipeline, and
depending on where you put it in your DAG, you have the choice to
stop the critical path, preventing from
publishing dubious data, or on the side and receive email alerts
without stopping the progress of the DAG.

**Arguments**:

- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
Template references are recognized by str ending in '.sql'
- `snowflake_conn_id`: Reference to
:ref:`Snowflake connection id<howto/connection:snowflake>`
- `autocommit`: if True, each command is automatically committed.
(default value: True)
- `parameters`: (optional) the parameters to render the SQL query with.
- `warehouse`: name of warehouse (will overwrite any warehouse
defined in the connection's extra JSON)
- `database`: name of database (will overwrite database defined
in connection)
- `schema`: name of schema (will overwrite schema defined in
connection)
- `role`: name of role (will overwrite any role defined in
connection's extra JSON)
- `authenticator`: authenticator for Snowflake.
'snowflake' (default) to use the internal Snowflake authenticator
'externalbrowser' to authenticate using your web browser and
Okta, ADFS or any other SAML 2.0-compliant identify provider
(IdP) that has been defined for your account
'https://<your_okta_account_name>.okta.com' to authenticate
through native Okta.
- `session_parameters`: You can set session-level parameters at
the time you connect to Snowflake

<a id="operators.snowflake.SnowflakeValueCheckOperator"></a>

## SnowflakeValueCheckOperator Objects

```python
class SnowflakeValueCheckOperator(SQLValueCheckOperator)
```

Performs a simple check using sql code against a specified value, within a

certain level of tolerance.

**Arguments**:

- `sql`: the sql to be executed
- `pass_value`: the value to check against
- `tolerance`: (optional) the tolerance allowed to accept the query as
passing
- `snowflake_conn_id`: Reference to
:ref:`Snowflake connection id<howto/connection:snowflake>`
- `autocommit`: if True, each command is automatically committed.
(default value: True)
- `parameters`: (optional) the parameters to render the SQL query with.
- `warehouse`: name of warehouse (will overwrite any warehouse
defined in the connection's extra JSON)
- `database`: name of database (will overwrite database defined
in connection)
- `schema`: name of schema (will overwrite schema defined in
connection)
- `role`: name of role (will overwrite any role defined in
connection's extra JSON)
- `authenticator`: authenticator for Snowflake.
'snowflake' (default) to use the internal Snowflake authenticator
'externalbrowser' to authenticate using your web browser and
Okta, ADFS or any other SAML 2.0-compliant identify provider
(IdP) that has been defined for your account
'https://<your_okta_account_name>.okta.com' to authenticate
through native Okta.
- `session_parameters`: You can set session-level parameters at
the time you connect to Snowflake

<a id="operators.snowflake.SnowflakeIntervalCheckOperator"></a>

## SnowflakeIntervalCheckOperator Objects

```python
class SnowflakeIntervalCheckOperator(SQLIntervalCheckOperator)
```

Checks that the values of metrics given as SQL expressions are within

a certain tolerance of the ones from days_back before.

This method constructs a query like so ::

    SELECT {metrics_threshold_dict_key} FROM {table}
    WHERE {date_filter_column}=<date>

**Arguments**:

- `table`: the table name
- `days_back`: number of days between ds and the ds we want to check
against. Defaults to 7 days
- `metrics_thresholds`: a dictionary of ratios indexed by metrics, for
example 'COUNT(*)': 1.5 would require a 50 percent or less difference
between the current day, and the prior days_back.
- `snowflake_conn_id`: Reference to
:ref:`Snowflake connection id<howto/connection:snowflake>`
- `autocommit`: if True, each command is automatically committed.
(default value: True)
- `parameters`: (optional) the parameters to render the SQL query with.
- `warehouse`: name of warehouse (will overwrite any warehouse
defined in the connection's extra JSON)
- `database`: name of database (will overwrite database defined
in connection)
- `schema`: name of schema (will overwrite schema defined in
connection)
- `role`: name of role (will overwrite any role defined in
connection's extra JSON)
- `authenticator`: authenticator for Snowflake.
'snowflake' (default) to use the internal Snowflake authenticator
'externalbrowser' to authenticate using your web browser and
Okta, ADFS or any other SAML 2.0-compliant identify provider
(IdP) that has been defined for your account
'https://<your_okta_account_name>.okta.com' to authenticate
through native Okta.
- `session_parameters`: You can set session-level parameters at
the time you connect to Snowflake

<a id="transfers"></a>

# transfers

<a id="transfers.snowflake_to_slack"></a>

# transfers.snowflake\_to\_slack

<a id="transfers.snowflake_to_slack.SnowflakeToSlackOperator"></a>

## SnowflakeToSlackOperator Objects

```python
class SnowflakeToSlackOperator(BaseOperator)
```

Executes an SQL statement in Snowflake and sends the results to Slack. The results of the query are

rendered into the 'slack_message' parameter as a Pandas dataframe using a JINJA variable called '{{
results_df }}'. The 'results_df' variable name can be changed by specifying a different
'results_df_name' parameter. The Tabulate library is added to the JINJA environment as a filter to
allow the dataframe to be rendered nicely. For example, set 'slack_message' to {{ results_df |
tabulate(tablefmt="pretty", headers="keys") }} to send the results to Slack as an ascii rendered table.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SnowflakeToSlackOperator`

**Arguments**:

- `sql`: The SQL statement to execute on Snowflake (templated)
- `slack_message`: The templated Slack message to send with the data returned from Snowflake.
You can use the default JINJA variable {{ results_df }} to access the pandas dataframe containing the
SQL results
- `snowflake_conn_id`: Reference to
:ref:`Snowflake connection id<howto/connection:snowflake>`
- `slack_conn_id`: The connection id for Slack
- `results_df_name`: The name of the JINJA template's dataframe variable, default is 'results_df'
- `parameters`: The parameters to pass to the SQL query
- `warehouse`: The Snowflake virtual warehouse to use to run the SQL query
- `database`: The Snowflake database to use for the SQL query
- `schema`: The schema to run the SQL against in Snowflake
- `role`: The role to use when connecting to Snowflake
- `slack_token`: The token to use to authenticate to Slack. If this is not provided, the
'webhook_token' attribute needs to be specified in the 'Extra' JSON field against the slack_conn_id

<a id="transfers.s3_to_snowflake"></a>

# transfers.s3\_to\_snowflake

This module contains AWS S3 to Snowflake operator.

<a id="transfers.s3_to_snowflake.S3ToSnowflakeOperator"></a>

## S3ToSnowflakeOperator Objects

```python
class S3ToSnowflakeOperator(BaseOperator)
```

Executes an COPY command to load files from s3 to Snowflake

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:S3ToSnowflakeOperator`

**Arguments**:

- `s3_keys`: reference to a list of S3 keys
- `table`: reference to a specific table in snowflake database
- `schema`: name of schema (will overwrite schema defined in
connection)
- `stage`: reference to a specific snowflake stage. If the stage's schema is not the same as the
table one, it must be specified
- `prefix`: cloud storage location specified to limit the set of files to load
- `file_format`: reference to a specific file format
- `warehouse`: name of warehouse (will overwrite any warehouse
defined in the connection's extra JSON)
- `database`: reference to a specific database in Snowflake connection
- `columns_array`: reference to a specific columns array in snowflake database
- `snowflake_conn_id`: Reference to
:ref:`Snowflake connection id<howto/connection:snowflake>`
- `role`: name of role (will overwrite any role defined in
connection's extra JSON)
- `authenticator`: authenticator for Snowflake.
'snowflake' (default) to use the internal Snowflake authenticator
'externalbrowser' to authenticate using your web browser and
Okta, ADFS or any other SAML 2.0-compliant identify provider
(IdP) that has been defined for your account
'https://<your_okta_account_name>.okta.com' to authenticate
through native Okta.
- `session_parameters`: You can set session-level parameters at
the time you connect to Snowflake

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_snowflake"></a>

# example\_dags.example\_snowflake

Example use of Snowflake related operators.

<a id="hooks"></a>

# hooks

<a id="hooks.snowflake"></a>

# hooks.snowflake

<a id="hooks.snowflake.SnowflakeHook"></a>

## SnowflakeHook Objects

```python
class SnowflakeHook(DbApiHook)
```

A client to interact with Snowflake.

This hook requires the snowflake_conn_id connection. The snowflake host, login,
and, password field must be setup in the connection. Other inputs can be defined
in the connection or hook instantiation.

**Arguments**:

- `snowflake_conn_id`: Reference to
:ref:`Snowflake connection id<howto/connection:snowflake>`
- `account`: snowflake account name
- `authenticator`: authenticator for Snowflake.
'snowflake' (default) to use the internal Snowflake authenticator
'externalbrowser' to authenticate using your web browser and
Okta, ADFS or any other SAML 2.0-compliant identify provider
(IdP) that has been defined for your account
``https://<your_okta_account_name>.okta.com`` to authenticate
through native Okta.
- `warehouse`: name of snowflake warehouse
- `database`: name of snowflake database
- `region`: name of snowflake region
- `role`: name of snowflake role
- `schema`: name of snowflake schema
- `session_parameters`: You can set session-level parameters at
the time you connect to Snowflake
- `insecure_mode`: Turns off OCSP certificate checks.
For details, see: `How To: Turn Off OCSP Checking in Snowflake Client Drivers - Snowflake Community
    <https://community.snowflake.com/s/article/How-to-turn-off-OCSP-checking-in-Snowflake-client-drivers>`__

.. note::
    ``get_sqlalchemy_engine()`` depends on ``snowflake-sqlalchemy``

.. seealso::
    For more information on how to use this Snowflake connection, take a look at the guide:
    :ref:`howto/operator:SnowflakeOperator`

<a id="hooks.snowflake.SnowflakeHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="hooks.snowflake.SnowflakeHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.snowflake.SnowflakeHook.get_uri"></a>

#### get\_uri

```python
def get_uri() -> str
```

Override DbApiHook get_uri method for get_sqlalchemy_engine()

<a id="hooks.snowflake.SnowflakeHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> SnowflakeConnection
```

Returns a snowflake.connection object

<a id="hooks.snowflake.SnowflakeHook.get_sqlalchemy_engine"></a>

#### get\_sqlalchemy\_engine

```python
def get_sqlalchemy_engine(engine_kwargs=None)
```

Get an sqlalchemy_engine object.

**Arguments**:

- `engine_kwargs`: Kwargs used in :func:`~sqlalchemy.create_engine`.

**Returns**:

the created engine.

<a id="hooks.snowflake.SnowflakeHook.run"></a>

#### run

```python
def run(sql: Union[str, list],
        autocommit: bool = False,
        parameters: Optional[Union[Sequence[Any], Dict[Any, Any]]] = None,
        handler: Optional[Callable] = None)
```

Runs a command or a list of commands. Pass a list of sql

statements to the sql parameter to get them to execute
sequentially. The variable execution_info is returned so that
it can be used in the Operators to modify the behavior
depending on the result of the query (i.e fail the operator
if the copy has processed 0 files)

**Arguments**:

- `sql`: the sql string to be executed with possibly multiple statements,
or a list of sql statements to execute
- `autocommit`: What to set the connection's autocommit setting to
before executing the query.
- `parameters`: The parameters to render the SQL query with.
- `handler`: The result handler which is called with the result of each statement.

<a id="hooks.snowflake.SnowflakeHook.test_connection"></a>

#### test\_connection

```python
def test_connection()
```

Test the Snowflake connection by running a simple query.

