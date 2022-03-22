---
title: "asana"
linkTitle: "asana"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     asana Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.asana_tasks"></a>

# operators.asana\_tasks

<a id="operators.asana_tasks.AsanaCreateTaskOperator"></a>

## AsanaCreateTaskOperator Objects

```python
class AsanaCreateTaskOperator(BaseOperator)
```

This operator can be used to create Asana tasks. For more information on

Asana optional task parameters, see https://developers.asana.com/docs/create-a-task

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AsanaCreateTaskOperator`

**Arguments**:

- `conn_id`: The Asana connection to use.
- `name`: Name of the Asana task.
- `task_parameters`: Any of the optional task creation parameters.
See https://developers.asana.com/docs/create-a-task for a complete list.
You must specify at least one of 'workspace', 'parent', or 'projects'
either here or in the connection.

<a id="operators.asana_tasks.AsanaUpdateTaskOperator"></a>

## AsanaUpdateTaskOperator Objects

```python
class AsanaUpdateTaskOperator(BaseOperator)
```

This operator can be used to update Asana tasks.

For more information on Asana optional task parameters, see
https://developers.asana.com/docs/update-a-task

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AsanaUpdateTaskOperator`

**Arguments**:

- `conn_id`: The Asana connection to use.
- `asana_task_gid`: Asana task ID to update
- `task_parameters`: Any task parameters that should be updated.
See https://developers.asana.com/docs/update-a-task for a complete list.

<a id="operators.asana_tasks.AsanaDeleteTaskOperator"></a>

## AsanaDeleteTaskOperator Objects

```python
class AsanaDeleteTaskOperator(BaseOperator)
```

This operator can be used to delete Asana tasks.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AsanaDeleteTaskOperator`

**Arguments**:

- `conn_id`: The Asana connection to use.
- `asana_task_gid`: Asana Task ID to delete.

<a id="operators.asana_tasks.AsanaFindTaskOperator"></a>

## AsanaFindTaskOperator Objects

```python
class AsanaFindTaskOperator(BaseOperator)
```

This operator can be used to retrieve Asana tasks that match various filters.

See https://developers.asana.com/docs/update-a-task for a list of possible filters.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AsanaFindTaskOperator`

**Arguments**:

- `conn_id`: The Asana connection to use.
- `search_parameters`: The parameters used to find relevant tasks. You must
specify at least one of `project`, `section`, `tag`, `user_task_list`, or both
`assignee` and `workspace` either here or in the connection.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_asana"></a>

# example\_dags.example\_asana

Example DAG showing how to use Asana TaskOperators.

<a id="hooks"></a>

# hooks

<a id="hooks.asana"></a>

# hooks.asana

Connect to Asana.

<a id="hooks.asana.AsanaHook"></a>

## AsanaHook Objects

```python
class AsanaHook(BaseHook)
```

Wrapper around Asana Python client library.

<a id="hooks.asana.AsanaHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="hooks.asana.AsanaHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.asana.AsanaHook.client"></a>

#### client

```python
@cached_property
def client() -> Client
```

Instantiates python-asana Client

<a id="hooks.asana.AsanaHook.create_task"></a>

#### create\_task

```python
def create_task(task_name: str, params: Optional[dict]) -> dict
```

Creates an Asana task.

**Arguments**:

- `task_name`: Name of the new task
- `params`: Other task attributes, such as due_on, parent, and notes. For a complete list
of possible parameters, see https://developers.asana.com/docs/create-a-task

**Returns**:

A dict of attributes of the created task, including its gid

<a id="hooks.asana.AsanaHook.delete_task"></a>

#### delete\_task

```python
def delete_task(task_id: str) -> dict
```

Deletes an Asana task.

**Arguments**:

- `task_id`: Asana GID of the task to delete

**Returns**:

A dict containing the response from Asana

<a id="hooks.asana.AsanaHook.find_task"></a>

#### find\_task

```python
def find_task(params: Optional[dict]) -> list
```

Retrieves a list of Asana tasks that match search parameters.

**Arguments**:

- `params`: Attributes that matching tasks should have. For a list of possible parameters,
see https://developers.asana.com/docs/get-multiple-tasks

**Returns**:

A list of dicts containing attributes of matching Asana tasks

<a id="hooks.asana.AsanaHook.update_task"></a>

#### update\_task

```python
def update_task(task_id: str, params: dict) -> dict
```

Updates an existing Asana task.

**Arguments**:

- `task_id`: Asana GID of task to update
- `params`: New values of the task's attributes. For a list of possible parameters, see
https://developers.asana.com/docs/update-a-task

**Returns**:

A dict containing the updated task's attributes

<a id="hooks.asana.AsanaHook.create_project"></a>

#### create\_project

```python
def create_project(params: dict) -> dict
```

Creates a new project.

**Arguments**:

- `params`: Attributes that the new project should have. See
https://developers.asana.com/docs/create-a-project#create-a-project-parameters
for a list of possible parameters.

**Returns**:

A dict containing the new project's attributes, including its GID.

<a id="hooks.asana.AsanaHook.find_project"></a>

#### find\_project

```python
def find_project(params: dict) -> list
```

Retrieves a list of Asana projects that match search parameters.

**Arguments**:

- `params`: Attributes which matching projects should have. See
https://developers.asana.com/docs/get-multiple-projects
for a list of possible parameters.

**Returns**:

A list of dicts containing attributes of matching Asana projects

<a id="hooks.asana.AsanaHook.update_project"></a>

#### update\_project

```python
def update_project(project_id: str, params: dict) -> dict
```

Updates an existing project.

**Arguments**:

- `project_id`: Asana GID of the project to update
- `params`: New attributes that the project should have. See
https://developers.asana.com/docs/update-a-project#update-a-project-parameters
for a list of possible parameters

**Returns**:

A dict containing the updated project's attributes

<a id="hooks.asana.AsanaHook.delete_project"></a>

#### delete\_project

```python
def delete_project(project_id: str) -> dict
```

Deletes a project.

**Arguments**:

- `project_id`: Asana GID of the project to delete

**Returns**:

A dict containing the response from Asana

