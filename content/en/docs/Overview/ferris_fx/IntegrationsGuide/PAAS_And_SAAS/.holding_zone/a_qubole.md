---
title: "qubole"
linkTitle: "qubole"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     qubole Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.qubole"></a>

# sensors.qubole

<a id="sensors.qubole.QuboleSensor"></a>

## QuboleSensor Objects

```python
class QuboleSensor(BaseSensorOperator)
```

Base class for all Qubole Sensors

<a id="sensors.qubole.QuboleFileSensor"></a>

## QuboleFileSensor Objects

```python
class QuboleFileSensor(QuboleSensor)
```

Wait for a file or folder to be present in cloud storage

and check for its presence via QDS APIs

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/operator:QuboleFileSensor`

**Arguments**:

- `qubole_conn_id`: Connection id which consists of qds auth_token
- `data`: a JSON object containing payload, whose presence needs to be checked
Check this `example <https://github.com/apache/airflow/blob/main\
    /airflow/providers/qubole/example_dags/example_qubole_sensor.py>`_ for sample payload
    structure.

.. note:: Both ``data`` and ``qubole_conn_id`` fields support templating. You can
    also use ``.txt`` files for template-driven use cases.

<a id="sensors.qubole.QubolePartitionSensor"></a>

## QubolePartitionSensor Objects

```python
class QubolePartitionSensor(QuboleSensor)
```

Wait for a Hive partition to show up in QHS (Qubole Hive Service)

and check for its presence via QDS APIs

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/operator:QubolePartitionSensor`

**Arguments**:

- `qubole_conn_id`: Connection id which consists of qds auth_token
- `data`: a JSON object containing payload, whose presence needs to be checked.
Check this `example <https://github.com/apache/airflow/blob/main\
    /airflow/providers/qubole/example_dags/example_qubole_sensor.py>`_ for sample payload
    structure.

.. note:: Both ``data`` and ``qubole_conn_id`` fields support templating. You can
    also use ``.txt`` files for template-driven use cases.

<a id="operators"></a>

# operators

<a id="operators.qubole"></a>

# operators.qubole

Qubole operator

<a id="operators.qubole.QDSLink"></a>

## QDSLink Objects

```python
class QDSLink(BaseOperatorLink)
```

Link to QDS

<a id="operators.qubole.QDSLink.get_link"></a>

#### get\_link

```python
def get_link(operator: "AbstractOperator",
             dttm: Optional[datetime] = None,
             *,
             ti_key: Optional["TaskInstanceKey"] = None) -> str
```

Get link to qubole command result page.

**Arguments**:

- `operator`: operator
- `dttm`: datetime

**Returns**:

url link

<a id="operators.qubole.QuboleOperator"></a>

## QuboleOperator Objects

```python
class QuboleOperator(BaseOperator)
```

Execute tasks (commands) on QDS (https://qubole.com).

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:QuboleOperator`

**Arguments**:

- `qubole_conn_id`: Connection id which consists of qds auth_token
kwargs:
    :command_type: type of command to be executed, e.g. hivecmd, shellcmd, hadoopcmd
    :tags: array of tags to be assigned with the command
    :cluster_label: cluster label on which the command will be executed
    :name: name to be given to command
    :notify: whether to send email on command completion or not (default is False)

    **Arguments specific to command types**

    hivecmd:
        :query: inline query statement
        :script_location: s3 location containing query statement
        :sample_size: size of sample in bytes on which to run query
        :macros: macro values which were used in query
        :sample_size: size of sample in bytes on which to run query
        :hive-version: Specifies the hive version to be used. eg: 0.13,1.2,etc.
    prestocmd:
        :query: inline query statement
        :script_location: s3 location containing query statement
        :macros: macro values which were used in query
    hadoopcmd:
        :sub_commnad: must be one these ["jar", "s3distcp", "streaming"] followed by
            1 or more args
    shellcmd:
        :script: inline command with args
        :script_location: s3 location containing query statement
        :files: list of files in s3 bucket as file1,file2 format. These files will be
            copied into the working directory where the qubole command is being
            executed.
        :archives: list of archives in s3 bucket as archive1,archive2 format. These
            will be unarchived into the working directory where the qubole command is
            being executed
        :parameters: any extra args which need to be passed to script (only when
            script_location is supplied)
    pigcmd:
        :script: inline query statement (latin_statements)
        :script_location: s3 location containing pig query
        :parameters: any extra args which need to be passed to script (only when
            script_location is supplied
    sparkcmd:
        :program: the complete Spark Program in Scala, R, or Python
        :cmdline: spark-submit command line, all required arguments must be specify
            in cmdline itself.
        :sql: inline sql query
        :script_location: s3 location containing query statement
        :language: language of the program, Scala, R, or Python
        :app_id: ID of an Spark job server app
        :arguments: spark-submit command line arguments.
            If `cmdline` is selected, this should not be used because all
            required arguments and configurations are to be passed in the `cmdline` itself.
        :user_program_arguments: arguments that the user program takes in
        :macros: macro values which were used in query
        :note_id: Id of the Notebook to run
    dbtapquerycmd:
        :db_tap_id: data store ID of the target database, in Qubole.
        :query: inline query statement
        :macros: macro values which were used in query
    dbexportcmd:
        :mode: Can be 1 for Hive export or 2 for HDFS/S3 export
        :schema: Db schema name assumed accordingly by database if not specified
        :hive_table: Name of the hive table
        :partition_spec: partition specification for Hive table.
        :dbtap_id: data store ID of the target database, in Qubole.
        :db_table: name of the db table
        :db_update_mode: allowinsert or updateonly
        :db_update_keys: columns used to determine the uniqueness of rows
        :export_dir: HDFS/S3 location from which data will be exported.
        :fields_terminated_by: hex of the char used as column separator in the dataset
        :use_customer_cluster: To use cluster to run command
        :customer_cluster_label: the label of the cluster to run the command on
        :additional_options: Additional Sqoop options which are needed enclose options in
            double or single quotes e.g. '--map-column-hive id=int,data=string'
    dbimportcmd:
        :mode: 1 (simple), 2 (advance)
        :hive_table: Name of the hive table
        :schema: Db schema name assumed accordingly by database if not specified
        :hive_serde: Output format of the Hive Table
        :dbtap_id: data store ID of the target database, in Qubole.
        :db_table: name of the db table
        :where_clause: where clause, if any
        :parallelism: number of parallel db connections to use for extracting data
        :extract_query: SQL query to extract data from db. $CONDITIONS must be part
            of the where clause.
        :boundary_query: Query to be used get range of row IDs to be extracted
        :split_column: Column used as row ID to split data into ranges (mode 2)
        :use_customer_cluster: To use cluster to run command
        :customer_cluster_label: the label of the cluster to run the command on
        :additional_options: Additional Sqoop options which are needed enclose options in
            double or single quotes
    jupytercmd:
        :path: Path including name of the Jupyter notebook to be run with extension.
        :arguments: Valid JSON to be sent to the notebook. Specify the parameters in notebooks and pass
            the parameter value using the JSON format. key is the parameter’s name and value is
            the parameter’s value. Supported types in parameters are string, integer, float and boolean.

.. note:

    Following fields are template-supported : ``query``, ``script_location``,
    ``sub_command``, ``script``, ``files``, ``archives``, ``program``, ``cmdline``,
    ``sql``, ``where_clause``, ``extract_query``, ``boundary_query``, ``macros``,
    ``tags``, ``name``, ``parameters``, ``dbtap_id``, ``hive_table``, ``db_table``,
    ``split_column``, ``note_id``, ``db_update_keys``, ``export_dir``,
    ``partition_spec``, ``qubole_conn_id``, ``arguments``, ``user_program_arguments``.
    You can also use ``.txt`` files for template driven use cases.

.. note:

    In QuboleOperator there is a default handler for task failures and retries,
    which generally kills the command running at QDS for the corresponding task
    instance. You can override this behavior by providing your own failure and retry
    handler in task definition.

<a id="operators.qubole.QuboleOperator.get_results"></a>

#### get\_results

```python
def get_results(ti=None,
                fp=None,
                inline: bool = True,
                delim=None,
                fetch: bool = True,
                include_headers: bool = False) -> str
```

get_results from Qubole

<a id="operators.qubole.QuboleOperator.get_log"></a>

#### get\_log

```python
def get_log(ti) -> None
```

get_log from Qubole

<a id="operators.qubole.QuboleOperator.get_jobs_id"></a>

#### get\_jobs\_id

```python
def get_jobs_id(ti) -> None
```

Get jobs_id from Qubole

<a id="operators.qubole.QuboleOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> QuboleHook
```

Reinitialising the hook, as some template fields might have changed

<a id="operators.qubole_check"></a>

# operators.qubole\_check

<a id="operators.qubole_check._QuboleCheckOperatorMixin"></a>

## \_QuboleCheckOperatorMixin Objects

```python
class _QuboleCheckOperatorMixin()
```

This is a Mixin for Qubole related check operators

<a id="operators.qubole_check._QuboleCheckOperatorMixin.execute"></a>

#### execute

```python
def execute(context=None) -> None
```

Execute a check operation against Qubole

<a id="operators.qubole_check._QuboleCheckOperatorMixin.get_db_hook"></a>

#### get\_db\_hook

```python
def get_db_hook() -> QuboleCheckHook
```

Get QuboleCheckHook

<a id="operators.qubole_check._QuboleCheckOperatorMixin.get_hook"></a>

#### get\_hook

```python
def get_hook() -> QuboleCheckHook
```

Reinitialising the hook, as some template fields might have changed
This method overwrites the original QuboleOperator.get_hook() which returns a QuboleHook.

<a id="operators.qubole_check.QuboleCheckOperator"></a>

## QuboleCheckOperator Objects

```python
class QuboleCheckOperator(_QuboleCheckOperatorMixin, SQLCheckOperator,
                          QuboleOperator)
```

Performs checks against Qubole Commands. ``QuboleCheckOperator`` expects

a command that will be executed on QDS.
By default, each value on first row of the result of this Qubole Command
is evaluated using python ``bool`` casting. If any of the
values return ``False``, the check is failed and errors out.

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

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:QuboleCheckOperator`

**Arguments**:

- `qubole_conn_id`: Connection id which consists of qds auth_token
kwargs:

    Arguments specific to Qubole command can be referred from QuboleOperator docs.

    :results_parser_callable: This is an optional parameter to
        extend the flexibility of parsing the results of Qubole
        command to the users. This is a python callable which
        can hold the logic to parse list of rows returned by Qubole command.
        By default, only the values on first row are used for performing checks.
        This callable should return a list of records on
        which the checks have to be performed.

.. note:: All fields in common with template fields of
    QuboleOperator and SQLCheckOperator are template-supported.

<a id="operators.qubole_check.QuboleValueCheckOperator"></a>

## QuboleValueCheckOperator Objects

```python
class QuboleValueCheckOperator(_QuboleCheckOperatorMixin,
                               SQLValueCheckOperator, QuboleOperator)
```

Performs a simple value check using Qubole command.

By default, each value on the first row of this
Qubole command is compared with a pre-defined value.
The check fails and errors out if the output of the command
is not within the permissible limit of expected value.

**Arguments**:

- `qubole_conn_id`: Connection id which consists of qds auth_token
- `pass_value`: Expected value of the query results.
- `tolerance`: Defines the permissible pass_value range, for example if
tolerance is 2, the Qubole command output can be anything between
    -2*pass_value and 2*pass_value, without the operator erring out.



kwargs:

    Arguments specific to Qubole command can be referred from QuboleOperator docs.

    :results_parser_callable: This is an optional parameter to
        extend the flexibility of parsing the results of Qubole
        command to the users. This is a python callable which
        can hold the logic to parse list of rows returned by Qubole command.
        By default, only the values on first row are used for performing checks.
        This callable should return a list of records on
        which the checks have to be performed.


.. note:: All fields in common with template fields of
        QuboleOperator and SQLValueCheckOperator are template-supported.

<a id="operators.qubole_check.get_sql_from_qbol_cmd"></a>

#### get\_sql\_from\_qbol\_cmd

```python
def get_sql_from_qbol_cmd(params) -> str
```

Get Qubole sql from Qubole command

<a id="operators.qubole_check.handle_airflow_exception"></a>

#### handle\_airflow\_exception

```python
def handle_airflow_exception(airflow_exception, hook: QuboleCheckHook)
```

Qubole check handle Airflow exception

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_qubole"></a>

# example\_dags.example\_qubole

<a id="hooks"></a>

# hooks

<a id="hooks.qubole"></a>

# hooks.qubole

Qubole hook

<a id="hooks.qubole.flatten_list"></a>

#### flatten\_list

```python
def flatten_list(list_of_lists) -> list
```

Flatten the list

<a id="hooks.qubole.filter_options"></a>

#### filter\_options

```python
def filter_options(options: list) -> list
```

Remove options from the list

<a id="hooks.qubole.get_options_list"></a>

#### get\_options\_list

```python
def get_options_list(command_class) -> list
```

Get options list

<a id="hooks.qubole.build_command_args"></a>

#### build\_command\_args

```python
def build_command_args() -> Tuple[Dict[str, list], list]
```

Build Command argument from command and options

<a id="hooks.qubole.QuboleHook"></a>

## QuboleHook Objects

```python
class QuboleHook(BaseHook)
```

Hook for Qubole communication

<a id="hooks.qubole.QuboleHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.qubole.QuboleHook.handle_failure_retry"></a>

#### handle\_failure\_retry

```python
@staticmethod
def handle_failure_retry(context) -> None
```

Handle retries in case of failures

<a id="hooks.qubole.QuboleHook.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Execute call

<a id="hooks.qubole.QuboleHook.kill"></a>

#### kill

```python
def kill(ti)
```

Kill (cancel) a Qubole command

**Arguments**:

- `ti`: Task Instance of the dag, used to determine the Quboles command id

**Returns**:

response from Qubole

<a id="hooks.qubole.QuboleHook.get_results"></a>

#### get\_results

```python
def get_results(ti=None,
                fp=None,
                inline: bool = True,
                delim=None,
                fetch: bool = True,
                include_headers: bool = False) -> str
```

Get results (or just s3 locations) of a command from Qubole and save into a file

**Arguments**:

- `ti`: Task Instance of the dag, used to determine the Quboles command id
- `fp`: Optional file pointer, will create one and return if None passed
- `inline`: True to download actual results, False to get s3 locations only
- `delim`: Replaces the CTL-A chars with the given delim, defaults to ','
- `fetch`: when inline is True, get results directly from s3 (if large)

**Returns**:

file location containing actual results or s3 locations of results

<a id="hooks.qubole.QuboleHook.get_log"></a>

#### get\_log

```python
def get_log(ti) -> None
```

Get Logs of a command from Qubole

**Arguments**:

- `ti`: Task Instance of the dag, used to determine the Quboles command id

**Returns**:

command log as text

<a id="hooks.qubole.QuboleHook.get_jobs_id"></a>

#### get\_jobs\_id

```python
def get_jobs_id(ti) -> None
```

Get jobs associated with a Qubole commands

**Arguments**:

- `ti`: Task Instance of the dag, used to determine the Quboles command id

**Returns**:

Job information associated with command

<a id="hooks.qubole.QuboleHook.create_cmd_args"></a>

#### create\_cmd\_args

```python
def create_cmd_args(context) -> List[str]
```

Creates command arguments

<a id="hooks.qubole_check"></a>

# hooks.qubole\_check

<a id="hooks.qubole_check.isint"></a>

#### isint

```python
def isint(value) -> bool
```

Whether Qubole column are integer

<a id="hooks.qubole_check.isfloat"></a>

#### isfloat

```python
def isfloat(value) -> bool
```

Whether Qubole column are float

<a id="hooks.qubole_check.isbool"></a>

#### isbool

```python
def isbool(value) -> bool
```

Whether Qubole column are boolean

<a id="hooks.qubole_check.parse_first_row"></a>

#### parse\_first\_row

```python
def parse_first_row(row_list) -> List[Union[bool, float, int, str]]
```

Parse Qubole first record list

<a id="hooks.qubole_check.QuboleCheckHook"></a>

## QuboleCheckHook Objects

```python
class QuboleCheckHook(QuboleHook, DbApiHook)
```

Qubole check hook

<a id="hooks.qubole_check.QuboleCheckHook.get_first"></a>

#### get\_first

```python
def get_first(sql)
```

Get Qubole query first record list

<a id="hooks.qubole_check.QuboleCheckHook.get_query_results"></a>

#### get\_query\_results

```python
def get_query_results() -> Optional[str]
```

Get Qubole query result

