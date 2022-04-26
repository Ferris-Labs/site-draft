---
title: "alibaba"
linkTitle: "alibaba"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     alibaba Plugin.
---


<a id="__init__"></a>

# \_\_init\_\_

<a id="cloud"></a>

# cloud

<a id="cloud.sensors.oss_key"></a>

# cloud.sensors.oss\_key

<a id="cloud.sensors.oss_key.OSSKeySensor"></a>

## OSSKeySensor Objects

```python
class OSSKeySensor(BaseSensorOperator)
```

Waits for a key (a file-like instance on OSS) to be present in a OSS bucket.

OSS being a key/value it does not support folders. The path is just a key
a resource.

**Arguments**:

- `bucket_key`: The key being waited on. Supports full oss:// style url
or relative path from root level. When it's specified as a full oss://
url, please leave bucket_name as `None`.
- `region`: OSS region
- `bucket_name`: OSS bucket name
- `oss_conn_id`: The Airflow connection used for OSS credentials.

<a id="cloud.sensors.oss_key.OSSKeySensor.get_hook"></a>

#### get\_hook

```python
@cached_property
def get_hook() -> OSSHook
```

Create and return an OSSHook

<a id="cloud.sensors"></a>

# cloud.sensors

<a id="cloud.operators"></a>

# cloud.operators

<a id="cloud.operators.oss"></a>

# cloud.operators.oss

This module contains Alibaba Cloud OSS operators.

<a id="cloud.operators.oss.OSSCreateBucketOperator"></a>

## OSSCreateBucketOperator Objects

```python
class OSSCreateBucketOperator(BaseOperator)
```

This operator creates an OSS bucket

**Arguments**:

- `region`: OSS region you want to create bucket
- `bucket_name`: This is bucket name you want to create
- `oss_conn_id`: The Airflow connection used for OSS credentials.

<a id="cloud.operators.oss.OSSDeleteBucketOperator"></a>

## OSSDeleteBucketOperator Objects

```python
class OSSDeleteBucketOperator(BaseOperator)
```

This operator to delete an OSS bucket

**Arguments**:

- `region`: OSS region you want to create bucket
- `bucket_name`: This is bucket name you want to delete
- `oss_conn_id`: The Airflow connection used for OSS credentials.

<a id="cloud.operators.oss.OSSUploadObjectOperator"></a>

## OSSUploadObjectOperator Objects

```python
class OSSUploadObjectOperator(BaseOperator)
```

This operator to upload an file-like object

**Arguments**:

- `key`: the OSS path of the object
- `file`: local file to upload.
- `region`: OSS region you want to create bucket
- `bucket_name`: This is bucket name you want to create
- `oss_conn_id`: The Airflow connection used for OSS credentials.

<a id="cloud.operators.oss.OSSDownloadObjectOperator"></a>

## OSSDownloadObjectOperator Objects

```python
class OSSDownloadObjectOperator(BaseOperator)
```

This operator to Download an OSS object

**Arguments**:

- `key`: key of the object to download.
- `local_file`: local path + file name to save.
- `region`: OSS region
- `bucket_name`: OSS bucket name
- `oss_conn_id`: The Airflow connection used for OSS credentials.

<a id="cloud.operators.oss.OSSDeleteBatchObjectOperator"></a>

## OSSDeleteBatchObjectOperator Objects

```python
class OSSDeleteBatchObjectOperator(BaseOperator)
```

This operator to delete OSS objects

**Arguments**:

- `key`: key list of the objects to delete.
- `region`: OSS region
- `bucket_name`: OSS bucket name
- `oss_conn_id`: The Airflow connection used for OSS credentials.

<a id="cloud.operators.oss.OSSDeleteObjectOperator"></a>

## OSSDeleteObjectOperator Objects

```python
class OSSDeleteObjectOperator(BaseOperator)
```

This operator to delete an OSS object

**Arguments**:

- `key`: key of the object to delete.
- `region`: OSS region
- `bucket_name`: OSS bucket name
- `oss_conn_id`: The Airflow connection used for OSS credentials.

<a id="cloud.example_dags"></a>

# cloud.example\_dags

<a id="cloud.example_dags.example_oss_object"></a>

# cloud.example\_dags.example\_oss\_object

<a id="cloud.example_dags.example_oss_bucket"></a>

# cloud.example\_dags.example\_oss\_bucket

<a id="cloud.hooks"></a>

# cloud.hooks

<a id="cloud.hooks.oss"></a>

# cloud.hooks.oss

<a id="cloud.hooks.oss.provide_bucket_name"></a>

#### provide\_bucket\_name

```python
def provide_bucket_name(func: T) -> T
```

Function decorator that unifies bucket name and key taken from the key
in case no bucket name and at least a key has been passed to the function.

<a id="cloud.hooks.oss.unify_bucket_name_and_key"></a>

#### unify\_bucket\_name\_and\_key

```python
def unify_bucket_name_and_key(func: T) -> T
```

Function decorator that unifies bucket name and key taken from the key
in case no bucket name and at least a key has been passed to the function.

<a id="cloud.hooks.oss.OSSHook"></a>

## OSSHook Objects

```python
class OSSHook(BaseHook)
```

Interact with Alibaba Cloud OSS, using the oss2 library.

<a id="cloud.hooks.oss.OSSHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> "Connection"
```

Returns connection for the hook.

<a id="cloud.hooks.oss.OSSHook.parse_oss_url"></a>

#### parse\_oss\_url

```python
@staticmethod
def parse_oss_url(ossurl: str) -> tuple
```

Parses the OSS Url into a bucket name and key.

**Arguments**:

- `ossurl`: The OSS Url to parse.

**Returns**:

the parsed bucket name and key

<a id="cloud.hooks.oss.OSSHook.object_exists"></a>

#### object\_exists

```python
@provide_bucket_name
@unify_bucket_name_and_key
def object_exists(key: str, bucket_name: Optional[str] = None) -> bool
```

Check if object exists.

**Arguments**:

- `key`: the path of the object
- `bucket_name`: the name of the bucket

**Returns**:

`bool`: True if it exists and False if not.

<a id="cloud.hooks.oss.OSSHook.get_bucket"></a>

#### get\_bucket

```python
@provide_bucket_name
def get_bucket(bucket_name: Optional[str] = None) -> oss2.api.Bucket
```

Returns a oss2.Bucket object

**Arguments**:

- `bucket_name`: the name of the bucket

**Returns**:

`oss2.api.Bucket`: the bucket object to the bucket name.

<a id="cloud.hooks.oss.OSSHook.load_string"></a>

#### load\_string

```python
@provide_bucket_name
@unify_bucket_name_and_key
def load_string(key: str,
                content: str,
                bucket_name: Optional[str] = None) -> None
```

Loads a string to OSS

**Arguments**:

- `key`: the path of the object
- `content`: str to set as content for the key.
- `bucket_name`: the name of the bucket

<a id="cloud.hooks.oss.OSSHook.upload_local_file"></a>

#### upload\_local\_file

```python
@provide_bucket_name
@unify_bucket_name_and_key
def upload_local_file(key: str,
                      file: str,
                      bucket_name: Optional[str] = None) -> None
```

Upload a local file to OSS

**Arguments**:

- `key`: the OSS path of the object
- `file`: local file to upload.
- `bucket_name`: the name of the bucket

<a id="cloud.hooks.oss.OSSHook.download_file"></a>

#### download\_file

```python
@provide_bucket_name
@unify_bucket_name_and_key
def download_file(key: str,
                  local_file: str,
                  bucket_name: Optional[str] = None) -> Optional[str]
```

Download file from OSS

**Arguments**:

- `key`: key of the file-like object to download.
- `local_file`: local path + file name to save.
- `bucket_name`: the name of the bucket

**Returns**:

`str`: the file name.

<a id="cloud.hooks.oss.OSSHook.delete_object"></a>

#### delete\_object

```python
@provide_bucket_name
@unify_bucket_name_and_key
def delete_object(key: str, bucket_name: Optional[str] = None) -> None
```

Delete object from OSS

**Arguments**:

- `key`: key of the object to delete.
- `bucket_name`: the name of the bucket

<a id="cloud.hooks.oss.OSSHook.delete_objects"></a>

#### delete\_objects

```python
@provide_bucket_name
@unify_bucket_name_and_key
def delete_objects(key: list, bucket_name: Optional[str] = None) -> None
```

Delete objects from OSS

**Arguments**:

- `key`: keys list of the objects to delete.
- `bucket_name`: the name of the bucket

<a id="cloud.hooks.oss.OSSHook.delete_bucket"></a>

#### delete\_bucket

```python
@provide_bucket_name
def delete_bucket(bucket_name: Optional[str] = None) -> None
```

Delete bucket from OSS

**Arguments**:

- `bucket_name`: the name of the bucket

<a id="cloud.hooks.oss.OSSHook.create_bucket"></a>

#### create\_bucket

```python
@provide_bucket_name
def create_bucket(bucket_name: Optional[str] = None) -> None
```

Create bucket

**Arguments**:

- `bucket_name`: the name of the bucket

<a id="cloud.hooks.oss.OSSHook.append_string"></a>

#### append\_string

```python
@provide_bucket_name
@unify_bucket_name_and_key
def append_string(bucket_name: Optional[str], content: str, key: str,
                  pos: int) -> None
```

Append string to a remote existing file

**Arguments**:

- `bucket_name`: the name of the bucket
- `content`: content to be appended
- `key`: oss bucket key
- `pos`: position of the existing file where the content will be appended

<a id="cloud.hooks.oss.OSSHook.read_key"></a>

#### read\_key

```python
@provide_bucket_name
@unify_bucket_name_and_key
def read_key(bucket_name: Optional[str], key: str) -> str
```

Read oss remote object content with the specified key

**Arguments**:

- `bucket_name`: the name of the bucket
- `key`: oss bucket key

<a id="cloud.hooks.oss.OSSHook.head_key"></a>

#### head\_key

```python
@provide_bucket_name
@unify_bucket_name_and_key
def head_key(bucket_name: Optional[str],
             key: str) -> oss2.models.HeadObjectResult
```

Get meta info of the specified remote object

**Arguments**:

- `bucket_name`: the name of the bucket
- `key`: oss bucket key

<a id="cloud.hooks.oss.OSSHook.key_exist"></a>

#### key\_exist

```python
@provide_bucket_name
@unify_bucket_name_and_key
def key_exist(bucket_name: Optional[str], key: str) -> bool
```

Find out whether the specified key exists in the oss remote storage

**Arguments**:

- `bucket_name`: the name of the bucket
- `key`: oss bucket key

<a id="cloud.log"></a>

# cloud.log

<a id="cloud.log.oss_task_handler"></a>

# cloud.log.oss\_task\_handler

<a id="cloud.log.oss_task_handler.OSSTaskHandler"></a>

## OSSTaskHandler Objects

```python
class OSSTaskHandler(FileTaskHandler, LoggingMixin)
```

OSSTaskHandler is a python log handler that handles and reads
task instance logs. It extends airflow FileTaskHandler and
uploads to and reads from OSS remote storage.

<a id="cloud.log.oss_task_handler.OSSTaskHandler.close"></a>

#### close

```python
def close()
```

Close and upload local log file to remote storage OSS.

<a id="cloud.log.oss_task_handler.OSSTaskHandler.oss_log_exists"></a>

#### oss\_log\_exists

```python
def oss_log_exists(remote_log_location)
```

Check if remote_log_location exists in remote storage

**Arguments**:

- `remote_log_location`: log's location in remote storage

**Returns**:

True if location exists else False

<a id="cloud.log.oss_task_handler.OSSTaskHandler.oss_read"></a>

#### oss\_read

```python
def oss_read(remote_log_location, return_error=False)
```

Returns the log found at the remote_log_location. Returns '' if no

logs are found or there is an error.

**Arguments**:

- `remote_log_location`: the log's location in remote storage
- `return_error`: if True, returns a string error message if an
error occurs. Otherwise returns '' when an error occurs.

<a id="cloud.log.oss_task_handler.OSSTaskHandler.oss_write"></a>

#### oss\_write

```python
def oss_write(log, remote_log_location, append=True)
```

Writes the log to the remote_log_location. Fails silently if no hook

was created.

**Arguments**:

- `log`: the log to write to the remote_log_location
- `remote_log_location`: the log's location in remote storage
- `append`: if False, any existing log file is overwritten. If True,
the new log is appended to any existing logs.

