---
title: "databricks"
linkTitle: "databricks"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     databricks Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.databricks_sql"></a>

# operators.databricks\_sql

This module contains Databricks operators.

<a id="operators.databricks_sql.DatabricksSqlOperator"></a>

## DatabricksSqlOperator Objects

```python
class DatabricksSqlOperator(BaseOperator)
```

Executes SQL code in a Databricks SQL endpoint or a Databricks cluster

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:DatabricksSqlOperator`

**Arguments**:

- `databricks_conn_id`: Reference to
:ref:`Databricks connection id<howto/connection:databricks>`
- `http_path`: Optional string specifying HTTP path of Databricks SQL Endpoint or cluster.
If not specified, it should be either specified in the Databricks connection's extra parameters,
or ``sql_endpoint_name`` must be specified.
- `sql_endpoint_name`: Optional name of Databricks SQL Endpoint. If not specified, ``http_path`` must
be provided as described above.
- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file. (templated)
Template references are recognized by str ending in '.sql'
- `parameters`: (optional) the parameters to render the SQL query with.
- `session_configuration`: An optional dictionary of Spark session parameters. Defaults to None.
If not specified, it could be specified in the Databricks connection's extra parameters.
- `output_path`: optional string specifying the file to which write selected data. (templated)
- `output_format`: format of output data if ``output_path` is specified.
Possible values are ``csv``, ``json``, ``jsonl``. Default is ``csv``.
- `csv_params`: parameters that will be passed to the ``csv.DictWriter`` class used to write CSV data.

<a id="operators.databricks_sql.DatabricksSqlOperator.__init__"></a>

#### \_\_init\_\_

