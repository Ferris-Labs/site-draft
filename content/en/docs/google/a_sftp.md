---
title: "sftp"
linkTitle: "sftp"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     sftp Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.sftp"></a>

# sensors.sftp

This module contains SFTP sensor.

<a id="sensors.sftp.SFTPSensor"></a>

## SFTPSensor Objects

```python
class SFTPSensor(BaseSensorOperator)
```

Waits for a file or directory to be present on SFTP.

**Arguments**:

- `path`: Remote file or directory path
- `sftp_conn_id`: The connection to run the sensor against

<a id="operators"></a>

# operators

<a id="operators.sftp"></a>

# operators.sftp

This module contains SFTP operator.

<a id="operators.sftp.SFTPOperation"></a>

## SFTPOperation Objects

```python
class SFTPOperation()
```

Operation that can be used with SFTP/

<a id="operators.sftp.SFTPOperator"></a>

## SFTPOperator Objects

```python
class SFTPOperator(BaseOperator)
```

SFTPOperator for transferring files from remote host to local or vice a versa.

This operator uses ssh_hook to open sftp transport channel that serve as basis
for file transfer.

**Arguments**:

- `ssh_hook`: predefined ssh_hook to use for remote execution.
Either `ssh_hook` or `ssh_conn_id` needs to be provided.
- `ssh_conn_id`: :ref:`ssh connection id<howto/connection:ssh>`
from airflow Connections. `ssh_conn_id` will be ignored if `ssh_hook`
is provided.
- `remote_host`: remote host to connect (templated)
Nullable. If provided, it will replace the `remote_host` which was
defined in `ssh_hook` or predefined in the connection of `ssh_conn_id`.
- `local_filepath`: local file path to get or put. (templated)
- `remote_filepath`: remote file path to get or put. (templated)
- `operation`: specify operation 'get' or 'put', defaults to put
- `confirm`: specify if the SFTP operation should be confirmed, defaults to True
- `create_intermediate_dirs`: create missing intermediate directories when
copying from remote to local and vice-versa. Default is False.

Example: The following task would copy ``file.txt`` to the remote host
at ``/tmp/tmp1/tmp2/`` while creating ``tmp``,``tmp1`` and ``tmp2`` if they
don't exist. If the parameter is not passed it would error as the directory
does not exist. ::

    put_file = SFTPOperator(
        task_id="test_sftp",
        ssh_conn_id="ssh_default",
        local_filepath="/tmp/file.txt",
        remote_filepath="/tmp/tmp1/tmp2/file.txt",
        operation="put",
        create_intermediate_dirs=True,
        dag=dag
    )

<a id="hooks"></a>

# hooks

<a id="hooks.sftp"></a>

# hooks.sftp

This module contains SFTP hook.

<a id="hooks.sftp.SFTPHook"></a>

## SFTPHook Objects

```python
class SFTPHook(SSHHook)
```

This hook is inherited from SSH hook. Please refer to SSH hook for the input

arguments.

Interact with SFTP.

**Arguments**:

- `ssh_conn_id`: The :ref:`sftp connection id<howto/connection:sftp>`
- `(Outdated)` (`ftp_conn_id`): The :ref:`sftp connection id<howto/connection:sftp>`

<a id="hooks.sftp.SFTPHook.get_conn"></a>

#### get\_conn

```python
@tenacity.retry(
    stop=tenacity.stop_after_delay(10),
    wait=tenacity.wait_exponential(multiplier=1, max=10),
    retry=tenacity.retry_if_exception_type(SSHException),
    reraise=True,
)
def get_conn() -> pysftp.Connection
```

Returns an SFTP connection object

<a id="hooks.sftp.SFTPHook.close_conn"></a>

#### close\_conn

```python
def close_conn() -> None
```

Closes the connection

<a id="hooks.sftp.SFTPHook.describe_directory"></a>

#### describe\_directory

```python
def describe_directory(path: str) -> Dict[str, Dict[str, str]]
```

Returns a dictionary of {filename: {attributes}} for all files

on the remote system (where the MLSD command is supported).

**Arguments**:

- `path`: full path to the remote directory

<a id="hooks.sftp.SFTPHook.list_directory"></a>

#### list\_directory

```python
def list_directory(path: str) -> List[str]
```

Returns a list of files on the remote system.

**Arguments**:

- `path`: full path to the remote directory to list

<a id="hooks.sftp.SFTPHook.create_directory"></a>

#### create\_directory

```python
def create_directory(path: str, mode: int = 777) -> None
```

Creates a directory on the remote system.

**Arguments**:

- `path`: full path to the remote directory to create
- `mode`: int representation of octal mode for directory

<a id="hooks.sftp.SFTPHook.delete_directory"></a>

#### delete\_directory

```python
def delete_directory(path: str) -> None
```

Deletes a directory on the remote system.

**Arguments**:

- `path`: full path to the remote directory to delete

<a id="hooks.sftp.SFTPHook.retrieve_file"></a>

#### retrieve\_file

```python
def retrieve_file(remote_full_path: str, local_full_path: str) -> None
```

Transfers the remote file to a local location.

If local_full_path is a string path, the file will be put
at that location

**Arguments**:

- `remote_full_path`: full path to the remote file
- `local_full_path`: full path to the local file

<a id="hooks.sftp.SFTPHook.store_file"></a>

#### store\_file

```python
def store_file(remote_full_path: str, local_full_path: str) -> None
```

Transfers a local file to the remote location.

If local_full_path_or_buffer is a string path, the file will be read
from that location

**Arguments**:

- `remote_full_path`: full path to the remote file
- `local_full_path`: full path to the local file

<a id="hooks.sftp.SFTPHook.delete_file"></a>

#### delete\_file

```python
def delete_file(path: str) -> None
```

Removes a file on the FTP Server

**Arguments**:

- `path`: full path to the remote file

<a id="hooks.sftp.SFTPHook.get_mod_time"></a>

#### get\_mod\_time

```python
def get_mod_time(path: str) -> str
```

Returns modification time.

**Arguments**:

- `path`: full path to the remote file

<a id="hooks.sftp.SFTPHook.path_exists"></a>

#### path\_exists

```python
def path_exists(path: str) -> bool
```

Returns True if a remote entity exists

**Arguments**:

- `path`: full path to the remote file or directory

<a id="hooks.sftp.SFTPHook.get_tree_map"></a>

#### get\_tree\_map

```python
def get_tree_map(path: str,
                 prefix: Optional[str] = None,
                 delimiter: Optional[str] = None
                 ) -> Tuple[List[str], List[str], List[str]]
```

Return tuple with recursive lists of files, directories and unknown paths from given path.

It is possible to filter results by giving prefix and/or delimiter parameters.

**Arguments**:

- `path`: path from which tree will be built
- `prefix`: if set paths will be added if start with prefix
- `delimiter`: if set paths will be added if end with delimiter

**Returns**:

`Tuple[List[str], List[str], List[str]]`: tuple with list of files, dirs and unknown items

<a id="hooks.sftp.SFTPHook.test_connection"></a>

#### test\_connection

```python
def test_connection() -> Tuple[bool, str]
```

Test the SFTP connection by calling path with directory

