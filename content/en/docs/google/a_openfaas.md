---
title: "openfaas"
linkTitle: "openfaas"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     openfaas Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="hooks"></a>

# hooks

<a id="hooks.openfaas"></a>

# hooks.openfaas

<a id="hooks.openfaas.OpenFaasHook"></a>

## OpenFaasHook Objects

```python
class OpenFaasHook(BaseHook)
```

Interact with OpenFaaS to query, deploy, invoke and update function

**Arguments**:

- `function_name`: Name of the function, Defaults to None
- `conn_id`: openfaas connection to use, Defaults to open_faas_default
for example host : http://openfaas.faas.com, Connection Type : Http

<a id="hooks.openfaas.OpenFaasHook.deploy_function"></a>

#### deploy\_function

```python
def deploy_function(overwrite_function_if_exist: bool,
                    body: Dict[str, Any]) -> None
```

Deploy OpenFaaS function

<a id="hooks.openfaas.OpenFaasHook.invoke_async_function"></a>

#### invoke\_async\_function

```python
def invoke_async_function(body: Dict[str, Any]) -> None
```

Invoking function asynchronously

<a id="hooks.openfaas.OpenFaasHook.invoke_function"></a>

#### invoke\_function

```python
def invoke_function(body: Dict[str, Any]) -> None
```

Invoking function synchronously, will block until function completes and returns

<a id="hooks.openfaas.OpenFaasHook.update_function"></a>

#### update\_function

```python
def update_function(body: Dict[str, Any]) -> None
```

Update OpenFaaS function

<a id="hooks.openfaas.OpenFaasHook.does_function_exist"></a>

#### does\_function\_exist

```python
def does_function_exist() -> bool
```

Whether OpenFaaS function exists or not

