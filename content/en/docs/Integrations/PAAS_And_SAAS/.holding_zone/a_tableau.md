---
title: "tableau"
linkTitle: "tableau"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     tableau Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.tableau_job_status"></a>

# sensors.tableau\_job\_status

<a id="sensors.tableau_job_status.TableauJobStatusSensor"></a>

## TableauJobStatusSensor Objects

```python
class TableauJobStatusSensor(BaseSensorOperator)
```

Watches the status of a Tableau Server Job.

.. seealso:: https://tableau.github.io/server-client-python/docs/api-ref#jobs

**Arguments**:

- `job_id`: Id of the job to watch.
- `site_id`: The id of the site where the workbook belongs to.
- `tableau_conn_id`: The :ref:`Tableau Connection id <howto/connection:tableau>`
containing the credentials to authenticate to the Tableau Server.

<a id="sensors.tableau_job_status.TableauJobStatusSensor.poke"></a>

#### poke

```python
def poke(context: 'Context') -> bool
```

Pokes until the job has successfully finished.

**Arguments**:

- `context`: The task context during execution.

**Returns**:

`bool`: True if it succeeded and False if not.

<a id="operators"></a>

# operators

<a id="operators.tableau"></a>

# operators.tableau

<a id="operators.tableau.TableauOperator"></a>

## TableauOperator Objects

```python
class TableauOperator(BaseOperator)
```

Execute a Tableau API Resource

https://tableau.github.io/server-client-python/docs/api-ref

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:TableauOperator`

**Arguments**:

- `resource`: The name of the resource to use.
- `method`: The name of the resource's method to execute.
- `find`: The reference of resource that will receive the action.
- `match_with`: The resource field name to be matched with find parameter.
- `site_id`: The id of the site where the workbook belongs to.
- `blocking_refresh`: By default will be blocking means it will wait until it has finished.
- `check_interval`: time in seconds that the job should wait in
between each instance state checks until operation is completed
- `tableau_conn_id`: The :ref:`Tableau Connection id <howto/connection:tableau>`
containing the credentials to authenticate to the Tableau Server.

<a id="operators.tableau.TableauOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> str
```

Executes the Tableau API resource and pushes the job id or downloaded file URI to xcom.

**Arguments**:

- `context`: The task context during execution.

**Returns**:

`str`: the id of the job that executes the extract refresh or downloaded file URI.

<a id="operators.tableau_refresh_workbook"></a>

# operators.tableau\_refresh\_workbook

<a id="operators.tableau_refresh_workbook.TableauRefreshWorkbookOperator"></a>

## TableauRefreshWorkbookOperator Objects

```python
class TableauRefreshWorkbookOperator(BaseOperator)
```

This operator is deprecated. Please use `airflow.providers.tableau.operators.tableau`.

Refreshes a Tableau Workbook/Extract

.. seealso:: https://tableau.github.io/server-client-python/docs/api-ref#workbooks

**Arguments**:

- `workbook_name`: The name of the workbook to refresh.
- `site_id`: The id of the site where the workbook belongs to.
- `blocking`: Defines if the job waits until the refresh has finished.
Default: True.
- `tableau_conn_id`: The :ref:`Tableau Connection id <howto/connection:tableau>`
containing the credentials to authenticate to the Tableau Server. Default:
'tableau_default'.
- `check_interval`: time in seconds that the job should wait in
between each instance state checks until operation is completed

<a id="operators.tableau_refresh_workbook.TableauRefreshWorkbookOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> str
```

Executes the Tableau Extract Refresh and pushes the job id to xcom.

**Arguments**:

- `context`: The task context during execution.

**Returns**:

`str`: the id of the job that executes the extract refresh

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_tableau_refresh_workbook"></a>

# example\_dags.example\_tableau\_refresh\_workbook

This is an example dag that performs two refresh operations on a Tableau Workbook aka Extract. The first one
waits until it succeeds. The second does not wait since this is an asynchronous operation and we don't know
when the operation actually finishes. That's why we have another task that checks only that.

<a id="example_dags.example_tableau"></a>

# example\_dags.example\_tableau

This is an example dag that performs two refresh operations on a Tableau Workbook aka Extract. The first one
waits until it succeeds. The second does not wait since this is an asynchronous operation and we don't know
when the operation actually finishes. That's why we have another task that checks only that.

<a id="hooks"></a>

# hooks

<a id="hooks.tableau"></a>

# hooks.tableau

<a id="hooks.tableau.parse_boolean"></a>

#### parse\_boolean

```python
def parse_boolean(val: str) -> Union[str, bool]
```

Try to parse a string into boolean.

The string is returned as-is if it does not look like a boolean value.

<a id="hooks.tableau.TableauJobFailedException"></a>

## TableauJobFailedException Objects

```python
class TableauJobFailedException(AirflowException)
```

An exception that indicates that a Job failed to complete.

<a id="hooks.tableau.TableauJobFinishCode"></a>

## TableauJobFinishCode Objects

```python
class TableauJobFinishCode(Enum)
```

The finish code indicates the status of the job.
.. seealso:: https://help.tableau.com/current/api/rest_api/en-us/REST/rest_api_ref.htm#query_job

<a id="hooks.tableau.TableauHook"></a>

## TableauHook Objects

```python
class TableauHook(BaseHook)
```

Connects to the Tableau Server Instance and allows to communicate with it.

Can be used as a context manager: automatically authenticates the connection
when opened and signs out when closed.

.. seealso:: https://tableau.github.io/server-client-python/docs/

**Arguments**:

- `site_id`: The id of the site where the workbook belongs to.
It will connect to the default site if you don't provide an id.
- `tableau_conn_id`: The :ref:`Tableau Connection id <howto/connection:tableau>`
containing the credentials to authenticate to the Tableau Server.

<a id="hooks.tableau.TableauHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Auth.contextmgr
```

Sign in to the Tableau Server.

**Returns**:

`tableauserverclient.server.Auth.contextmgr`: an authorized Tableau Server Context Manager object.

<a id="hooks.tableau.TableauHook.get_all"></a>

#### get\_all

```python
def get_all(resource_name: str) -> Pager
```

Get all items of the given resource.

.. see also:: https://tableau.github.io/server-client-python/docs/page-through-results

**Arguments**:

- `resource_name`: The name of the resource to paginate.
For example: jobs or workbooks.

**Returns**:

`tableauserverclient.Pager`: all items by returning a Pager.

<a id="hooks.tableau.TableauHook.get_job_status"></a>

#### get\_job\_status

```python
def get_job_status(job_id: str) -> TableauJobFinishCode
```

Get the current state of a defined Tableau Job.

.. see also:: https://tableau.github.io/server-client-python/docs/api-ref#jobs

**Arguments**:

- `job_id`: The id of the job to check.

**Returns**:

`TableauJobFinishCode`: An Enum that describe the Tableau job’s return code

<a id="hooks.tableau.TableauHook.wait_for_state"></a>

#### wait\_for\_state

```python
def wait_for_state(job_id: str, target_state: TableauJobFinishCode,
                   check_interval: float) -> bool
```

Wait until the current state of a defined Tableau Job is equal

to target_state or different from PENDING.

**Arguments**:

- `job_id`: The id of the job to check.
- `target_state`: Enum that describe the Tableau job’s target state
- `check_interval`: time in seconds that the job should wait in
between each instance state checks until operation is completed

**Returns**:

`bool`: return True if the job is equal to the target_status, False otherwise.

