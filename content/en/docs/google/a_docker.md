---
title: "docker"
linkTitle: "docker"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     docker Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.docker"></a>

# operators.docker

Implements Docker operator

<a id="operators.docker.stringify"></a>

#### stringify

```python
def stringify(line: Union[str, bytes])
```

Make sure string is returned even if bytes are passed. Docker stream can return bytes.

<a id="operators.docker.DockerOperator"></a>

## DockerOperator Objects

```python
class DockerOperator(BaseOperator)
```

Execute a command inside a docker container.

By default, a temporary directory is
created on the host and mounted into a container to allow storing files
that together exceed the default disk size of 10GB in a container.
In this case The path to the mounted directory can be accessed
via the environment variable ``AIRFLOW_TMP_DIR``.

If the volume cannot be mounted, warning is printed and an attempt is made to execute the docker
command without the temporary folder mounted. This is to make it works by default with remote docker
engine or when you run docker-in-docker solution and temporary directory is not shared with the
docker engine. Warning is printed in logs in this case.

If you know you run DockerOperator with remote engine or via docker-in-docker
you should set ``mount_tmp_dir`` parameter to False. In this case, you can still use
``mounts`` parameter to mount already existing named volumes in your Docker Engine
to achieve similar capability where you can store files exceeding default disk size
of the container,

If a login to a private registry is required prior to pulling the image, a
Docker connection needs to be configured in Airflow and the connection ID
be provided with the parameter ``docker_conn_id``.

**Arguments**:

- `image`: Docker image from which to create the container.
If image tag is omitted, "latest" will be used. (templated)
- `api_version`: Remote API version. Set to ``auto`` to automatically
detect the server's version.
- `command`: Command to be run in the container. (templated)
- `container_name`: Name of the container. Optional (templated)
- `cpus`: Number of CPUs to assign to the container.
This value gets multiplied with 1024. See
https://docs.docker.com/engine/reference/run/`cpu`-share-constraint
- `docker_url`: URL of the host running the docker daemon.
Default is unix://var/run/docker.sock
- `environment`: Environment variables to set in the container. (templated)
- `private_environment`: Private environment variables to set in the container.
These are not templated, and hidden from the website.
- `force_pull`: Pull the docker image on every run. Default is False.
- `mem_limit`: Maximum amount of memory the container can use.
Either a float value, which represents the limit in bytes,
or a string like ``128m`` or ``1g``.
- `host_tmp_dir`: Specify the location of the temporary directory on the host which will
be mapped to tmp_dir. If not provided defaults to using the standard system temp directory.
- `network_mode`: Network mode for the container.
It can be one of the following:
bridge - Create new network stack for the container with default docker bridge network
None - No networking for this container
container:<name|id> - Use the network stack of another container specified via <name|id>
host - Use the host network stack. Incompatible with `port_bindings`
'<network-name>|<network-id>' - Connects the container to user created network
(using `docker network create` command)
- `tls_ca_cert`: Path to a PEM-encoded certificate authority
to secure the docker connection.
- `tls_client_cert`: Path to the PEM-encoded certificate
used to authenticate docker client.
- `tls_client_key`: Path to the PEM-encoded key used to authenticate docker client.
- `tls_hostname`: Hostname to match against
the docker server certificate or False to disable the check.
- `tls_ssl_version`: Version of SSL to use when communicating with docker daemon.
- `mount_tmp_dir`: Specify whether the temporary directory should be bind-mounted
from the host to the container. Defaults to True
- `tmp_dir`: Mount point inside the container to
a temporary directory created on the host by the operator.
The path is also made available via the environment variable
``AIRFLOW_TMP_DIR`` inside the container.
- `user`: Default user inside the docker container.
- `mounts`: List of volumes to mount into the container. Each item should
be a :py:class:`docker.types.Mount` instance.
- `entrypoint`: Overwrite the default ENTRYPOINT of the image
- `working_dir`: Working directory to
set on the container (equivalent to the -w switch the docker client)
- `xcom_all`: Push all the stdout or just the last line.
The default is False (last line).
- `docker_conn_id`: The :ref:`Docker connection id <howto/connection:docker>`
- `dns`: Docker custom DNS servers
- `dns_search`: Docker custom DNS search domain
- `auto_remove`: Auto-removal of the container on daemon side when the
container's process exits.
The default is False.
- `shm_size`: Size of ``/dev/shm`` in bytes. The size must be
greater than 0. If omitted uses system default.
- `tty`: Allocate pseudo-TTY to the container
This needs to be set see logs of the Docker container.
- `privileged`: Give extended privileges to this container.
- `cap_add`: Include container capabilities
- `retrieve_output`: Should this docker image consistently attempt to pull from and output
file before manually shutting down the image. Useful for cases where users want a pickle serialized
output that is not posted to logs
- `retrieve_output_path`: path for output file that will be retrieved and passed to xcom

<a id="operators.docker.DockerOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> DockerHook
```

Retrieves hook for the operator.

**Returns**:

The Docker Hook

<a id="operators.docker.DockerOperator.format_command"></a>

#### format\_command

```python
@staticmethod
def format_command(command: Union[str, List[str]]) -> Union[List[str], str]
```

Retrieve command(s). if command string starts with [, it returns the command list)

**Arguments**:

- `command`: Docker command or entrypoint

**Returns**:

`str | List[str]`: the command (or commands)

<a id="operators.docker_swarm"></a>

# operators.docker\_swarm

Run ephemeral Docker Swarm services

<a id="operators.docker_swarm.DockerSwarmOperator"></a>

## DockerSwarmOperator Objects

```python
class DockerSwarmOperator(DockerOperator)
```

Execute a command as an ephemeral docker swarm service.

Example use-case - Using Docker Swarm orchestration to make one-time
scripts highly available.

A temporary directory is created on the host and
mounted into a container to allow storing files
that together exceed the default disk size of 10GB in a container.
The path to the mounted directory can be accessed
via the environment variable ``AIRFLOW_TMP_DIR``.

If a login to a private registry is required prior to pulling the image, a
Docker connection needs to be configured in Airflow and the connection ID
be provided with the parameter ``docker_conn_id``.

**Arguments**:

- `image`: Docker image from which to create the container.
If image tag is omitted, "latest" will be used.
- `api_version`: Remote API version. Set to ``auto`` to automatically
detect the server's version.
- `auto_remove`: Auto-removal of the container on daemon side when the
container's process exits.
The default is False.
- `command`: Command to be run in the container. (templated)
- `docker_url`: URL of the host running the docker daemon.
Default is unix://var/run/docker.sock
- `environment`: Environment variables to set in the container. (templated)
- `force_pull`: Pull the docker image on every run. Default is False.
- `mem_limit`: Maximum amount of memory the container can use.
Either a float value, which represents the limit in bytes,
or a string like ``128m`` or ``1g``.
- `tls_ca_cert`: Path to a PEM-encoded certificate authority
to secure the docker connection.
- `tls_client_cert`: Path to the PEM-encoded certificate
used to authenticate docker client.
- `tls_client_key`: Path to the PEM-encoded key used to authenticate docker client.
- `tls_hostname`: Hostname to match against
the docker server certificate or False to disable the check.
- `tls_ssl_version`: Version of SSL to use when communicating with docker daemon.
- `tmp_dir`: Mount point inside the container to
a temporary directory created on the host by the operator.
The path is also made available via the environment variable
``AIRFLOW_TMP_DIR`` inside the container.
- `user`: Default user inside the docker container.
- `docker_conn_id`: The :ref:`Docker connection id <howto/connection:docker>`
- `tty`: Allocate pseudo-TTY to the container of this service
This needs to be set see logs of the Docker container / service.
- `enable_logging`: Show the application's logs in operator's logs.
Supported only if the Docker engine is using json-file or journald logging drivers.
The `tty` parameter should be set to use this with Python applications.
- `configs`: List of docker configs to be exposed to the containers of the swarm service.
The configs are ConfigReference objects as per the docker api
[https://docker-py.readthedocs.io/en/stable/services.html#docker.models.services.ServiceCollection.create]_
- `secrets`: List of docker secrets to be exposed to the containers of the swarm service.
The secrets are SecretReference objects as per the docker create_service api.
[https://docker-py.readthedocs.io/en/stable/services.html#docker.models.services.ServiceCollection.create]_
- `mode`: Indicate whether a service should be deployed as a replicated or global service,
and associated parameters
- `networks`: List of network names or IDs or NetworkAttachmentConfig to attach the service to.
- `placement`: Placement instructions for the scheduler. If a list is passed instead,
it is assumed to be a list of constraints as part of a Placement object.

<a id="decorators"></a>

# decorators

<a id="decorators.docker"></a>

# decorators.docker

<a id="decorators.docker.docker_task"></a>

#### docker\_task

