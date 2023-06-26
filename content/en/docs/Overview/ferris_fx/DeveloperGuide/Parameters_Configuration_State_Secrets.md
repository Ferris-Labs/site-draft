---
title: "Parameters and Configurations"
linkTitle: "Parameters and Configurations"
weight: 204
description: >-
     Retrieve Parameters and Configurations using ferris_ef module.
---


# The FERRIS Executor Helper

 The `ferris_ef` package can be used for fetching package's configuration, parameters, secrets and state through its context.
 
```python
from ferris_ef import context
```

### Accessing package configuration

```python
from ferris_ef import context

context.config.get('some_configuration_key')
```

To create a configuration set just place a `config.json` in your service directory. Ferris loads and maintains it in Consul.

The following is a sample configuration file.

```json
{
  "my_simple_attribute": "my_db_host_name",
  "my_configuration_array": ["a","b","c"],
  "my_configuration_dictionary": {
    "alias": "johndoe",
    "first_name": "john"
  }
}
```
As illustrated above the configuration may contain simple attributes, dictionaries and arrays.


### Accessing execution parameters

You can access execution parameters as shown below.

```python
from ferris_ef import context

context.params.get('param_name')
```

These parameters are populated from the `data` section of the trigerring CloudEvent or from the values entered in the form attached to the service. Please review section [Service UI generation](/docs/overview/ferris_fx/developerguide/"ui_generator")

An example CloudEvent:

```json
{
    "specversion" : "1.0",
    "type" : "com.example.someevent", // The Event Type
    "source" : "/mycontext",
    "subject": null,
    "id" : "C234-1234-1234",
    "time" : "2018-04-05T17:31:00Z",
    "datacontenttype" : "application/json",
    "data" : {                       // The event payload as JSON
        "appinfoA" : "abc",
        "appinfoB" : 123,
        "appinfoC" : true
    }
}
```

In the next section we discuss Secrets Storage and Retreival and passing state between executions of a service.

### Accessing secrets

With `ferris_ef.context.secrets` you can access secrets stored on platform, project or package level.    

```python
from ferris_ef import context

context.secrets.get('secret_name')
```

This command will first lookup for secret named `secret_name` within package secrets (defined in `secrets.json` file of the package). If such key doesn't exist it will lookup for it within project secrets, and finally within platform's secrets. If secret with such name doesn't exist `None` will be returned.

### Setting secrets

Using `ferris_ef.context.secrets.set(name, value, context)` method you can set secrets on project and platform level.   

```python
from ferris_ef import context

context.secrets.set(name="platform_secret", value={"somekey":"someval"}, context="platform")
```

| Parameter | Description                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| name | Name of the secret to be set. If secret with the same name already exist it will be updated |
| value | Value of the secret that should be set |
| context | Context of the secret. Possible values are `platform` and `project` |


### Accessing package id and name

```python
from ferris_ef import context

context.package.name
context.package.id
```

### Accessing and updating package state

```python
from ferris_ef import context

context.state.get()
context.state.put("some_key", "some_value")
```


## Using `ferris_ef` for local development

To use `ferris_ef` for local development and testing without need to run scripts through Executor `EF_ENV=local` env variable must be set. When it is set `ferris_ef.context` will be read from local file `ef_env.json` that must be created within same directory as the script that is accessing `ferris_ef.context`.  
`ef_env.json` must have following structure:

```json
{
  "params": {
    "package_name": "some_package_name",
    "package_id": "some_package_id",
    "optional_param_1": "param_1_value",
    "optional_param_2": "param_2_value"
  },
  "secrets": {
    "secret_param_1": "secret_1_value",
    "secret_param_2": "secret_2_value"
  },
  "config": {
    "config_param_1": "config_1_value",
    "config_param_2": "config_2_value"
  }
}
```

NOTE: `params`, `package_name` and `package_id` are mandatory.

When `EF_ENV=local` is set, package state is also stored and fetched from the local file `ef_package_state.json` within the same directory. If file does not exist it will be created on the fly. 
