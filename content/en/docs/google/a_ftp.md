---
title: "ftp"
linkTitle: "ftp"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     ftp Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.ftp"></a>

# sensors.ftp

<a id="sensors.ftp.FTPSensor"></a>

## FTPSensor Objects

```python
class FTPSensor(BaseSensorOperator)
```

Waits for a file or directory to be present on FTP.

**Arguments**:

- `path`: Remote file or directory path
- `fail_on_transient_errors`: Fail on all errors,
including 4xx transient errors. Default True.
- `ftp_conn_id`: The :ref:`ftp connection id <howto/connection:ftp>`
reference to run the sensor against.

<a id="sensors.ftp.FTPSensor.template_fields"></a>

#### template\_fields

Errors that are transient in nature, and where action can be retried

<a id="sensors.ftp.FTPSSensor"></a>

## FTPSSensor Objects

```python
class FTPSSensor(FTPSensor)
```

Waits for a file or directory to be present on FTP over SSL.

<a id="hooks"></a>

# hooks

<a id="hooks.ftp"></a>

# hooks.ftp

<a id="hooks.ftp.FTPHook"></a>

## FTPHook Objects

```python
class FTPHook(BaseHook)
```

Interact with FTP.

Errors that may occur throughout but should be handled downstream.
You can specify mode for data transfers in the extra field of your
connection as ``{"passive": "true"}``.

**Arguments**:

- `ftp_conn_id`: The :ref:`ftp connection id <howto/connection:ftp>`
reference.

<a id="hooks.ftp.FTPHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> ftplib.FTP
```

Returns a FTP connection object

<a id="hooks.ftp.FTPHook.close_conn"></a>

#### close\_conn

```python
def close_conn()
```

Closes the connection. An error will occur if the
connection wasn't ever opened.

<a id="hooks.ftp.FTPHook.describe_directory"></a>

#### describe\_directory

```python
def describe_directory(path: str) -> dict
```

Returns a dictionary of {filename: {attributes}} for all files

on the remote system (where the MLSD command is supported).

**Arguments**:

- `path`: full path to the remote directory

<a id="hooks.ftp.FTPHook.list_directory"></a>

#### list\_directory

```python
def list_directory(path: str) -> List[str]
```

Returns a list of files on the remote system.

**Arguments**:

- `path`: full path to the remote directory to list

<a id="hooks.ftp.FTPHook.create_directory"></a>

#### create\_directory

```python
def create_directory(path: str) -> None
```

Creates a directory on the remote system.

**Arguments**:

- `path`: full path to the remote directory to create

<a id="hooks.ftp.FTPHook.delete_directory"></a>

#### delete\_directory

```python
def delete_directory(path: str) -> None
```

Deletes a directory on the remote system.

**Arguments**:

- `path`: full path to the remote directory to delete

<a id="hooks.ftp.FTPHook.retrieve_file"></a>

#### retrieve\_file

```python
def retrieve_file(remote_full_path, local_full_path_or_buffer, callback=None)
```

Transfers the remote file to a local location.

If local_full_path_or_buffer is a string path, the file will be put
at that location; if it is a file-like buffer, the file will
be written to the buffer but not closed.

**Arguments**:

- `remote_full_path`: full path to the remote file
- `local_full_path_or_buffer`: full path to the local file or a
file-like buffer
- `callback`: callback which is called each time a block of data
is read. if you do not use a callback, these blocks will be written
    to the file or buffer passed in. if you do pass in a callback, note
    that writing to a file or buffer will need to be handled inside the
    callback.
    [default: output_handle.write()]

.. code-block:: python

    hook = FTPHook(ftp_conn_id="my_conn")

    remote_path = "/path/to/remote/file"
    local_path = "/path/to/local/file"

    # with a custom callback (in this case displaying progress on each read)
    def print_progress(percent_progress):
        self.log.info("Percent Downloaded: %s%%" % percent_progress)


    total_downloaded = 0
    total_file_size = hook.get_size(remote_path)
    output_handle = open(local_path, "wb")


    def write_to_file_with_progress(data):
        total_downloaded += len(data)
        output_handle.write(data)
        percent_progress = (total_downloaded / total_file_size) * 100
        print_progress(percent_progress)


    hook.retrieve_file(remote_path, None, callback=write_to_file_with_progress)

    # without a custom callback data is written to the local_path
    hook.retrieve_file(remote_path, local_path)

<a id="hooks.ftp.FTPHook.store_file"></a>

#### store\_file

```python
def store_file(remote_full_path: str, local_full_path_or_buffer: Any) -> None
```

Transfers a local file to the remote location.

If local_full_path_or_buffer is a string path, the file will be read
from that location; if it is a file-like buffer, the file will
be read from the buffer but not closed.

**Arguments**:

- `remote_full_path`: full path to the remote file
- `local_full_path_or_buffer`: full path to the local file or a
file-like buffer

<a id="hooks.ftp.FTPHook.delete_file"></a>

#### delete\_file

```python
def delete_file(path: str) -> None
```

Removes a file on the FTP Server.

**Arguments**:

- `path`: full path to the remote file

<a id="hooks.ftp.FTPHook.rename"></a>

#### rename

```python
def rename(from_name: str, to_name: str) -> str
```

Rename a file.

**Arguments**:

- `from_name`: rename file from name
- `to_name`: rename file to name

<a id="hooks.ftp.FTPHook.get_mod_time"></a>

#### get\_mod\_time

```python
def get_mod_time(path: str) -> datetime.datetime
```

Returns a datetime object representing the last time the file was modified

**Arguments**:

- `path`: remote file path

<a id="hooks.ftp.FTPHook.get_size"></a>

#### get\_size

```python
def get_size(path: str) -> Optional[int]
```

Returns the size of a file (in bytes)

**Arguments**:

- `path`: remote file path

<a id="hooks.ftp.FTPHook.test_connection"></a>

#### test\_connection

```python
def test_connection() -> Tuple[bool, str]
```

Test the FTP connection by calling path with directory

<a id="hooks.ftp.FTPSHook"></a>

## FTPSHook Objects

```python
class FTPSHook(FTPHook)
```

Interact with FTPS.

<a id="hooks.ftp.FTPSHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> ftplib.FTP
```

Returns a FTPS connection object.

