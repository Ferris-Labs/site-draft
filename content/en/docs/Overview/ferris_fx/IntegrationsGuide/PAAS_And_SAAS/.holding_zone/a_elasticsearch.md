---
title: "elasticsearch"
linkTitle: "elasticsearch"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     elasticsearch Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_elasticsearch_query"></a>

# example\_dags.example\_elasticsearch\_query

<a id="example_dags.example_elasticsearch_query.show_tables"></a>

#### show\_tables

```python
@task(task_id='es_print_tables')
def show_tables()
```

show_tables queries elasticsearch to list available tables

<a id="hooks"></a>

# hooks

<a id="hooks.elasticsearch"></a>

# hooks.elasticsearch

<a id="hooks.elasticsearch.ElasticsearchHook"></a>

## ElasticsearchHook Objects

```python
class ElasticsearchHook(DbApiHook)
```

Interact with Elasticsearch through the elasticsearch-dbapi.

This hook uses the Elasticsearch conn_id.

**Arguments**:

- `elasticsearch_conn_id`: The :ref:`ElasticSearch connection id <howto/connection:elasticsearch>`
used for Elasticsearch credentials.

<a id="hooks.elasticsearch.ElasticsearchHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> ESConnection
```

Returns a elasticsearch connection object

<a id="log"></a>

# log

<a id="log.es_task_handler"></a>

# log.es\_task\_handler

<a id="log.es_task_handler.ElasticsearchTaskHandler"></a>

## ElasticsearchTaskHandler Objects

```python
class ElasticsearchTaskHandler(FileTaskHandler, ExternalLoggingMixin,
                               LoggingMixin)
```

ElasticsearchTaskHandler is a python log handler that
reads logs from Elasticsearch. Note that Airflow does not handle the indexing
of logs into Elasticsearch. Instead, Airflow flushes logs
into local files. Additional software setup is required
to index the logs into Elasticsearch, such as using
Filebeat and Logstash.
To efficiently query and sort Elasticsearch results, this handler assumes each
log message has a field `log_id` consists of ti primary keys:
`log_id = {dag_id}-{task_id}-{execution_date}-{try_number}`
Log messages with specific log_id are sorted based on `offset`,
which is a unique integer indicates log message's order.
Timestamps here are unreliable because multiple log messages
might have the same timestamp.

<a id="log.es_task_handler.ElasticsearchTaskHandler.__init__"></a>

#### \_\_init\_\_

```python
def __init__(
    base_log_folder: str,
    filename_template: str,
    log_id_template: str,
    end_of_log_mark: str,
    write_stdout: bool,
    json_format: bool,
    json_fields: str,
    host_field: str = "host",
    offset_field: str = "offset",
    host: str = "localhost:9200",
    frontend: str = "localhost:5601",
    es_kwargs: Optional[dict] = conf.getsection("elasticsearch_configs"))
```

**Arguments**:

- `base_log_folder`: base folder to store logs locally
- `log_id_template`: log id template
- `host`: Elasticsearch host name

<a id="log.es_task_handler.ElasticsearchTaskHandler.es_read"></a>

#### es\_read

```python
def es_read(log_id: str, offset: str, metadata: dict) -> list
```

Returns the logs matching log_id in Elasticsearch and next offset.

Returns '' if no log is found or there was an error.

**Arguments**:

- `log_id`: the log_id of the log to read.
- `offset`: the offset start to read log from.
- `metadata`: log metadata, used for steaming log download.

<a id="log.es_task_handler.ElasticsearchTaskHandler.set_context"></a>

#### set\_context

```python
def set_context(ti: TaskInstance) -> None
```

Provide task_instance context to airflow task handler.

**Arguments**:

- `ti`: task instance object

<a id="log.es_task_handler.ElasticsearchTaskHandler.log_name"></a>

#### log\_name

```python
@property
def log_name() -> str
```

The log name

<a id="log.es_task_handler.ElasticsearchTaskHandler.get_external_log_url"></a>

#### get\_external\_log\_url

```python
def get_external_log_url(task_instance: TaskInstance, try_number: int) -> str
```

Creates an address for an external log collecting service.

**Arguments**:

- `task_instance`: task instance object
- `try_number`: task instance try_number to read logs from.

**Returns**:

`str`: URL to the external log collection service

<a id="log.es_task_handler.ElasticsearchTaskHandler.supports_external_link"></a>

#### supports\_external\_link

```python
@property
def supports_external_link() -> bool
```

Whether we can support external links

