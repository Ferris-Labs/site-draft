---
title: "ssh"
linkTitle: "ssh"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     ssh Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.ssh"></a>

# operators.ssh

<a id="operators.ssh.SSHOperator"></a>

## SSHOperator Objects

```python
class SSHOperator(BaseOperator)
```

SSHOperator to execute commands on given remote host using the ssh_hook.

**Arguments**:

- `ssh_hook`: predefined ssh_hook to use for remote execution.
Either `ssh_hook` or `ssh_conn_id` needs to be provided.
- `ssh_conn_id`: :ref:`ssh connection id<howto/connection:ssh>`
from airflow Connections. `ssh_conn_id` will be ignored if
`ssh_hook` is provided.
- `remote_host`: remote host to connect (templated)
Nullable. If provided, it will replace the `remote_host` which was
defined in `ssh_hook` or predefined in the connection of `ssh_conn_id`.
- `command`: command to execute on remote host. (templated)
- `conn_timeout`: timeout (in seconds) for maintaining the connection. The default is 10 seconds.
Nullable. If provided, it will replace the `conn_timeout` which was
predefined in the connection of `ssh_conn_id`.
- `cmd_timeout`: timeout (in seconds) for executing the command. The default is 10 seconds.
- `timeout`: (deprecated) timeout (in seconds) for executing the command. The default is 10 seconds.
Use conn_timeout and cmd_timeout parameters instead.
- `environment`: a dict of shell environment variables. Note that the
server will reject them silently if `AcceptEnv` is not set in SSH config.
- `get_pty`: request a pseudo-terminal from the server. Set to ``True``
to have the remote process killed upon task timeout.
The default is ``False`` but note that `get_pty` is forced to ``True``
when the `command` starts with ``sudo``.
- `banner_timeout`: timeout to wait for banner from the server in seconds

<a id="operators.ssh.SSHOperator.tunnel"></a>

#### tunnel

```python
def tunnel() -> None
```

Get ssh tunnel

<a id="hooks"></a>

# hooks

<a id="hooks.ssh"></a>

# hooks.ssh

Hook for SSH connections.

<a id="hooks.ssh.SSHHook"></a>

## SSHHook Objects

```python
class SSHHook(BaseHook)
```

Hook for ssh remote execution using Paramiko.

ref: https://github.com/paramiko/paramiko
This hook also lets you create ssh tunnel and serve as basis for SFTP file transfer

**Arguments**:

- `ssh_conn_id`: :ref:`ssh connection id<howto/connection:ssh>` from airflow
Connections from where all the required parameters can be fetched like
username, password or key_file. Thought the priority is given to the
param passed during init
- `remote_host`: remote host to connect
- `username`: username to connect to the remote_host
- `password`: password of the username to connect to the remote_host
- `key_file`: path to key file to use to connect to the remote_host
- `port`: port of remote host to connect (Default is paramiko SSH_PORT)
- `conn_timeout`: timeout (in seconds) for the attempt to connect to the remote_host.
The default is 10 seconds. If provided, it will replace the `conn_timeout` which was
predefined in the connection of `ssh_conn_id`.
- `timeout`: (Deprecated). timeout for the attempt to connect to the remote_host.
Use conn_timeout instead.
- `keepalive_interval`: send a keepalive packet to remote host every
keepalive_interval seconds
- `banner_timeout`: timeout to wait for banner from the server in seconds

<a id="hooks.ssh.SSHHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.ssh.SSHHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> paramiko.SSHClient
```

Opens a ssh connection to the remote host.


<a id="hooks.ssh.SSHHook.get_tunnel"></a>

#### get\_tunnel

```python
def get_tunnel(remote_port: int,
               remote_host: str = "localhost",
               local_port: Optional[int] = None) -> SSHTunnelForwarder
```

Creates a tunnel between two hosts. Like ssh -L <LOCAL_PORT>:host:<REMOTE_PORT>.

**Arguments**:

- `remote_port`: The remote port to create a tunnel to
- `remote_host`: The remote host to create a tunnel to (default localhost)
- `local_port`: The local port to attach the tunnel to

**Returns**:

sshtunnel.SSHTunnelForwarder object

<a id="hooks.ssh.SSHHook.create_tunnel"></a>

#### create\_tunnel

```python
def create_tunnel(local_port: int,
                  remote_port: int,
                  remote_host: str = "localhost") -> SSHTunnelForwarder
```

Creates tunnel for SSH connection [Deprecated].

**Arguments**:

- `local_port`: local port number
- `remote_port`: remote port number
- `remote_host`: remote host

