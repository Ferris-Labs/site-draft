---
title: "postgres"
linkTitle: "postgres"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     postgres Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.postgres"></a>

# operators.postgres

<a id="operators.postgres.PostgresOperator"></a>

## PostgresOperator Objects

```python
class PostgresOperator(BaseOperator)
```

Executes sql code in a specific Postgres database

**Arguments**:

- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
Template references are recognized by str ending in '.sql'
- `postgres_conn_id`: The :ref:`postgres conn id <howto/connection:postgres>`
reference to a specific postgres database.
- `autocommit`: if True, each command is automatically committed.
(default value: False)
- `parameters`: (optional) the parameters to render the SQL query with.
- `database`: name of database which overwrite defined one in connection

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_postgres"></a>

# example\_dags.example\_postgres

<a id="hooks"></a>

# hooks

<a id="hooks.postgres"></a>

# hooks.postgres

<a id="hooks.postgres.PostgresHook"></a>

## PostgresHook Objects

```python
class PostgresHook(DbApiHook)
```

Interact with Postgres.

You can specify ssl parameters in the extra field of your connection
as ``{"sslmode": "require", "sslcert": "/path/to/cert.pem", etc}``.
Also you can choose cursor as ``{"cursor": "dictcursor"}``. Refer to the
psycopg2.extras for more details.

Note: For Redshift, use keepalives_idle in the extra connection parameters
and set it to less than 300 seconds.

Note: For AWS IAM authentication, use iam in the extra connection parameters
and set it to true. Leave the password field empty. This will use the
"aws_default" connection to get the temporary token unless you override
in extras.
extras example: ``{"iam":true, "aws_conn_id":"my_aws_conn"}``
For Redshift, also use redshift in the extra connection parameters and
set it to true. The cluster-identifier is extracted from the beginning of
the host field, so is optional. It can however be overridden in the extra field.
extras example: ``{"iam":true, "redshift":true, "cluster-identifier": "my_cluster_id"}``

**Arguments**:

- `postgres_conn_id`: The :ref:`postgres conn id <howto/connection:postgres>`
reference to a specific postgres database.

<a id="hooks.postgres.PostgresHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> connection
```

Establishes a connection to a postgres database.

<a id="hooks.postgres.PostgresHook.copy_expert"></a>

#### copy\_expert

```python
def copy_expert(sql: str, filename: str) -> None
```

Executes SQL using psycopg2 copy_expert method.
Necessary to execute COPY command without access to a superuser.

Note: if this method is called with a "COPY FROM" statement and
the specified input file does not exist, it creates an empty
file and no data is loaded, but the operation succeeds.
So if users want to be aware when the input file does not exist,
they have to check its existence by themselves.

<a id="hooks.postgres.PostgresHook.get_uri"></a>

#### get\_uri

```python
def get_uri() -> str
```

Extract the URI from the connection.

**Returns**:

the extracted uri.

<a id="hooks.postgres.PostgresHook.bulk_load"></a>

#### bulk\_load

```python
def bulk_load(table: str, tmp_file: str) -> None
```

Loads a tab-delimited file into a database table

<a id="hooks.postgres.PostgresHook.bulk_dump"></a>

#### bulk\_dump

```python
def bulk_dump(table: str, tmp_file: str) -> None
```

Dumps a database table into a tab-delimited file

<a id="hooks.postgres.PostgresHook.get_iam_token"></a>

#### get\_iam\_token

```python
def get_iam_token(conn: Connection) -> Tuple[str, str, int]
```

Uses AWSHook to retrieve a temporary password to connect to Postgres
or Redshift. Port is required. If none is provided, default is used for
each service

<a id="hooks.postgres.PostgresHook.get_table_primary_key"></a>

#### get\_table\_primary\_key

```python
def get_table_primary_key(table: str,
                          schema: Optional[str] = "public"
                          ) -> Optional[List[str]]
```

Helper method that returns the table primary key

**Arguments**:

- `table`: Name of the target table
- `schema`: Name of the target schema, public by default

**Returns**:

`List[str]`: Primary key columns list

