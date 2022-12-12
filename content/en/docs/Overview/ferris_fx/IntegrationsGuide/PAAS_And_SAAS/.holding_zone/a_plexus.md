---
title: "plexus"
linkTitle: "plexus"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     plexus Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.job"></a>

# operators.job

<a id="operators.job.PlexusJobOperator"></a>

## PlexusJobOperator Objects

```python
class PlexusJobOperator(BaseOperator)
```

Submits a Plexus job.

**Arguments**:

- `job_params`: parameters required to launch a job.
Required job parameters are the following
    - "name": job name created by user.
    - "app": name of the application to run. found in Plexus UI.
    - "queue": public cluster name. found in Plexus UI.
    - "num_nodes": number of nodes.
    - "num_cores":  number of cores per node.

<a id="operators.job.PlexusJobOperator.construct_job_params"></a>

#### construct\_job\_params

```python
def construct_job_params(hook: Any) -> Dict[Any, Optional[Any]]
```

Creates job_params dict for api call to

launch a Plexus job.

Some parameters required to launch a job
are not available to the user in the Plexus
UI. For example, an app id is required, but
only the app name is provided in the UI.
This function acts as a backend lookup
of the required param value using the
user-provided value.

**Arguments**:

- `hook`: plexus hook object

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_plexus"></a>

# example\_dags.example\_plexus

<a id="hooks"></a>

# hooks

<a id="hooks.plexus"></a>

# hooks.plexus

<a id="hooks.plexus.PlexusHook"></a>

## PlexusHook Objects

```python
class PlexusHook(BaseHook)
```

Used for jwt token generation and storage to
make Plexus API calls. Requires email and password
Airflow variables be created.

**Example**:

  - export AIRFLOW_VAR_EMAIL = user@corescientific.com
  - export AIRFLOW_VAR_PASSWORD = *******

<a id="hooks.plexus.PlexusHook.token"></a>

#### token

```python
@property
def token() -> Any
```

Returns users token

