---
title: "apache"
linkTitle: "apache"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     apache Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="drill"></a>

# drill

<a id="drill.operators"></a>

# drill.operators

<a id="drill.operators.drill"></a>

# drill.operators.drill

<a id="drill.operators.drill.DrillOperator"></a>

## DrillOperator Objects

```python
class DrillOperator(BaseOperator)
```

Executes the provided SQL in the identified Drill environment.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:DrillOperator`

**Arguments**:

- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
Template references are recognized by str ending in '.sql'
- `drill_conn_id`: id of the connection config for the target Drill
environment
- `parameters`: (optional) the parameters to render the SQL query with.

<a id="drill.example_dags"></a>

# drill.example\_dags

<a id="drill.example_dags.example_drill_dag"></a>

# drill.example\_dags.example\_drill\_dag

Example Airflow DAG to execute SQL in an Apache Drill environment using the `DrillOperator`.

<a id="drill.hooks"></a>

# drill.hooks

<a id="drill.hooks.drill"></a>

# drill.hooks.drill

<a id="drill.hooks.drill.DrillHook"></a>

## DrillHook Objects

```python
class DrillHook(DbApiHook)
```

Interact with Apache Drill via sqlalchemy-drill.

You can specify the SQLAlchemy dialect and driver that sqlalchemy-drill
will employ to communicate with Drill in the extras field of your
connection, e.g. ``{"dialect_driver": "drill+sadrill"}`` for communication
over Drill's REST API.  See the sqlalchemy-drill documentation for
descriptions of the supported dialects and drivers.

You can specify the default storage_plugin for the sqlalchemy-drill
connection using the extras field e.g. ``{"storage_plugin": "dfs"}``.

<a id="drill.hooks.drill.DrillHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Connection
```

Establish a connection to Drillbit.

<a id="drill.hooks.drill.DrillHook.get_uri"></a>

#### get\_uri

```python
def get_uri() -> str
```

Returns the connection URI

e.g: ``drill://localhost:8047/dfs``

<a id="pig"></a>

# pig

<a id="pig.operators"></a>

# pig.operators

<a id="pig.operators.pig"></a>

# pig.operators.pig

<a id="pig.operators.pig.PigOperator"></a>

## PigOperator Objects

```python
class PigOperator(BaseOperator)
```

Executes pig script.

**Arguments**:

- `pig`: the pig latin script to be executed. (templated)
- `pig_cli_conn_id`: reference to the Hive database
- `pigparams_jinja_translate`: when True, pig params-type templating
${var} gets translated into jinja-type templating {{ var }}. Note that
you may want to use this along with the
``DAG(user_defined_macros=myargs)`` parameter. View the DAG
object documentation for more details.
- `pig_opts`: pig options, such as: -x tez, -useHCatalog, ...

<a id="pig.example_dags"></a>

# pig.example\_dags

<a id="pig.example_dags.example_pig"></a>

# pig.example\_dags.example\_pig

Example DAG demonstrating the usage of the PigOperator.

<a id="pig.hooks"></a>

# pig.hooks

<a id="pig.hooks.pig"></a>

# pig.hooks.pig

<a id="pig.hooks.pig.PigCliHook"></a>

## PigCliHook Objects

```python
class PigCliHook(BaseHook)
```

Simple wrapper around the pig CLI.

Note that you can also set default pig CLI properties using the
``pig_properties`` to be used in your connection as in
``{"pig_properties": "-Dpig.tmpfilecompression=true"}``

<a id="pig.hooks.pig.PigCliHook.run_cli"></a>

#### run\_cli

```python
def run_cli(pig: str,
            pig_opts: Optional[str] = None,
            verbose: bool = True) -> Any
```

Run an pig script using the pig cli

>>> ph = PigCliHook()
>>> result = ph.run_cli("ls /;", pig_opts="-x mapreduce")
>>> ("hdfs://" in result)
True

<a id="pig.hooks.pig.PigCliHook.kill"></a>

#### kill

```python
def kill() -> None
```

Kill Pig job

<a id="pinot"></a>

# pinot

<a id="pinot.hooks"></a>

# pinot.hooks

<a id="pinot.hooks.pinot"></a>

# pinot.hooks.pinot

<a id="pinot.hooks.pinot.PinotAdminHook"></a>

## PinotAdminHook Objects

```python
class PinotAdminHook(BaseHook)
```

This hook is a wrapper around the pinot-admin.sh script.

For now, only small subset of its subcommands are implemented,
which are required to ingest offline data into Apache Pinot
(i.e., AddSchema, AddTable, CreateSegment, and UploadSegment).
Their command options are based on Pinot v0.1.0.

Unfortunately, as of v0.1.0, pinot-admin.sh always exits with
status code 0. To address this behavior, users can use the
pinot_admin_system_exit flag. If its value is set to false,
this hook evaluates the result based on the output message
instead of the status code. This Pinot's behavior is supposed
to be improved in the next release, which will include the
following PR: https://github.com/apache/incubator-pinot/pull/4110

**Arguments**:

- `conn_id`: The name of the connection to use.
- `cmd_path`: The filepath to the pinot-admin.sh executable
- `pinot_admin_system_exit`: If true, the result is evaluated based on the status code.
Otherwise, the result is evaluated as a failure if "Error" or
"Exception" is in the output message.

<a id="pinot.hooks.pinot.PinotAdminHook.add_schema"></a>

#### add\_schema

```python
def add_schema(schema_file: str, with_exec: bool = True) -> Any
```

Add Pinot schema by run AddSchema command

**Arguments**:

- `schema_file`: Pinot schema file
- `with_exec`: bool

<a id="pinot.hooks.pinot.PinotAdminHook.add_table"></a>

#### add\_table

```python
def add_table(file_path: str, with_exec: bool = True) -> Any
```

Add Pinot table with run AddTable command

**Arguments**:

- `file_path`: Pinot table configure file
- `with_exec`: bool

<a id="pinot.hooks.pinot.PinotAdminHook.create_segment"></a>

#### create\_segment

```python
def create_segment(generator_config_file: Optional[str] = None,
                   data_dir: Optional[str] = None,
                   segment_format: Optional[str] = None,
                   out_dir: Optional[str] = None,
                   overwrite: Optional[str] = None,
                   table_name: Optional[str] = None,
                   segment_name: Optional[str] = None,
                   time_column_name: Optional[str] = None,
                   schema_file: Optional[str] = None,
                   reader_config_file: Optional[str] = None,
                   enable_star_tree_index: Optional[str] = None,
                   star_tree_index_spec_file: Optional[str] = None,
                   hll_size: Optional[str] = None,
                   hll_columns: Optional[str] = None,
                   hll_suffix: Optional[str] = None,
                   num_threads: Optional[str] = None,
                   post_creation_verification: Optional[str] = None,
                   retry: Optional[str] = None) -> Any
```

Create Pinot segment by run CreateSegment command

<a id="pinot.hooks.pinot.PinotAdminHook.upload_segment"></a>

#### upload\_segment

```python
def upload_segment(segment_dir: str, table_name: Optional[str] = None) -> Any
```

Upload Segment with run UploadSegment command

**Arguments**:

- `segment_dir`: 
- `table_name`: 

<a id="pinot.hooks.pinot.PinotAdminHook.run_cli"></a>

#### run\_cli

```python
def run_cli(cmd: List[str], verbose: bool = True) -> str
```

Run command with pinot-admin.sh

**Arguments**:

- `cmd`: List of command going to be run by pinot-admin.sh script
- `verbose`: 

<a id="pinot.hooks.pinot.PinotDbApiHook"></a>

## PinotDbApiHook Objects

```python
class PinotDbApiHook(DbApiHook)
```

Interact with Pinot Broker Query API

This hook uses standard-SQL endpoint since PQL endpoint is soon to be deprecated.
https://docs.pinot.apache.org/users/api/querying-pinot-using-standard-sql

<a id="pinot.hooks.pinot.PinotDbApiHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Any
```

Establish a connection to pinot broker through pinot dbapi.

<a id="pinot.hooks.pinot.PinotDbApiHook.get_uri"></a>

#### get\_uri

```python
def get_uri() -> str
```

Get the connection uri for pinot broker.

e.g: http://localhost:9000/query/sql

<a id="pinot.hooks.pinot.PinotDbApiHook.get_records"></a>

#### get\_records

```python
def get_records(
        sql: str,
        parameters: Optional[Union[Dict[str, Any],
                                   Iterable[Any]]] = None) -> Any
```

Executes the sql and returns a set of records.

**Arguments**:

- `sql`: the sql statement to be executed (str) or a list of
sql statements to execute
- `parameters`: The parameters to render the SQL query with.

<a id="pinot.hooks.pinot.PinotDbApiHook.get_first"></a>

#### get\_first

```python
def get_first(
        sql: str,
        parameters: Optional[Union[Dict[str, Any],
                                   Iterable[Any]]] = None) -> Any
```

Executes the sql and returns the first resulting row.

**Arguments**:

- `sql`: the sql statement to be executed (str) or a list of
sql statements to execute
- `parameters`: The parameters to render the SQL query with.

<a id="kylin"></a>

# kylin

<a id="kylin.operators.kylin_cube"></a>

# kylin.operators.kylin\_cube

<a id="kylin.operators.kylin_cube.KylinCubeOperator"></a>

## KylinCubeOperator Objects

```python
class KylinCubeOperator(BaseOperator)
```

This operator is used to submit request about kylin build/refresh/merge,

and can track job status . so users can easier to build kylin job

For more detail information in
`Apache Kylin <http://kylin.apache.org/>`_

**Arguments**:

- `kylin_conn_id`: The connection id as configured in Airflow administration.
- `project`: kylin project name, this param will overwrite the project in kylin_conn_id:
- `cube`: kylin cube name
- `dsn`: (dsn , dsn url of kylin connection ,which will overwrite kylin_conn_id.
for example: kylin://ADMIN:KYLIN@sandbox/learn_kylin?timeout=60&is_debug=1)
- `command`: (kylin command include 'build', 'merge', 'refresh', 'delete',
'build_streaming', 'merge_streaming', 'refresh_streaming', 'disable', 'enable',
'purge', 'clone', 'drop'.
build - use /kylin/api/cubes/{cubeName}/build rest api,and buildType is ‘BUILD’,
and you should give start_time and end_time
refresh - use build rest api,and buildType is ‘REFRESH’
merge - use build rest api,and buildType is ‘MERGE’
build_streaming - use /kylin/api/cubes/{cubeName}/build2 rest api,and buildType is ‘BUILD’
and you should give offset_start and offset_end
refresh_streaming - use build2 rest api,and buildType is ‘REFRESH’
merge_streaming - use build2 rest api,and buildType is ‘MERGE’
delete - delete segment, and you should give segment_name value
disable - disable cube
enable - enable cube
purge - purge cube
clone - clone cube,new cube name is {cube_name}_clone
drop - drop cube)
- `start_time`: build segment start time
- `end_time`: build segment end time
- `offset_start`: streaming build segment start time
- `offset_end`: streaming build segment end time
- `segment_name`: segment name
- `is_track_job`: (whether to track job status. if value is True,will track job until
job status is in("FINISHED", "ERROR", "DISCARDED", "KILLED", "SUICIDAL",
"STOPPED") or timeout)
- `interval`: track job status,default value is 60s
- `timeout`: timeout value,default value is 1 day,60 * 60 * 24 s
- `eager_error_status`: (jobs error status,if job status in this list ,this task will be error.
default value is tuple(["ERROR", "DISCARDED", "KILLED", "SUICIDAL", "STOPPED"]))

<a id="kylin.operators"></a>

# kylin.operators

<a id="kylin.example_dags"></a>

# kylin.example\_dags

<a id="kylin.example_dags.example_kylin_dag"></a>

# kylin.example\_dags.example\_kylin\_dag

This is an example DAG which uses the KylinCubeOperator.
The tasks below include kylin build, refresh, merge operation.

<a id="kylin.example_dags.example_kylin_dag.gen_build_time"></a>

#### gen\_build\_time

```python
@dag.task
def gen_build_time()
```

Gen build time and push to XCom (with key of "return_value")

**Returns**:

A dict with build time values.

<a id="kylin.hooks"></a>

# kylin.hooks

<a id="kylin.hooks.kylin"></a>

# kylin.hooks.kylin

<a id="kylin.hooks.kylin.KylinHook"></a>

## KylinHook Objects

```python
class KylinHook(BaseHook)
```

Interact with Kylin to run CubeSource commands and get job status.

**Arguments**:

- `kylin_conn_id`: The connection id as configured in Airflow administration.
- `project`: project name
- `dsn`: dsn

<a id="kylin.hooks.kylin.KylinHook.cube_run"></a>

#### cube\_run

```python
def cube_run(datasource_name, op, **op_args)
```

Run CubeSource command which in CubeSource.support_invoke_command

**Arguments**:

- `datasource_name`: 
- `op`: command
- `op_args`: command args

**Returns**:

response

<a id="kylin.hooks.kylin.KylinHook.get_job_status"></a>

#### get\_job\_status

```python
def get_job_status(job_id)
```

Get job status

**Arguments**:

- `job_id`: kylin job id

**Returns**:

job status

<a id="sqoop"></a>

# sqoop

<a id="sqoop.operators.sqoop"></a>

# sqoop.operators.sqoop

This module contains a sqoop 1 operator

<a id="sqoop.operators.sqoop.SqoopOperator"></a>

## SqoopOperator Objects

```python
class SqoopOperator(BaseOperator)
```

Execute a Sqoop job.

Documentation for Apache Sqoop can be found here:
https://sqoop.apache.org/docs/1.4.2/SqoopUserGuide.html

**Arguments**:

- `conn_id`: str
- `cmd_type`: str specify command to execute "export" or "import"
- `schema`: Schema name
- `table`: Table to read
- `query`: Import result of arbitrary SQL query. Instead of using the table,
columns and where arguments, you can specify a SQL statement with the query
argument. Must also specify a destination directory with target_dir.
- `target_dir`: HDFS destination directory where the data
from the rdbms will be written
- `append`: Append data to an existing dataset in HDFS
- `file_type`: "avro", "sequence", "text" Imports data to
into the specified format. Defaults to text.
- `columns`: <col,col,col> Columns to import from table
- `num_mappers`: Use n mapper tasks to import/export in parallel
- `split_by`: Column of the table used to split work units
- `where`: WHERE clause to use during import
- `export_dir`: HDFS Hive database directory to export to the rdbms
- `input_null_string`: The string to be interpreted as null
for string columns
- `input_null_non_string`: The string to be interpreted as null
for non-string columns
- `staging_table`: The table in which data will be staged before
being inserted into the destination table
- `clear_staging_table`: Indicate that any data present in the
staging table can be deleted
- `enclosed_by`: Sets a required field enclosing character
- `escaped_by`: Sets the escape character
- `input_fields_terminated_by`: Sets the input field separator
- `input_lines_terminated_by`: Sets the input end-of-line character
- `input_optionally_enclosed_by`: Sets a field enclosing character
- `batch`: Use batch mode for underlying statement execution
- `direct`: Use direct export fast path
- `driver`: Manually specify JDBC driver class to use
- `verbose`: Switch to more verbose logging for debug purposes
- `relaxed_isolation`: use read uncommitted isolation level
- `hcatalog_database`: Specifies the database name for the HCatalog table
- `hcatalog_table`: The argument value for this option is the HCatalog table
- `create_hcatalog_table`: Have sqoop create the hcatalog table passed
in or not
- `properties`: additional JVM properties passed to sqoop
- `extra_import_options`: Extra import options to pass as dict.
If a key doesn't have a value, just pass an empty string to it.
Don't include prefix of -- for sqoop options.
- `extra_export_options`: Extra export options to pass as dict.
If a key doesn't have a value, just pass an empty string to it.
Don't include prefix of -- for sqoop options.

<a id="sqoop.operators.sqoop.SqoopOperator.execute"></a>

#### execute

```python
def execute(context: "Context") -> None
```

Execute sqoop job

<a id="sqoop.operators"></a>

# sqoop.operators

<a id="sqoop.hooks.sqoop"></a>

# sqoop.hooks.sqoop

This module contains a sqoop 1.x hook

<a id="sqoop.hooks.sqoop.SqoopHook"></a>

## SqoopHook Objects

```python
class SqoopHook(BaseHook)
```

This hook is a wrapper around the sqoop 1 binary. To be able to use the hook

it is required that "sqoop" is in the PATH.

Additional arguments that can be passed via the 'extra' JSON field of the
sqoop connection:

    * ``job_tracker``: Job tracker local|jobtracker:port.
    * ``namenode``: Namenode.
    * ``lib_jars``: Comma separated jar files to include in the classpath.
    * ``files``: Comma separated files to be copied to the map reduce cluster.
    * ``archives``: Comma separated archives to be unarchived on the compute
        machines.
    * ``password_file``: Path to file containing the password.

**Arguments**:

- `conn_id`: Reference to the sqoop connection.
- `verbose`: Set sqoop to verbose.
- `num_mappers`: Number of map tasks to import in parallel.
- `properties`: Properties to set via the -D argument

<a id="sqoop.hooks.sqoop.SqoopHook.cmd_mask_password"></a>

#### cmd\_mask\_password

```python
def cmd_mask_password(cmd_orig: List[str]) -> List[str]
```

Mask command password for safety

<a id="sqoop.hooks.sqoop.SqoopHook.popen"></a>

#### popen

```python
def popen(cmd: List[str], **kwargs: Any) -> None
```

Remote Popen

**Arguments**:

- `cmd`: command to remotely execute
- `kwargs`: extra arguments to Popen (see subprocess.Popen)

**Returns**:

handle to subprocess

<a id="sqoop.hooks.sqoop.SqoopHook.import_table"></a>

#### import\_table

```python
def import_table(table: str,
                 target_dir: Optional[str] = None,
                 append: bool = False,
                 file_type: str = "text",
                 columns: Optional[str] = None,
                 split_by: Optional[str] = None,
                 where: Optional[str] = None,
                 direct: bool = False,
                 driver: Any = None,
                 extra_import_options: Optional[Dict[str, Any]] = None,
                 schema: Optional[str] = None) -> Any
```

Imports table from remote location to target dir. Arguments are

copies of direct sqoop command line arguments

**Arguments**:

- `table`: Table to read
- `schema`: Schema name
- `target_dir`: HDFS destination dir
- `append`: Append data to an existing dataset in HDFS
- `file_type`: "avro", "sequence", "text" or "parquet".
Imports data to into the specified format. Defaults to text.
- `columns`: <col,col,col…> Columns to import from table
- `split_by`: Column of the table used to split work units
- `where`: WHERE clause to use during import
- `direct`: Use direct connector if exists for the database
- `driver`: Manually specify JDBC driver class to use
- `extra_import_options`: Extra import options to pass as dict.
If a key doesn't have a value, just pass an empty string to it.
Don't include prefix of -- for sqoop options.

<a id="sqoop.hooks.sqoop.SqoopHook.import_query"></a>

#### import\_query

```python
def import_query(query: str,
                 target_dir: Optional[str] = None,
                 append: bool = False,
                 file_type: str = "text",
                 split_by: Optional[str] = None,
                 direct: Optional[bool] = None,
                 driver: Optional[Any] = None,
                 extra_import_options: Optional[Dict[str, Any]] = None) -> Any
```

Imports a specific query from the rdbms to hdfs

**Arguments**:

- `query`: Free format query to run
- `target_dir`: HDFS destination dir
- `append`: Append data to an existing dataset in HDFS
- `file_type`: "avro", "sequence", "text" or "parquet"
Imports data to hdfs into the specified format. Defaults to text.
- `split_by`: Column of the table used to split work units
- `direct`: Use direct import fast path
- `driver`: Manually specify JDBC driver class to use
- `extra_import_options`: Extra import options to pass as dict.
If a key doesn't have a value, just pass an empty string to it.
Don't include prefix of -- for sqoop options.

<a id="sqoop.hooks.sqoop.SqoopHook.export_table"></a>

#### export\_table

```python
def export_table(table: str,
                 export_dir: Optional[str] = None,
                 input_null_string: Optional[str] = None,
                 input_null_non_string: Optional[str] = None,
                 staging_table: Optional[str] = None,
                 clear_staging_table: bool = False,
                 enclosed_by: Optional[str] = None,
                 escaped_by: Optional[str] = None,
                 input_fields_terminated_by: Optional[str] = None,
                 input_lines_terminated_by: Optional[str] = None,
                 input_optionally_enclosed_by: Optional[str] = None,
                 batch: bool = False,
                 relaxed_isolation: bool = False,
                 extra_export_options: Optional[Dict[str, Any]] = None,
                 schema: Optional[str] = None) -> None
```

Exports Hive table to remote location. Arguments are copies of direct

sqoop command line Arguments

**Arguments**:

- `table`: Table remote destination
- `schema`: Schema name
- `export_dir`: Hive table to export
- `input_null_string`: The string to be interpreted as null for
string columns
- `input_null_non_string`: The string to be interpreted as null
for non-string columns
- `staging_table`: The table in which data will be staged before
being inserted into the destination table
- `clear_staging_table`: Indicate that any data present in the
staging table can be deleted
- `enclosed_by`: Sets a required field enclosing character
- `escaped_by`: Sets the escape character
- `input_fields_terminated_by`: Sets the field separator character
- `input_lines_terminated_by`: Sets the end-of-line character
- `input_optionally_enclosed_by`: Sets a field enclosing character
- `batch`: Use batch mode for underlying statement execution
- `relaxed_isolation`: Transaction isolation to read uncommitted
for the mappers
- `extra_export_options`: Extra export options to pass as dict.
If a key doesn't have a value, just pass an empty string to it.
Don't include prefix of -- for sqoop options.

<a id="sqoop.hooks"></a>

# sqoop.hooks

<a id="livy"></a>

# livy

<a id="livy.sensors"></a>

# livy.sensors

<a id="livy.sensors.livy"></a>

# livy.sensors.livy

This module contains the Apache Livy sensor.

<a id="livy.sensors.livy.LivySensor"></a>

## LivySensor Objects

```python
class LivySensor(BaseSensorOperator)
```

Monitor a Livy sessions for termination.

**Arguments**:

- `livy_conn_id`: reference to a pre-defined Livy connection
- `batch_id`: identifier of the monitored batch
depends on the option that's being modified.

<a id="livy.sensors.livy.LivySensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> LivyHook
```

Get valid hook.

**Returns**:

`LivyHook`: hook

<a id="livy.operators"></a>

# livy.operators

<a id="livy.operators.livy"></a>

# livy.operators.livy

This module contains the Apache Livy operator.

<a id="livy.operators.livy.LivyOperator"></a>

## LivyOperator Objects

```python
class LivyOperator(BaseOperator)
```

This operator wraps the Apache Livy batch REST API, allowing to submit a Spark

application to the underlying cluster.

**Arguments**:

- `file`: path of the file containing the application to execute (required).
- `class_name`: name of the application Java/Spark main class.
- `args`: application command line arguments.
- `jars`: jars to be used in this sessions.
- `py_files`: python files to be used in this session.
- `files`: files to be used in this session.
- `driver_memory`: amount of memory to use for the driver process.
- `driver_cores`: number of cores to use for the driver process.
- `executor_memory`: amount of memory to use per executor process.
- `executor_cores`: number of cores to use for each executor.
- `num_executors`: number of executors to launch for this session.
- `archives`: archives to be used in this session.
- `queue`: name of the YARN queue to which the application is submitted.
- `name`: name of this session.
- `conf`: Spark configuration properties.
- `proxy_user`: user to impersonate when running the job.
- `livy_conn_id`: reference to a pre-defined Livy Connection.
- `polling_interval`: time in seconds between polling for job completion. Don't poll for values >=0
- `extra_options`: A dictionary of options, where key is string and value
depends on the option that's being modified.
- `extra_headers`: A dictionary of headers passed to the HTTP request to livy.
- `retry_args`: Arguments which define the retry behaviour.
See Tenacity documentation at https://github.com/jd/tenacity

<a id="livy.operators.livy.LivyOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> LivyHook
```

Get valid hook.

**Returns**:

`LivyHook`: hook

<a id="livy.operators.livy.LivyOperator.poll_for_termination"></a>

#### poll\_for\_termination

```python
def poll_for_termination(batch_id: Union[int, str]) -> None
```

Pool Livy for batch termination.

**Arguments**:

- `batch_id`: id of the batch session to monitor.

<a id="livy.operators.livy.LivyOperator.kill"></a>

#### kill

```python
def kill() -> None
```

Delete the current batch session.

<a id="livy.example_dags"></a>

# livy.example\_dags

<a id="livy.example_dags.example_livy"></a>

# livy.example\_dags.example\_livy

This is an example DAG which uses the LivyOperator.
The tasks below trigger the computation of pi on the Spark instance
using the Java and Python executables provided in the example library.

<a id="livy.hooks"></a>

# livy.hooks

<a id="livy.hooks.livy"></a>

# livy.hooks.livy

This module contains the Apache Livy hook.

<a id="livy.hooks.livy.BatchState"></a>

## BatchState Objects

```python
class BatchState(Enum)
```

Batch session states

<a id="livy.hooks.livy.LivyHook"></a>

## LivyHook Objects

```python
class LivyHook(HttpHook, LoggingMixin)
```

Hook for Apache Livy through the REST API.

**Arguments**:

- `livy_conn_id`: reference to a pre-defined Livy Connection.
- `extra_options`: A dictionary of options passed to Livy.
- `extra_headers`: A dictionary of headers passed to the HTTP request to livy.
.. seealso::
    For more details refer to the Apache Livy API reference:
    https://livy.apache.org/docs/latest/rest-api.html

<a id="livy.hooks.livy.LivyHook.get_conn"></a>

#### get\_conn

```python
def get_conn(headers: Optional[Dict[str, Any]] = None) -> Any
```

Returns http session for use with requests

**Arguments**:

- `headers`: additional headers to be passed through as a dictionary

**Returns**:

`requests.Session`: requests session

<a id="livy.hooks.livy.LivyHook.run_method"></a>

#### run\_method

```python
def run_method(endpoint: str,
               method: str = 'GET',
               data: Optional[Any] = None,
               headers: Optional[Dict[str, Any]] = None,
               retry_args: Optional[Dict[str, Any]] = None) -> Any
```

Wrapper for HttpHook, allows to change method on the same HttpHook

**Arguments**:

- `method`: http method
- `endpoint`: endpoint
- `data`: request payload
- `headers`: headers
- `retry_args`: Arguments which define the retry behaviour.
See Tenacity documentation at https://github.com/jd/tenacity

**Returns**:

`requests.Response`: http response

<a id="livy.hooks.livy.LivyHook.post_batch"></a>

#### post\_batch

```python
def post_batch(*args: Any, **kwargs: Any) -> Any
```

Perform request to submit batch

**Returns**:

`int`: batch session id

<a id="livy.hooks.livy.LivyHook.get_batch"></a>

#### get\_batch

```python
def get_batch(session_id: Union[int, str]) -> Any
```

Fetch info about the specified batch

**Arguments**:

- `session_id`: identifier of the batch sessions

**Returns**:

`dict`: response body

<a id="livy.hooks.livy.LivyHook.get_batch_state"></a>

#### get\_batch\_state

```python
def get_batch_state(session_id: Union[int, str],
                    retry_args: Optional[Dict[str, Any]] = None) -> BatchState
```

Fetch the state of the specified batch

**Arguments**:

- `session_id`: identifier of the batch sessions
- `retry_args`: Arguments which define the retry behaviour.
See Tenacity documentation at https://github.com/jd/tenacity

**Returns**:

`BatchState`: batch state

<a id="livy.hooks.livy.LivyHook.delete_batch"></a>

#### delete\_batch

```python
def delete_batch(session_id: Union[int, str]) -> Any
```

Delete the specified batch

**Arguments**:

- `session_id`: identifier of the batch sessions

**Returns**:

`dict`: response body

<a id="livy.hooks.livy.LivyHook.get_batch_logs"></a>

#### get\_batch\_logs

```python
def get_batch_logs(session_id: Union[int, str], log_start_position,
                   log_batch_size) -> Any
```

Gets the session logs for a specified batch.

**Arguments**:

- `session_id`: identifier of the batch sessions
- `log_start_position`: Position from where to pull the logs
- `log_batch_size`: Number of lines to pull in one batch

**Returns**:

`dict`: response body

<a id="livy.hooks.livy.LivyHook.dump_batch_logs"></a>

#### dump\_batch\_logs

```python
def dump_batch_logs(session_id: Union[int, str]) -> Any
```

Dumps the session logs for a specified batch

**Arguments**:

- `session_id`: identifier of the batch sessions

**Returns**:

`dict`: response body

<a id="livy.hooks.livy.LivyHook.build_post_batch_body"></a>

#### build\_post\_batch\_body

```python
@staticmethod
def build_post_batch_body(file: str,
                          args: Optional[Sequence[Union[str, int,
                                                        float]]] = None,
                          class_name: Optional[str] = None,
                          jars: Optional[List[str]] = None,
                          py_files: Optional[List[str]] = None,
                          files: Optional[List[str]] = None,
                          archives: Optional[List[str]] = None,
                          name: Optional[str] = None,
                          driver_memory: Optional[str] = None,
                          driver_cores: Optional[Union[int, str]] = None,
                          executor_memory: Optional[str] = None,
                          executor_cores: Optional[int] = None,
                          num_executors: Optional[Union[int, str]] = None,
                          queue: Optional[str] = None,
                          proxy_user: Optional[str] = None,
                          conf: Optional[Dict[Any, Any]] = None) -> Any
```

Build the post batch request body.

For more information about the format refer to
.. seealso:: https://livy.apache.org/docs/latest/rest-api.html

**Arguments**:

- `file`: Path of the file containing the application to execute (required).
- `proxy_user`: User to impersonate when running the job.
- `class_name`: Application Java/Spark main class string.
- `args`: Command line arguments for the application s.
- `jars`: jars to be used in this sessions.
- `py_files`: Python files to be used in this session.
- `files`: files to be used in this session.
- `driver_memory`: Amount of memory to use for the driver process  string.
- `driver_cores`: Number of cores to use for the driver process int.
- `executor_memory`: Amount of memory to use per executor process  string.
- `executor_cores`: Number of cores to use for each executor  int.
- `num_executors`: Number of executors to launch for this session  int.
- `archives`: Archives to be used in this session.
- `queue`: The name of the YARN queue to which submitted string.
- `name`: The name of this session string.
- `conf`: Spark configuration properties.

**Returns**:

`dict`: request body

<a id="cassandra"></a>

# cassandra

<a id="cassandra.sensors"></a>

# cassandra.sensors

<a id="cassandra.sensors.record"></a>

# cassandra.sensors.record

This module contains sensor that check the existence
of a record in a Cassandra cluster.

<a id="cassandra.sensors.record.CassandraRecordSensor"></a>

## CassandraRecordSensor Objects

```python
class CassandraRecordSensor(BaseSensorOperator)
```

Checks for the existence of a record in a Cassandra cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:CassandraRecordSensor`

For example, if you want to wait for a record that has values 'v1' and 'v2' for each
primary keys 'p1' and 'p2' to be populated in keyspace 'k' and table 't',
instantiate it as follows:

>>> cassandra_sensor = CassandraRecordSensor(table="k.t",
...                                          keys={"p1": "v1", "p2": "v2"},
...                                          cassandra_conn_id="cassandra_default",
...                                          task_id="cassandra_sensor")

**Arguments**:

- `table`: Target Cassandra table.
Use dot notation to target a specific keyspace.
- `keys`: The keys and their values to be monitored
- `cassandra_conn_id`: The connection ID to use
when connecting to Cassandra cluster

<a id="cassandra.sensors.table"></a>

# cassandra.sensors.table

This module contains sensor that check the existence
of a table in a Cassandra cluster.

<a id="cassandra.sensors.table.CassandraTableSensor"></a>

## CassandraTableSensor Objects

```python
class CassandraTableSensor(BaseSensorOperator)
```

Checks for the existence of a table in a Cassandra cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:CassandraTableSensor`


For example, if you want to wait for a table called 't' to be created
in a keyspace 'k', instantiate it as follows:

>>> cassandra_sensor = CassandraTableSensor(table="k.t",
...                                         cassandra_conn_id="cassandra_default",
...                                         task_id="cassandra_sensor")

**Arguments**:

- `table`: Target Cassandra table.
Use dot notation to target a specific keyspace.
- `cassandra_conn_id`: The connection ID to use
when connecting to Cassandra cluster

<a id="cassandra.example_dags"></a>

# cassandra.example\_dags

<a id="cassandra.example_dags.example_cassandra_dag"></a>

# cassandra.example\_dags.example\_cassandra\_dag

Example Airflow DAG to check if a Cassandra Table and a Records exists
or not using `CassandraTableSensor` and `CassandraRecordSensor`.

<a id="cassandra.hooks.cassandra"></a>

# cassandra.hooks.cassandra

This module contains hook to integrate with Apache Cassandra.

<a id="cassandra.hooks.cassandra.CassandraHook"></a>

## CassandraHook Objects

```python
class CassandraHook(BaseHook, LoggingMixin)
```

Hook used to interact with Cassandra

Contact points can be specified as a comma-separated string in the 'hosts'
field of the connection.

Port can be specified in the port field of the connection.

If SSL is enabled in Cassandra, pass in a dict in the extra field as kwargs for
``ssl.wrap_socket()``. For example::

    {
        'ssl_options' : {
            'ca_certs' : PATH_TO_CA_CERTS
        }
    }

Default load balancing policy is RoundRobinPolicy. To specify a different
LB policy::

    - DCAwareRoundRobinPolicy
        {
            'load_balancing_policy': 'DCAwareRoundRobinPolicy',
            'load_balancing_policy_args': {
                'local_dc': LOCAL_DC_NAME,                      // optional
                'used_hosts_per_remote_dc': SOME_INT_VALUE,     // optional
            }
         }
    - WhiteListRoundRobinPolicy
        {
            'load_balancing_policy': 'WhiteListRoundRobinPolicy',
            'load_balancing_policy_args': {
                'hosts': ['HOST1', 'HOST2', 'HOST3']
            }
        }
    - TokenAwarePolicy
        {
            'load_balancing_policy': 'TokenAwarePolicy',
            'load_balancing_policy_args': {
                'child_load_balancing_policy': CHILD_POLICY_NAME, // optional
                'child_load_balancing_policy_args': { ... }       // optional
            }
        }

For details of the Cluster config, see cassandra.cluster.

<a id="cassandra.hooks.cassandra.CassandraHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Session
```

Returns a cassandra Session object

<a id="cassandra.hooks.cassandra.CassandraHook.get_cluster"></a>

#### get\_cluster

```python
def get_cluster() -> Cluster
```

Returns Cassandra cluster.

<a id="cassandra.hooks.cassandra.CassandraHook.shutdown_cluster"></a>

#### shutdown\_cluster

```python
def shutdown_cluster() -> None
```

Closes all sessions and connections associated with this Cluster.

<a id="cassandra.hooks.cassandra.CassandraHook.get_lb_policy"></a>

#### get\_lb\_policy

```python
@staticmethod
def get_lb_policy(policy_name: str, policy_args: Dict[str, Any]) -> Policy
```

Creates load balancing policy.

**Arguments**:

- `policy_name`: Name of the policy to use.
- `policy_args`: Parameters for the policy.

<a id="cassandra.hooks.cassandra.CassandraHook.table_exists"></a>

#### table\_exists

```python
def table_exists(table: str) -> bool
```

Checks if a table exists in Cassandra

**Arguments**:

- `table`: Target Cassandra table.
Use dot notation to target a specific keyspace.

<a id="cassandra.hooks.cassandra.CassandraHook.record_exists"></a>

#### record\_exists

```python
def record_exists(table: str, keys: Dict[str, str]) -> bool
```

Checks if a record exists in Cassandra

**Arguments**:

- `table`: Target Cassandra table.
Use dot notation to target a specific keyspace.
- `keys`: The keys and their values to check the existence.

<a id="cassandra.hooks"></a>

# cassandra.hooks

<a id="druid"></a>

# druid

<a id="druid.operators"></a>

# druid.operators

<a id="druid.operators.druid_check"></a>

# druid.operators.druid\_check

<a id="druid.operators.druid_check.DruidCheckOperator"></a>

## DruidCheckOperator Objects

```python
class DruidCheckOperator(SQLCheckOperator)
```

This class is deprecated.
Please use `airflow.operators.sql.SQLCheckOperator`.

<a id="druid.operators.druid"></a>

# druid.operators.druid

<a id="druid.operators.druid.DruidOperator"></a>

## DruidOperator Objects

```python
class DruidOperator(BaseOperator)
```

Allows to submit a task directly to druid

**Arguments**:

- `json_index_file`: The filepath to the druid index specification
- `druid_ingest_conn_id`: The connection id of the Druid overlord which
accepts index jobs
- `timeout`: The interval (in seconds) between polling the Druid job for the status
of the ingestion job. Must be greater than or equal to 1
- `max_ingestion_time`: The maximum ingestion time before assuming the job failed

<a id="druid.transfers.hive_to_druid"></a>

# druid.transfers.hive\_to\_druid

This module contains operator to move data from Hive to Druid.

<a id="druid.transfers.hive_to_druid.HiveToDruidOperator"></a>

## HiveToDruidOperator Objects

```python
class HiveToDruidOperator(BaseOperator)
```

Moves data from Hive to Druid, [del]note that for now the data is loaded

into memory before being pushed to Druid, so this operator should
be used for smallish amount of data.[/del]

**Arguments**:

- `sql`: SQL query to execute against the Druid database. (templated)
- `druid_datasource`: the datasource you want to ingest into in druid
- `ts_dim`: the timestamp dimension
- `metric_spec`: the metrics you want to define for your data
- `hive_cli_conn_id`: the hive connection id
- `druid_ingest_conn_id`: the druid ingest connection id
- `metastore_conn_id`: the metastore connection id
- `hadoop_dependency_coordinates`: list of coordinates to squeeze
int the ingest json
- `intervals`: list of time intervals that defines segments,
this is passed as is to the json object. (templated)
- `num_shards`: Directly specify the number of shards to create.
- `target_partition_size`: Target number of rows to include in a partition,
- `query_granularity`: The minimum granularity to be able to query results at and the granularity of
the data inside the segment. E.g. a value of "minute" will mean that data is aggregated at minutely
granularity. That is, if there are collisions in the tuple (minute(timestamp), dimensions), then it
will aggregate values together using the aggregators instead of storing individual rows.
A granularity of 'NONE' means millisecond granularity.
- `segment_granularity`: The granularity to create time chunks at. Multiple segments can be created per
time chunk. For example, with 'DAY' segmentGranularity, the events of the same day fall into the
same time chunk which can be optionally further partitioned into multiple segments based on other
configurations and input size.
- `hive_tblproperties`: additional properties for tblproperties in
hive for the staging table
- `job_properties`: additional properties for job

<a id="druid.transfers.hive_to_druid.HiveToDruidOperator.construct_ingest_query"></a>

#### construct\_ingest\_query

```python
def construct_ingest_query(static_path: str,
                           columns: List[str]) -> Dict[str, Any]
```

Builds an ingest query for an HDFS TSV load.

**Arguments**:

- `static_path`: The path on hdfs where the data is
- `columns`: List of all the columns that are available

<a id="druid.transfers"></a>

# druid.transfers

<a id="druid.example_dags"></a>

# druid.example\_dags

<a id="druid.example_dags.example_druid_dag"></a>

# druid.example\_dags.example\_druid\_dag

Example Airflow DAG to submit Apache Druid json index file using `DruidOperator`

<a id="druid.hooks"></a>

# druid.hooks

<a id="druid.hooks.druid"></a>

# druid.hooks.druid

<a id="druid.hooks.druid.DruidHook"></a>

## DruidHook Objects

```python
class DruidHook(BaseHook)
```

Connection to Druid overlord for ingestion

To connect to a Druid cluster that is secured with the druid-basic-security
extension, add the username and password to the druid ingestion connection.

**Arguments**:

- `druid_ingest_conn_id`: The connection id to the Druid overlord machine
which accepts index jobs
- `timeout`: The interval between polling
the Druid job for the status of the ingestion job.
Must be greater than or equal to 1
- `max_ingestion_time`: The maximum ingestion time before assuming the job failed

<a id="druid.hooks.druid.DruidHook.get_conn_url"></a>

#### get\_conn\_url

```python
def get_conn_url() -> str
```

Get Druid connection url

<a id="druid.hooks.druid.DruidHook.get_auth"></a>

#### get\_auth

```python
def get_auth() -> Optional[requests.auth.HTTPBasicAuth]
```

Return username and password from connections tab as requests.auth.HTTPBasicAuth object.

If these details have not been set then returns None.

<a id="druid.hooks.druid.DruidHook.submit_indexing_job"></a>

#### submit\_indexing\_job

```python
def submit_indexing_job(json_index_spec: Union[Dict[str, Any], str]) -> None
```

Submit Druid ingestion job

<a id="druid.hooks.druid.DruidDbApiHook"></a>

## DruidDbApiHook Objects

```python
class DruidDbApiHook(DbApiHook)
```

Interact with Druid broker

This hook is purely for users to query druid broker.
For ingestion, please use druidHook.

<a id="druid.hooks.druid.DruidDbApiHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> connect
```

Establish a connection to druid broker.

<a id="druid.hooks.druid.DruidDbApiHook.get_uri"></a>

#### get\_uri

```python
def get_uri() -> str
```

Get the connection uri for druid broker.

e.g: druid://localhost:8082/druid/v2/sql/

<a id="hdfs"></a>

# hdfs

<a id="hdfs.sensors"></a>

# hdfs.sensors

<a id="hdfs.sensors.hdfs"></a>

# hdfs.sensors.hdfs

<a id="hdfs.sensors.hdfs.HdfsSensor"></a>

## HdfsSensor Objects

```python
class HdfsSensor(BaseSensorOperator)
```

Waits for a file or folder to land in HDFS

**Arguments**:

- `filepath`: The route to a stored file.
- `hdfs_conn_id`: The Airflow connection used for HDFS credentials.
- `ignored_ext`: This is the list of ignored extensions.
- `ignore_copying`: Shall we ignore?
- `file_size`: This is the size of the file.
.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:HdfsSensor`

<a id="hdfs.sensors.hdfs.HdfsSensor.filter_for_filesize"></a>

#### filter\_for\_filesize

```python
@staticmethod
def filter_for_filesize(result: List[Dict[Any, Any]],
                        size: Optional[int] = None) -> List[Dict[Any, Any]]
```

Will test the filepath result and test if its size is at least self.filesize

**Arguments**:

- `result`: a list of dicts returned by Snakebite ls
- `size`: the file size in MB a file should be at least to trigger True

**Returns**:

(bool) depending on the matching criteria

<a id="hdfs.sensors.hdfs.HdfsSensor.filter_for_ignored_ext"></a>

#### filter\_for\_ignored\_ext

```python
@staticmethod
def filter_for_ignored_ext(result: List[Dict[Any,
                                             Any]], ignored_ext: List[str],
                           ignore_copying: bool) -> List[Dict[Any, Any]]
```

Will filter if instructed to do so the result to remove matching criteria

**Arguments**:

- `result`: list of dicts returned by Snakebite ls
- `ignored_ext`: list of ignored extensions
- `ignore_copying`: shall we ignore ?

**Returns**:

`list[dict]`: list of dicts which were not removed

<a id="hdfs.sensors.hdfs.HdfsSensor.poke"></a>

#### poke

```python
def poke(context: "Context") -> bool
```

Get a snakebite client connection and check for file.

<a id="hdfs.sensors.hdfs.HdfsRegexSensor"></a>

## HdfsRegexSensor Objects

```python
class HdfsRegexSensor(HdfsSensor)
```

Waits for matching files by matching on regex

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:HdfsRegexSensor`

<a id="hdfs.sensors.hdfs.HdfsRegexSensor.poke"></a>

#### poke

```python
def poke(context: "Context") -> bool
```

Poke matching files in a directory with self.regex

**Returns**:

Bool depending on the search criteria

<a id="hdfs.sensors.hdfs.HdfsFolderSensor"></a>

## HdfsFolderSensor Objects

```python
class HdfsFolderSensor(HdfsSensor)
```

Waits for a non-empty directory

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:HdfsFolderSensor`

<a id="hdfs.sensors.hdfs.HdfsFolderSensor.poke"></a>

#### poke

```python
def poke(context: "Context") -> bool
```

Poke for a non empty directory

**Returns**:

Bool depending on the search criteria

<a id="hdfs.sensors.web_hdfs"></a>

# hdfs.sensors.web\_hdfs

<a id="hdfs.sensors.web_hdfs.WebHdfsSensor"></a>

## WebHdfsSensor Objects

```python
class WebHdfsSensor(BaseSensorOperator)
```

Waits for a file or folder to land in HDFS

<a id="hdfs.hooks"></a>

# hdfs.hooks

<a id="hdfs.hooks.webhdfs"></a>

# hdfs.hooks.webhdfs

Hook for Web HDFS

<a id="hdfs.hooks.webhdfs.AirflowWebHDFSHookException"></a>

## AirflowWebHDFSHookException Objects

```python
class AirflowWebHDFSHookException(AirflowException)
```

Exception specific for WebHDFS hook

<a id="hdfs.hooks.webhdfs.WebHDFSHook"></a>

## WebHDFSHook Objects

```python
class WebHDFSHook(BaseHook)
```

Interact with HDFS. This class is a wrapper around the hdfscli library.

**Arguments**:

- `webhdfs_conn_id`: The connection id for the webhdfs client to connect to.
- `proxy_user`: The user used to authenticate.

<a id="hdfs.hooks.webhdfs.WebHDFSHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Any
```

Establishes a connection depending on the security mode set via config or environment variable.

**Returns**:

`hdfs.InsecureClient or hdfs.ext.kerberos.KerberosClient`: a hdfscli InsecureClient or KerberosClient object.

<a id="hdfs.hooks.webhdfs.WebHDFSHook.check_for_path"></a>

#### check\_for\_path

```python
def check_for_path(hdfs_path: str) -> bool
```

Check for the existence of a path in HDFS by querying FileStatus.

**Arguments**:

- `hdfs_path`: The path to check.

**Returns**:

`bool`: True if the path exists and False if not.

<a id="hdfs.hooks.hdfs"></a>

# hdfs.hooks.hdfs

Hook for HDFS operations

<a id="hdfs.hooks.hdfs.HDFSHookException"></a>

## HDFSHookException Objects

```python
class HDFSHookException(AirflowException)
```

Exception specific for HDFS

<a id="hdfs.hooks.hdfs.HDFSHook"></a>

## HDFSHook Objects

```python
class HDFSHook(BaseHook)
```

Interact with HDFS. This class is a wrapper around the snakebite library.

**Arguments**:

- `hdfs_conn_id`: Connection id to fetch connection info
- `proxy_user`: effective user for HDFS operations
- `autoconfig`: use snakebite's automatically configured client

<a id="hdfs.hooks.hdfs.HDFSHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Any
```

Returns a snakebite HDFSClient object.

<a id="hive"></a>

# hive

<a id="hive.sensors.named_hive_partition"></a>

# hive.sensors.named\_hive\_partition

<a id="hive.sensors.named_hive_partition.NamedHivePartitionSensor"></a>

## NamedHivePartitionSensor Objects

```python
class NamedHivePartitionSensor(BaseSensorOperator)
```

Waits for a set of partitions to show up in Hive.

**Arguments**:

- `partition_names`: List of fully qualified names of the
partitions to wait for. A fully qualified name is of the
form ``schema.table/pk1=pv1/pk2=pv2``, for example,
default.users/ds=2016-01-01. This is passed as is to the metastore
Thrift client ``get_partitions_by_name`` method. Note that
you cannot use logical or comparison operators as in
HivePartitionSensor.
- `metastore_conn_id`: Reference to the
:ref:`metastore thrift service connection id <howto/connection:hive_metastore>`.

<a id="hive.sensors.named_hive_partition.NamedHivePartitionSensor.parse_partition_name"></a>

#### parse\_partition\_name

```python
@staticmethod
def parse_partition_name(partition: str) -> Tuple[Any, ...]
```

Get schema, table, and partition info.

<a id="hive.sensors.named_hive_partition.NamedHivePartitionSensor.poke_partition"></a>

#### poke\_partition

```python
def poke_partition(partition: str) -> Any
```

Check for a named partition.

<a id="hive.sensors"></a>

# hive.sensors

<a id="hive.sensors.hive_partition"></a>

# hive.sensors.hive\_partition

<a id="hive.sensors.hive_partition.HivePartitionSensor"></a>

## HivePartitionSensor Objects

```python
class HivePartitionSensor(BaseSensorOperator)
```

Waits for a partition to show up in Hive.

Note: Because ``partition`` supports general logical operators, it
can be inefficient. Consider using NamedHivePartitionSensor instead if
you don't need the full flexibility of HivePartitionSensor.

**Arguments**:

- `table`: The name of the table to wait for, supports the dot
notation (my_database.my_table)
- `partition`: The partition clause to wait for. This is passed as
is to the metastore Thrift client ``get_partitions_by_filter`` method,
and apparently supports SQL like notation as in ``ds='2015-01-01'
AND type='value'`` and comparison operators as in ``"ds>=2015-01-01"``
- `metastore_conn_id`: reference to the
:ref: `metastore thrift service connection id <howto/connection:hive_metastore>`

<a id="hive.sensors.metastore_partition"></a>

# hive.sensors.metastore\_partition

<a id="hive.sensors.metastore_partition.MetastorePartitionSensor"></a>

## MetastorePartitionSensor Objects

```python
class MetastorePartitionSensor(SqlSensor)
```

An alternative to the HivePartitionSensor that talk directly to the

MySQL db. This was created as a result of observing sub optimal
queries generated by the Metastore thrift service when hitting
subpartitioned tables. The Thrift service's queries were written in a
way that wouldn't leverage the indexes.

**Arguments**:

- `schema`: the schema
- `table`: the table
- `partition_name`: the partition name, as defined in the PARTITIONS
table of the Metastore. Order of the fields does matter.
Examples: ``ds=2016-01-01`` or
``ds=2016-01-01/sub=foo`` for a sub partitioned table
- `mysql_conn_id`: a reference to the MySQL conn_id for the metastore

<a id="hive.operators"></a>

# hive.operators

<a id="hive.operators.hive"></a>

# hive.operators.hive

<a id="hive.operators.hive.HiveOperator"></a>

## HiveOperator Objects

```python
class HiveOperator(BaseOperator)
```

Executes hql code or hive script in a specific Hive database.

**Arguments**:

- `hql`: the hql to be executed. Note that you may also use
a relative path from the dag file of a (template) hive
script. (templated)
- `hive_cli_conn_id`: Reference to the
:ref:`Hive CLI connection id <howto/connection:hive_cli>`. (templated)
- `hiveconfs`: if defined, these key value pairs will be passed
to hive as ``-hiveconf "key"="value"``
- `hiveconf_jinja_translate`: when True, hiveconf-type templating
${var} gets translated into jinja-type templating {{ var }} and
${hiveconf:var} gets translated into jinja-type templating {{ var }}.
Note that you may want to use this along with the
``DAG(user_defined_macros=myargs)`` parameter. View the DAG
object documentation for more details.
- `script_begin_tag`: If defined, the operator will get rid of the
part of the script before the first occurrence of `script_begin_tag`
- `run_as_owner`: Run HQL code as a DAG's owner.
- `mapred_queue`: queue used by the Hadoop CapacityScheduler. (templated)
- `mapred_queue_priority`: priority within CapacityScheduler queue.
Possible settings include: VERY_HIGH, HIGH, NORMAL, LOW, VERY_LOW
- `mapred_job_name`: This name will appear in the jobtracker.
This can make monitoring easier.

<a id="hive.operators.hive.HiveOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> HiveCliHook
```

Get Hive cli hook

<a id="hive.operators.hive.HiveOperator.clear_airflow_vars"></a>

#### clear\_airflow\_vars

```python
def clear_airflow_vars() -> None
```

Reset airflow environment variables to prevent existing ones from impacting behavior.

<a id="hive.operators.hive_stats"></a>

# hive.operators.hive\_stats

<a id="hive.operators.hive_stats.HiveStatsCollectionOperator"></a>

## HiveStatsCollectionOperator Objects

```python
class HiveStatsCollectionOperator(BaseOperator)
```

Gathers partition statistics using a dynamically generated Presto

query, inserts the stats into a MySql table with this format. Stats
overwrite themselves if you rerun the same date/partition. ::

    CREATE TABLE hive_stats (
        ds VARCHAR(16),
        table_name VARCHAR(500),
        metric VARCHAR(200),
        value BIGINT
    );

**Arguments**:

- `metastore_conn_id`: Reference to the
:ref:`Hive Metastore connection id <howto/connection:hive_metastore>`.
- `table`: the source table, in the format ``database.table_name``. (templated)
- `partition`: the source partition. (templated)
- `extra_exprs`: dict of expression to run against the table where
keys are metric names and values are Presto compatible expressions
- `excluded_columns`: list of columns to exclude, consider
excluding blobs, large json columns, ...
- `assignment_func`: a function that receives a column name and
a type, and returns a dict of metric names and an Presto expressions.
If None is returned, the global defaults are applied. If an
empty dictionary is returned, no stats are computed for that
column.

<a id="hive.operators.hive_stats.HiveStatsCollectionOperator.get_default_exprs"></a>

#### get\_default\_exprs

```python
def get_default_exprs(col: str, col_type: str) -> Dict[Any, Any]
```

Get default expressions

<a id="hive.transfers.vertica_to_hive"></a>

# hive.transfers.vertica\_to\_hive

This module contains an operator to move data from Vertica to Hive.

<a id="hive.transfers.vertica_to_hive.VerticaToHiveOperator"></a>

## VerticaToHiveOperator Objects

```python
class VerticaToHiveOperator(BaseOperator)
```

Moves data from Vertica to Hive. The operator runs

your query against Vertica, stores the file locally
before loading it into a Hive table. If the ``create`` or
``recreate`` arguments are set to ``True``,
a ``CREATE TABLE`` and ``DROP TABLE`` statements are generated.
Hive data types are inferred from the cursor's metadata.
Note that the table generated in Hive uses ``STORED AS textfile``
which isn't the most efficient serialization format. If a
large amount of data is loaded and/or if the table gets
queried considerably, you may want to use this operator only to
stage the data into a temporary table before loading it into its
final destination using a ``HiveOperator``.

**Arguments**:

- `sql`: SQL query to execute against the Vertica database. (templated)
- `hive_table`: target Hive table, use dot notation to target a
specific database. (templated)
- `create`: whether to create the table if it doesn't exist
- `recreate`: whether to drop and recreate the table at every execution
- `partition`: target partition as a dict of partition columns
and values. (templated)
- `delimiter`: field delimiter in the file
- `vertica_conn_id`: source Vertica connection
- `hive_cli_conn_id`: Reference to the
:ref:`Hive CLI connection id <howto/connection:hive_cli>`.

<a id="hive.transfers.vertica_to_hive.VerticaToHiveOperator.type_map"></a>

#### type\_map

```python
@classmethod
def type_map(cls, vertica_type)
```

Vertica-python datatype.py does not provide the full type mapping access.
Manual hack. Reference:
https://github.com/uber/vertica-python/blob/master/vertica_python/vertica/column.py

<a id="hive.transfers.mssql_to_hive"></a>

# hive.transfers.mssql\_to\_hive

This module contains an operator to move data from MSSQL to Hive.

<a id="hive.transfers.mssql_to_hive.MsSqlToHiveOperator"></a>

## MsSqlToHiveOperator Objects

```python
class MsSqlToHiveOperator(BaseOperator)
```

Moves data from Microsoft SQL Server to Hive. The operator runs

your query against Microsoft SQL Server, stores the file locally
before loading it into a Hive table. If the ``create`` or
``recreate`` arguments are set to ``True``,
a ``CREATE TABLE`` and ``DROP TABLE`` statements are generated.
Hive data types are inferred from the cursor's metadata.
Note that the table generated in Hive uses ``STORED AS textfile``
which isn't the most efficient serialization format. If a
large amount of data is loaded and/or if the table gets
queried considerably, you may want to use this operator only to
stage the data into a temporary table before loading it into its
final destination using a ``HiveOperator``.

**Arguments**:

- `sql`: SQL query to execute against the Microsoft SQL Server
database. (templated)
- `hive_table`: target Hive table, use dot notation to target a specific
database. (templated)
- `create`: whether to create the table if it doesn't exist
- `recreate`: whether to drop and recreate the table at every execution
- `partition`: target partition as a dict of partition columns and
values. (templated)
- `delimiter`: field delimiter in the file
- `mssql_conn_id`: source Microsoft SQL Server connection
- `hive_cli_conn_id`: Reference to the
:ref:`Hive CLI connection id <howto/connection:hive_cli>`.
- `tblproperties`: TBLPROPERTIES of the hive table being created

<a id="hive.transfers.mssql_to_hive.MsSqlToHiveOperator.type_map"></a>

#### type\_map

```python
@classmethod
def type_map(cls, mssql_type: int) -> str
```

Maps MsSQL type to Hive type.

<a id="hive.transfers.hive_to_mysql"></a>

# hive.transfers.hive\_to\_mysql

This module contains an operator to move data from Hive to MySQL.

<a id="hive.transfers.hive_to_mysql.HiveToMySqlOperator"></a>

## HiveToMySqlOperator Objects

```python
class HiveToMySqlOperator(BaseOperator)
```

Moves data from Hive to MySQL, note that for now the data is loaded

into memory before being pushed to MySQL, so this operator should
be used for smallish amount of data.

**Arguments**:

- `sql`: SQL query to execute against Hive server. (templated)
- `mysql_table`: target MySQL table, use dot notation to target a
specific database. (templated)
- `mysql_conn_id`: source mysql connection
- `metastore_conn_id`: Reference to the
:ref:`metastore thrift service connection id <howto/connection:hive_metastore>`.
- `mysql_preoperator`: sql statement to run against mysql prior to
import, typically use to truncate of delete in place
of the data coming in, allowing the task to be idempotent (running
the task twice won't double load data). (templated)
- `mysql_postoperator`: sql statement to run against mysql after the
import, typically used to move data from staging to
production and issue cleanup commands. (templated)
- `bulk_load`: flag to use bulk_load option.  This loads mysql directly
from a tab-delimited text file using the LOAD DATA LOCAL INFILE command.
This option requires an extra connection parameter for the
destination MySQL connection: {'local_infile': true}.
- `hive_conf`: 

<a id="hive.transfers.mysql_to_hive"></a>

# hive.transfers.mysql\_to\_hive

This module contains an operator to move data from MySQL to Hive.

<a id="hive.transfers.mysql_to_hive.MySqlToHiveOperator"></a>

## MySqlToHiveOperator Objects

```python
class MySqlToHiveOperator(BaseOperator)
```

Moves data from MySql to Hive. The operator runs your query against

MySQL, stores the file locally before loading it into a Hive table.
If the ``create`` or ``recreate`` arguments are set to ``True``,
a ``CREATE TABLE`` and ``DROP TABLE`` statements are generated.
Hive data types are inferred from the cursor's metadata. Note that the
table generated in Hive uses ``STORED AS textfile``
which isn't the most efficient serialization format. If a
large amount of data is loaded and/or if the table gets
queried considerably, you may want to use this operator only to
stage the data into a temporary table before loading it into its
final destination using a ``HiveOperator``.

**Arguments**:

- `sql`: SQL query to execute against the MySQL database. (templated)
- `hive_table`: target Hive table, use dot notation to target a
specific database. (templated)
- `create`: whether to create the table if it doesn't exist
- `recreate`: whether to drop and recreate the table at every
execution
- `partition`: target partition as a dict of partition columns
and values. (templated)
- `delimiter`: field delimiter in the file
- `quoting`: controls when quotes should be generated by csv writer,
It can take on any of the csv.QUOTE_* constants.
- `quotechar`: one-character string used to quote fields
containing special characters.
- `escapechar`: one-character string used by csv writer to escape
the delimiter or quotechar.
- `mysql_conn_id`: source mysql connection
- `hive_cli_conn_id`: Reference to the
:ref:`Hive CLI connection id <howto/connection:hive_cli>`.
- `tblproperties`: TBLPROPERTIES of the hive table being created

<a id="hive.transfers.mysql_to_hive.MySqlToHiveOperator.type_map"></a>

#### type\_map

```python
@classmethod
def type_map(cls, mysql_type: int) -> str
```

Maps MySQL type to Hive type.

<a id="hive.transfers"></a>

# hive.transfers

<a id="hive.transfers.s3_to_hive"></a>

# hive.transfers.s3\_to\_hive

This module contains an operator to move data from an S3 bucket to Hive.

<a id="hive.transfers.s3_to_hive.S3ToHiveOperator"></a>

## S3ToHiveOperator Objects

```python
class S3ToHiveOperator(BaseOperator)
```

Moves data from S3 to Hive. The operator downloads a file from S3,

stores the file locally before loading it into a Hive table.
If the ``create`` or ``recreate`` arguments are set to ``True``,
a ``CREATE TABLE`` and ``DROP TABLE`` statements are generated.
Hive data types are inferred from the cursor's metadata from.

Note that the table generated in Hive uses ``STORED AS textfile``
which isn't the most efficient serialization format. If a
large amount of data is loaded and/or if the tables gets
queried considerably, you may want to use this operator only to
stage the data into a temporary table before loading it into its
final destination using a ``HiveOperator``.

**Arguments**:

- `s3_key`: The key to be retrieved from S3. (templated)
- `field_dict`: A dictionary of the fields name in the file
as keys and their Hive types as values
- `hive_table`: target Hive table, use dot notation to target a
specific database. (templated)
- `delimiter`: field delimiter in the file
- `create`: whether to create the table if it doesn't exist
- `recreate`: whether to drop and recreate the table at every
execution
- `partition`: target partition as a dict of partition columns
and values. (templated)
- `headers`: whether the file contains column names on the first
line
- `check_headers`: whether the column names on the first line should be
checked against the keys of field_dict
- `wildcard_match`: whether the s3_key should be interpreted as a Unix
wildcard pattern
- `aws_conn_id`: source s3 connection
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
You can provide the following values:

- ``False``: do not validate SSL certificates. SSL will still be used
         (unless use_ssl is False), but SSL certificates will not be
         verified.
- ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
         You can specify this argument if you want to use a different
         CA cert bundle than the one used by botocore.
- `hive_cli_conn_id`: Reference to the
:ref:`Hive CLI connection id <howto/connection:hive_cli>`.
- `input_compressed`: Boolean to determine if file decompression is
required to process headers
- `tblproperties`: TBLPROPERTIES of the hive table being created
- `select_expression`: S3 Select expression

<a id="hive.transfers.hive_to_samba"></a>

# hive.transfers.hive\_to\_samba

This module contains an operator to move data from Hive to Samba.

<a id="hive.transfers.hive_to_samba.HiveToSambaOperator"></a>

## HiveToSambaOperator Objects

```python
class HiveToSambaOperator(BaseOperator)
```

Executes hql code in a specific Hive database and loads the

results of the query as a csv to a Samba location.

**Arguments**:

- `hql`: the hql to be exported. (templated)
- `destination_filepath`: the file path to where the file will be pushed onto samba
- `samba_conn_id`: reference to the samba destination
- `hiveserver2_conn_id`: Reference to the
:ref: `Hive Server2 thrift service connection id <howto/connection:hiveserver2>`.

<a id="hive.example_dags"></a>

# hive.example\_dags

<a id="hive.example_dags.example_twitter_dag"></a>

# hive.example\_dags.example\_twitter\_dag

This is an example dag for managing twitter data.

<a id="hive.example_dags.example_twitter_dag.fetch_tweets"></a>

#### fetch\_tweets

```python
@task
def fetch_tweets()
```

This task should call Twitter API and retrieve tweets from yesterday from and to for the four twitter
users (Twitter_A,..,Twitter_D) There should be eight csv output files generated by this task and naming
convention is direction(from or to)_twitterHandle_date.csv

<a id="hive.example_dags.example_twitter_dag.clean_tweets"></a>

#### clean\_tweets

```python
@task
def clean_tweets()
```

This is a placeholder to clean the eight files. In this step you can get rid of or cherry pick columns
and different parts of the text.

<a id="hive.example_dags.example_twitter_dag.analyze_tweets"></a>

#### analyze\_tweets

```python
@task
def analyze_tweets()
```

This is a placeholder to analyze the twitter data. Could simply be a sentiment analysis through algorithms
like bag of words or something more complicated. You can also take a look at Web Services to do such
tasks.

<a id="hive.example_dags.example_twitter_dag.transfer_to_db"></a>

#### transfer\_to\_db

```python
@task
def transfer_to_db()
```

This is a placeholder to extract summary from Hive data and store it to MySQL.

<a id="hive.hooks"></a>

# hive.hooks

<a id="hive.hooks.hive"></a>

# hive.hooks.hive

<a id="hive.hooks.hive.get_context_from_env_var"></a>

#### get\_context\_from\_env\_var

```python
def get_context_from_env_var() -> Dict[Any, Any]
```

Extract context from env variable, e.g. dag_id, task_id and execution_date,

so that they can be used inside BashOperator and PythonOperator.

**Returns**:

The context of interest.

<a id="hive.hooks.hive.HiveCliHook"></a>

## HiveCliHook Objects

```python
class HiveCliHook(BaseHook)
```

Simple wrapper around the hive CLI.

It also supports the ``beeline``
a lighter CLI that runs JDBC and is replacing the heavier
traditional CLI. To enable ``beeline``, set the use_beeline param in the
extra field of your connection as in ``{ "use_beeline": true }``

Note that you can also set default hive CLI parameters using the
``hive_cli_params`` to be used in your connection as in
``{"hive_cli_params": "-hiveconf mapred.job.tracker=some.jobtracker:444"}``
Parameters passed here can be overridden by run_cli's hive_conf param

The extra connection parameter ``auth`` gets passed as in the ``jdbc``
connection string as is.

**Arguments**:

- `hive_cli_conn_id`: Reference to the
:ref:`Hive CLI connection id <howto/connection:hive_cli>`.
- `mapred_queue`: queue used by the Hadoop Scheduler (Capacity or Fair)
- `mapred_queue_priority`: priority within the job queue.
Possible settings include: VERY_HIGH, HIGH, NORMAL, LOW, VERY_LOW
- `mapred_job_name`: This name will appear in the jobtracker.
This can make monitoring easier.

<a id="hive.hooks.hive.HiveCliHook.run_cli"></a>

#### run\_cli

```python
def run_cli(hql: str,
            schema: Optional[str] = None,
            verbose: bool = True,
            hive_conf: Optional[Dict[Any, Any]] = None) -> Any
```

Run an hql statement using the hive cli. If hive_conf is specified

it should be a dict and the entries will be set as key/value pairs
in HiveConf.

**Arguments**:

- `hql`: an hql (hive query language) statement to run with hive cli
- `schema`: Name of hive schema (database) to use
- `verbose`: Provides additional logging. Defaults to True.
- `hive_conf`: if specified these key value pairs will be passed
to hive as ``-hiveconf "key"="value"``. Note that they will be
    passed after the ``hive_cli_params`` and thus will override
    whatever values are specified in the database.

>>> hh = HiveCliHook()
>>> result = hh.run_cli("USE airflow;")
>>> ("OK" in result)
True

<a id="hive.hooks.hive.HiveCliHook.test_hql"></a>

#### test\_hql

```python
def test_hql(hql: str) -> None
```

Test an hql statement using the hive cli and EXPLAIN

<a id="hive.hooks.hive.HiveCliHook.load_df"></a>

#### load\_df

