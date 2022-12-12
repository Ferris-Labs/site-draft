---
title: "singularity"
linkTitle: "singularity"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     singularity Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.singularity"></a>

# operators.singularity

<a id="operators.singularity.SingularityOperator"></a>

## SingularityOperator Objects

```python
class SingularityOperator(BaseOperator)
```

Execute a command inside a Singularity container

Singularity has more seamless connection to the host than Docker, so
no special binds are needed to ensure binding content in the user $HOME
and temporary directories. If the user needs custom binds, this can
be done with --volumes

**Arguments**:

- `image`: Singularity image or URI from which to create the container.
- `auto_remove`: Delete the container when the process exits.
The default is False.
- `command`: Command to be run in the container. (templated)
- `start_command`: Start command to pass to the container instance.
- `environment`: Environment variables to set in the container. (templated)
- `working_dir`: Set a working directory for the instance.
- `force_pull`: Pull the image on every run. Default is False.
- `volumes`: List of volumes to mount into the container, e.g.
``['/host/path:/container/path', '/host/path2:/container/path2']``.
- `options`: Other flags (list) to provide to the instance start.
- `working_dir`: Working directory to
set on the container (equivalent to the -w switch the docker client).

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_singularity"></a>

# example\_dags.example\_singularity

