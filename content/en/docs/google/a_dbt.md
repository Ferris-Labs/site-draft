---
title: "dbt"
linkTitle: "dbt"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     dbt Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="cloud"></a>

# cloud

<a id="cloud.sensors.dbt"></a>

# cloud.sensors.dbt

<a id="cloud.sensors.dbt.DbtCloudJobRunSensor"></a>

## DbtCloudJobRunSensor Objects

```python
class DbtCloudJobRunSensor(BaseSensorOperator)
```

Checks the status of a dbt Cloud job run.

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/operator:DbtCloudJobRunSensor`

**Arguments**:

- `dbt_cloud_conn_id`: The connection identifier for connecting to dbt Cloud.
- `run_id`: The job run identifier.
- `account_id`: The dbt Cloud account identifier.

<a id="cloud.sensors"></a>

# cloud.sensors

<a id="cloud.operators.dbt"></a>

# cloud.operators.dbt

<a id="cloud.operators.dbt.DbtCloudRunJobOperatorLink"></a>

## DbtCloudRunJobOperatorLink Objects

```python
class DbtCloudRunJobOperatorLink(BaseOperatorLink)
```

Operator link for DbtCloudRunJobOperator. This link allows users to monitor the triggered job run
directly in dbt Cloud.

<a id="cloud.operators.dbt.DbtCloudRunJobOperator"></a>

## DbtCloudRunJobOperator Objects

```python
class DbtCloudRunJobOperator(BaseOperator)
```

Executes a dbt Cloud job.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:DbtCloudRunJobOperator`

**Arguments**:

- `dbt_cloud_conn_id`: The connection ID for connecting to dbt Cloud.
- `job_id`: The ID of a dbt Cloud job.
- `account_id`: Optional. The ID of a dbt Cloud account.
- `trigger_reason`: Optional. Description of the reason to trigger the job.
- `steps_override`: Optional. List of dbt commands to execute when triggering the job instead of those
configured in dbt Cloud.
- `schema_override`: Optional. Override the destination schema in the configured target for this job.
- `wait_for_termination`: Flag to wait on a job run's termination.  By default, this feature is
enabled but could be disabled to perform an asynchronous wait for a long-running job run execution
using the ``DbtCloudJobRunSensor``.
- `timeout`: Time in seconds to wait for a job run to reach a terminal status for non-asynchronous
waits. Used only if ``wait_for_termination`` is True. Defaults to 7 days.
- `check_interval`: Time in seconds to check on a job run's status for non-asynchronous waits.
Used only if ``wait_for_termination`` is True. Defaults to 60 seconds.
- `additional_run_config`: Optional. Any additional parameters that should be included in the API
request when triggering the job.

**Returns**:

The ID of the triggered dbt Cloud job run.

<a id="cloud.operators.dbt.DbtCloudGetJobRunArtifactOperator"></a>

## DbtCloudGetJobRunArtifactOperator Objects

```python
class DbtCloudGetJobRunArtifactOperator(BaseOperator)
```

Download artifacts from a dbt Cloud job run.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:DbtCloudGetJobRunArtifactOperator`

**Arguments**:

- `dbt_cloud_conn_id`: The connection ID for connecting to dbt Cloud.
- `run_id`: The ID of a dbt Cloud job run.
- `path`: The file path related to the artifact file. Paths are rooted at the target/ directory.
Use "manifest.json", "catalog.json", or "run_results.json" to download dbt-generated artifacts
for the run.
- `account_id`: Optional. The ID of a dbt Cloud account.
- `step`: Optional. The index of the Step in the Run to query for artifacts. The first step in the
run has the index 1. If the step parameter is omitted, artifacts for the last step in the run will
be returned.
- `output_file_name`: Optional. The desired file name for the download artifact file.
Defaults to <run_id>_<path> (e.g. "728368_run_results.json").

<a id="cloud.operators"></a>

# cloud.operators

<a id="cloud.example_dags.example_dbt_cloud"></a>

# cloud.example\_dags.example\_dbt\_cloud

<a id="cloud.example_dags"></a>

# cloud.example\_dags

<a id="cloud.hooks.dbt"></a>

# cloud.hooks.dbt

<a id="cloud.hooks.dbt.fallback_to_default_account"></a>

#### fallback\_to\_default\_account

```python
def fallback_to_default_account(func: Callable) -> Callable
```

Decorator which provides a fallback value for ``account_id``. If the ``account_id`` is None or not passed
to the decorated function, the value will be taken from the configured dbt Cloud Airflow Connection.

<a id="cloud.hooks.dbt.TokenAuth"></a>

## TokenAuth Objects

```python
class TokenAuth(AuthBase)
```

Helper class for Auth when executing requests.

<a id="cloud.hooks.dbt.JobRunInfo"></a>

## JobRunInfo Objects

```python
class JobRunInfo(TypedDict)
```

Type class for the ``job_run_info`` dictionary.

<a id="cloud.hooks.dbt.DbtCloudJobRunStatus"></a>

## DbtCloudJobRunStatus Objects

```python
class DbtCloudJobRunStatus(Enum)
```

dbt Cloud Job statuses.

<a id="cloud.hooks.dbt.DbtCloudJobRunStatus.check_is_valid"></a>

#### check\_is\_valid

```python
@classmethod
def check_is_valid(cls, statuses: Union[int, Sequence[int], Set[int]])
```

Validates input statuses are a known value.

<a id="cloud.hooks.dbt.DbtCloudJobRunStatus.is_terminal"></a>

#### is\_terminal

```python
@classmethod
def is_terminal(cls, status: int) -> bool
```

Checks if the input status is that of a terminal type.

<a id="cloud.hooks.dbt.DbtCloudJobRunException"></a>

## DbtCloudJobRunException Objects

```python
class DbtCloudJobRunException(AirflowException)
```

An exception that indicates a job run failed to complete.

<a id="cloud.hooks.dbt.DbtCloudHook"></a>

## DbtCloudHook Objects

```python
class DbtCloudHook(HttpHook)
```

Interact with dbt Cloud using the V2 API.

**Arguments**:

- `dbt_cloud_conn_id`: The ID of the :ref:`dbt Cloud connection <howto/connection:dbt-cloud>`.

<a id="cloud.hooks.dbt.DbtCloudHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Builds custom field behavior for the dbt Cloud connection form in the Airflow UI.

<a id="cloud.hooks.dbt.DbtCloudHook.list_accounts"></a>

#### list\_accounts

```python
def list_accounts() -> List[Response]
```

Retrieves all of the dbt Cloud accounts the configured API token is authorized to access.

**Returns**:

List of request responses.

<a id="cloud.hooks.dbt.DbtCloudHook.get_account"></a>

#### get\_account

```python
@fallback_to_default_account
def get_account(account_id: Optional[int] = None) -> Response
```

Retrieves metadata for a specific dbt Cloud account.

**Arguments**:

- `account_id`: Optional. The ID of a dbt Cloud account.

**Returns**:

The request response.

<a id="cloud.hooks.dbt.DbtCloudHook.list_projects"></a>

#### list\_projects

```python
@fallback_to_default_account
def list_projects(account_id: Optional[int] = None) -> List[Response]
```

Retrieves metadata for all projects tied to a specified dbt Cloud account.

**Arguments**:

- `account_id`: Optional. The ID of a dbt Cloud account.

**Returns**:

List of request responses.

<a id="cloud.hooks.dbt.DbtCloudHook.get_project"></a>

#### get\_project

```python
@fallback_to_default_account
def get_project(project_id: int, account_id: Optional[int] = None) -> Response
```

Retrieves metadata for a specific project.

**Arguments**:

- `project_id`: The ID of a dbt Cloud project.
- `account_id`: Optional. The ID of a dbt Cloud account.

**Returns**:

The request response.

<a id="cloud.hooks.dbt.DbtCloudHook.list_jobs"></a>

#### list\_jobs

```python
@fallback_to_default_account
def list_jobs(account_id: Optional[int] = None,
              order_by: Optional[str] = None,
              project_id: Optional[int] = None) -> List[Response]
```

Retrieves metadata for all jobs tied to a specified dbt Cloud account. If a ``project_id`` is

supplied, only jobs pertaining to this job will be retrieved.

**Arguments**:

- `account_id`: Optional. The ID of a dbt Cloud account.
- `order_by`: Optional. Field to order the result by. Use '-' to indicate reverse order.
For example, to use reverse order by the run ID use ``order_by=-id``.
- `project_id`: The ID of a dbt Cloud project.

**Returns**:

List of request responses.

<a id="cloud.hooks.dbt.DbtCloudHook.get_job"></a>

#### get\_job

```python
@fallback_to_default_account
def get_job(job_id: int, account_id: Optional[int] = None) -> Response
```

Retrieves metadata for a specific job.

**Arguments**:

- `job_id`: The ID of a dbt Cloud job.
- `account_id`: Optional. The ID of a dbt Cloud account.

**Returns**:

The request response.

<a id="cloud.hooks.dbt.DbtCloudHook.trigger_job_run"></a>

#### trigger\_job\_run

```python
@fallback_to_default_account
def trigger_job_run(
        job_id: int,
        cause: str,
        account_id: Optional[int] = None,
        steps_override: Optional[List[str]] = None,
        schema_override: Optional[str] = None,
        additional_run_config: Optional[Dict[str, Any]] = None) -> Response
```

Triggers a run of a dbt Cloud job.

**Arguments**:

- `job_id`: The ID of a dbt Cloud job.
- `cause`: Description of the reason to trigger the job.
- `account_id`: Optional. The ID of a dbt Cloud account.
- `steps_override`: Optional. List of dbt commands to execute when triggering the job
instead of those configured in dbt Cloud.
- `schema_override`: Optional. Override the destination schema in the configured target for this
job.
- `additional_run_config`: Optional. Any additional parameters that should be included in the API
request when triggering the job.

**Returns**:

The request response.

<a id="cloud.hooks.dbt.DbtCloudHook.list_job_runs"></a>

#### list\_job\_runs

```python
@fallback_to_default_account
def list_job_runs(account_id: Optional[int] = None,
                  include_related: Optional[List[str]] = None,
                  job_definition_id: Optional[int] = None,
                  order_by: Optional[str] = None) -> List[Response]
```

Retrieves metadata for all of the dbt Cloud job runs for an account. If a ``job_definition_id`` is

supplied, only metadata for runs of that specific job are pulled.

**Arguments**:

- `account_id`: Optional. The ID of a dbt Cloud account.
- `include_related`: Optional. List of related fields to pull with the run.
Valid values are "trigger", "job", "repository", and "environment".
- `job_definition_id`: Optional. The dbt Cloud job ID to retrieve run metadata.
- `order_by`: Optional. Field to order the result by. Use '-' to indicate reverse order.
For example, to use reverse order by the run ID use ``order_by=-id``.

**Returns**:

List of request responses.

<a id="cloud.hooks.dbt.DbtCloudHook.get_job_run"></a>

#### get\_job\_run

```python
@fallback_to_default_account
def get_job_run(run_id: int,
                account_id: Optional[int] = None,
                include_related: Optional[List[str]] = None) -> Response
```

Retrieves metadata for a specific run of a dbt Cloud job.

**Arguments**:

- `run_id`: The ID of a dbt Cloud job run.
- `account_id`: Optional. The ID of a dbt Cloud account.
- `include_related`: Optional. List of related fields to pull with the run.
Valid values are "trigger", "job", "repository", and "environment".

**Returns**:

The request response.

<a id="cloud.hooks.dbt.DbtCloudHook.get_job_run_status"></a>

#### get\_job\_run\_status

```python
def get_job_run_status(run_id: int, account_id: Optional[int] = None) -> int
```

Retrieves the status for a specific run of a dbt Cloud job.

**Arguments**:

- `run_id`: The ID of a dbt Cloud job run.
- `account_id`: Optional. The ID of a dbt Cloud account.

**Returns**:

The status of a dbt Cloud job run.

<a id="cloud.hooks.dbt.DbtCloudHook.wait_for_job_run_status"></a>

#### wait\_for\_job\_run\_status

```python
def wait_for_job_run_status(run_id: int,
                            account_id: Optional[int] = None,
                            expected_statuses: Union[
                                int, Sequence[int],
                                Set[int]] = DbtCloudJobRunStatus.SUCCESS.value,
                            check_interval: int = 60,
                            timeout: int = 60 * 60 * 24 * 7) -> bool
```

Waits for a dbt Cloud job run to match an expected status.

**Arguments**:

- `run_id`: The ID of a dbt Cloud job run.
- `account_id`: Optional. The ID of a dbt Cloud account.
- `expected_statuses`: Optional. The desired status(es) to check against a job run's current
status. Defaults to the success status value.
- `check_interval`: Time in seconds to check on a pipeline run's status.
- `timeout`: Time in seconds to wait for a pipeline to reach a terminal status or the expected
status.

**Returns**:

Boolean indicating if the job run has reached the ``expected_status``.

<a id="cloud.hooks.dbt.DbtCloudHook.cancel_job_run"></a>

#### cancel\_job\_run

```python
@fallback_to_default_account
def cancel_job_run(run_id: int, account_id: Optional[int] = None) -> None
```

Cancel a specific dbt Cloud job run.

**Arguments**:

- `run_id`: The ID of a dbt Cloud job run.
- `account_id`: Optional. The ID of a dbt Cloud account.

<a id="cloud.hooks.dbt.DbtCloudHook.list_job_run_artifacts"></a>

#### list\_job\_run\_artifacts

```python
@fallback_to_default_account
def list_job_run_artifacts(run_id: int,
                           account_id: Optional[int] = None,
                           step: Optional[int] = None) -> List[Response]
```

Retrieves a list of the available artifact files generated for a completed run of a dbt Cloud job. By

default, this returns artifacts from the last step in the run. To list artifacts from other steps in
the run, use the ``step`` parameter.

**Arguments**:

- `run_id`: The ID of a dbt Cloud job run.
- `account_id`: Optional. The ID of a dbt Cloud account.
- `step`: Optional. The index of the Step in the Run to query for artifacts. The first step in the
run has the index 1. If the step parameter is omitted, artifacts for the last step in the run will
be returned.

**Returns**:

List of request responses.

<a id="cloud.hooks.dbt.DbtCloudHook.get_job_run_artifact"></a>

#### get\_job\_run\_artifact

```python
@fallback_to_default_account
def get_job_run_artifact(run_id: int,
                         path: str,
                         account_id: Optional[int] = None,
                         step: Optional[int] = None) -> Response
```

Retrieves a list of the available artifact files generated for a completed run of a dbt Cloud job. By

default, this returns artifacts from the last step in the run. To list artifacts from other steps in
the run, use the ``step`` parameter.

**Arguments**:

- `run_id`: The ID of a dbt Cloud job run.
- `path`: The file path related to the artifact file. Paths are rooted at the target/ directory.
Use "manifest.json", "catalog.json", or "run_results.json" to download dbt-generated artifacts
for the run.
- `account_id`: Optional. The ID of a dbt Cloud account.
- `step`: Optional. The index of the Step in the Run to query for artifacts. The first step in the
run has the index 1. If the step parameter is omitted, artifacts for the last step in the run will
be returned.

**Returns**:

The request response.

<a id="cloud.hooks.dbt.DbtCloudHook.test_connection"></a>

#### test\_connection

```python
def test_connection() -> Tuple[bool, str]
```

Test dbt Cloud connection.

<a id="cloud.hooks"></a>

# cloud.hooks

