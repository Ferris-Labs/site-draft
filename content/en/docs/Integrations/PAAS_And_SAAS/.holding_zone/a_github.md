---
title: "github"
linkTitle: "github"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     github Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.github"></a>

# sensors.github

<a id="sensors.github.GithubSensor"></a>

## GithubSensor Objects

```python
class GithubSensor(BaseSensorOperator)
```

Base GithubSensor which can monitor for any change.

**Arguments**:

- `github_conn_id`: reference to a pre-defined Github Connection
- `method_name`: method name from PyGithub to be executed
- `method_params`: parameters for the method method_name
- `result_processor`: function that return boolean and act as a sensor response

<a id="sensors.github.BaseGithubRepositorySensor"></a>

## BaseGithubRepositorySensor Objects

```python
class BaseGithubRepositorySensor(GithubSensor)
```

Base GitHub sensor at Repository level.

**Arguments**:

- `github_conn_id`: reference to a pre-defined GitHub Connection
- `repository_name`: full qualified name of the repository to be monitored, ex. "apache/airflow"

<a id="sensors.github.BaseGithubRepositorySensor.poke"></a>

#### poke

```python
def poke(context: 'Context') -> bool
```

Function that the sensors defined while deriving this class should
override.

<a id="sensors.github.GithubTagSensor"></a>

## GithubTagSensor Objects

```python
class GithubTagSensor(BaseGithubRepositorySensor)
```

Monitors a github tag for its creation.

**Arguments**:

- `github_conn_id`: reference to a pre-defined Github Connection
- `tag_name`: name of the tag to be monitored
- `repository_name`: fully qualified name of the repository to be monitored, ex. "apache/airflow"

<a id="sensors.github.GithubTagSensor.tag_checker"></a>

#### tag\_checker

```python
def tag_checker(repo: Any) -> Optional[bool]
```

Checking existence of Tag in a Repository

<a id="operators"></a>

# operators

<a id="operators.github"></a>

# operators.github

<a id="operators.github.GithubOperator"></a>

## GithubOperator Objects

```python
class GithubOperator(BaseOperator)
```

GithubOperator to interact and perform action on GitHub API.

This operator is designed to use GitHub Python SDK: https://github.com/PyGithub/PyGithub

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:GithubOperator`

**Arguments**:

- `github_conn_id`: reference to a pre-defined GitHub Connection
- `github_method`: method name from GitHub Python SDK to be called
- `github_method_args`: required method parameters for the github_method. (templated)
- `result_processor`: function to further process the response from GitHub API

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_github"></a>

# example\_dags.example\_github

<a id="hooks"></a>

# hooks

<a id="hooks.github"></a>

# hooks.github

This module allows to connect to a Github.

<a id="hooks.github.GithubHook"></a>

## GithubHook Objects

```python
class GithubHook(BaseHook)
```

Interact with Github.

Performs a connection to GitHub and retrieves client.

**Arguments**:

- `github_conn_id`: Reference to :ref:`GitHub connection id <howto/connection:github>`.

<a id="hooks.github.GithubHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> GithubClient
```

Function that initiates a new GitHub connection
with token and hostname ( for GitHub Enterprise )

<a id="hooks.github.GithubHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict
```

Returns custom field behaviour

