---
title: "yandex"
linkTitle: "yandex"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     yandex Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.yandexcloud_dataproc"></a>

# operators.yandexcloud\_dataproc

<a id="operators.yandexcloud_dataproc.DataprocCreateClusterOperator"></a>

## DataprocCreateClusterOperator Objects

```python
class DataprocCreateClusterOperator(BaseOperator)
```

Creates Yandex.Cloud Data Proc cluster.

**Arguments**:

- `folder_id`: ID of the folder in which cluster should be created.
- `cluster_name`: Cluster name. Must be unique inside the folder.
- `cluster_description`: Cluster description.
- `cluster_image_version`: Cluster image version. Use default.
- `ssh_public_keys`: List of SSH public keys that will be deployed to created compute instances.
- `subnet_id`: ID of the subnetwork. All Data Proc cluster nodes will use one subnetwork.
- `services`: List of services that will be installed to the cluster. Possible options:
HDFS, YARN, MAPREDUCE, HIVE, TEZ, ZOOKEEPER, HBASE, SQOOP, FLUME, SPARK, SPARK, ZEPPELIN, OOZIE
- `s3_bucket`: Yandex.Cloud S3 bucket to store cluster logs.
Jobs will not work if the bucket is not specified.
- `zone`: Availability zone to create cluster in.
Currently there are ru-central1-a, ru-central1-b and ru-central1-c.
- `service_account_id`: Service account id for the cluster.
Service account can be created inside the folder.
- `masternode_resource_preset`: Resources preset (CPU+RAM configuration)
for the primary node of the cluster.
- `masternode_disk_size`: Masternode storage size in GiB.
- `masternode_disk_type`: Masternode storage type. Possible options: network-ssd, network-hdd.
- `datanode_resource_preset`: Resources preset (CPU+RAM configuration)
for the data nodes of the cluster.
- `datanode_disk_size`: Datanodes storage size in GiB.
- `datanode_disk_type`: Datanodes storage type. Possible options: network-ssd, network-hdd.
- `computenode_resource_preset`: Resources preset (CPU+RAM configuration)
for the compute nodes of the cluster.
- `computenode_disk_size`: Computenodes storage size in GiB.
- `computenode_disk_type`: Computenodes storage type. Possible options: network-ssd, network-hdd.
- `connection_id`: ID of the Yandex.Cloud Airflow connection.
- `computenode_max_count`: Maximum number of nodes of compute autoscaling subcluster.
- `computenode_warmup_duration`: The warmup time of the instance in seconds. During this time,
traffic is sent to the instance,
but instance metrics are not collected. In seconds.
- `computenode_stabilization_duration`: Minimum amount of time in seconds for monitoring before
Instance Groups can reduce the number of instances in the group.
During this time, the group size doesn't decrease,
even if the new metric values indicate that it should. In seconds.
- `computenode_preemptible`: Preemptible instances are stopped at least once every 24 hours,
and can be stopped at any time if their resources are needed by Compute.
- `computenode_cpu_utilization_target`: Defines an autoscaling rule
based on the average CPU utilization of the instance group.
in percents. 10-100.
By default is not set and default autoscaling strategy is used.
- `computenode_decommission_timeout`: Timeout to gracefully decommission nodes during downscaling.
In seconds.
- `log_group_id`: Id of log group to write logs. By default logs will be sent to default log group.
To disable cloud log sending set cluster property dataproc:disable_cloud_logging = true

<a id="operators.yandexcloud_dataproc.DataprocDeleteClusterOperator"></a>

## DataprocDeleteClusterOperator Objects

```python
class DataprocDeleteClusterOperator(BaseOperator)
```

Deletes Yandex.Cloud Data Proc cluster.

**Arguments**:

- `connection_id`: ID of the Yandex.Cloud Airflow connection.
- `cluster_id`: ID of the cluster to remove. (templated)

<a id="operators.yandexcloud_dataproc.DataprocCreateHiveJobOperator"></a>

## DataprocCreateHiveJobOperator Objects

```python
class DataprocCreateHiveJobOperator(BaseOperator)
```

Runs Hive job in Data Proc cluster.

**Arguments**:

- `query`: Hive query.
- `query_file_uri`: URI of the script that contains Hive queries. Can be placed in HDFS or S3.
- `properties`: A mapping of property names to values, used to configure Hive.
- `script_variables`: Mapping of query variable names to values.
- `continue_on_failure`: Whether to continue executing queries if a query fails.
- `name`: Name of the job. Used for labeling.
- `cluster_id`: ID of the cluster to run job in.
Will try to take the ID from Dataproc Hook object if it's specified. (templated)
- `connection_id`: ID of the Yandex.Cloud Airflow connection.

<a id="operators.yandexcloud_dataproc.DataprocCreateMapReduceJobOperator"></a>

## DataprocCreateMapReduceJobOperator Objects

```python
class DataprocCreateMapReduceJobOperator(BaseOperator)
```

Runs Mapreduce job in Data Proc cluster.

**Arguments**:

- `main_jar_file_uri`: URI of jar file with job.
Can be placed in HDFS or S3. Can be specified instead of main_class.
- `main_class`: Name of the main class of the job. Can be specified instead of main_jar_file_uri.
- `file_uris`: URIs of files used in the job. Can be placed in HDFS or S3.
- `archive_uris`: URIs of archive files used in the job. Can be placed in HDFS or S3.
- `jar_file_uris`: URIs of JAR files used in the job. Can be placed in HDFS or S3.
- `properties`: Properties for the job.
- `args`: Arguments to be passed to the job.
- `name`: Name of the job. Used for labeling.
- `cluster_id`: ID of the cluster to run job in.
Will try to take the ID from Dataproc Hook object if it's specified. (templated)
- `connection_id`: ID of the Yandex.Cloud Airflow connection.

<a id="operators.yandexcloud_dataproc.DataprocCreateSparkJobOperator"></a>

## DataprocCreateSparkJobOperator Objects

```python
class DataprocCreateSparkJobOperator(BaseOperator)
```

Runs Spark job in Data Proc cluster.

**Arguments**:

- `main_jar_file_uri`: URI of jar file with job. Can be placed in HDFS or S3.
- `main_class`: Name of the main class of the job.
- `file_uris`: URIs of files used in the job. Can be placed in HDFS or S3.
- `archive_uris`: URIs of archive files used in the job. Can be placed in HDFS or S3.
- `jar_file_uris`: URIs of JAR files used in the job. Can be placed in HDFS or S3.
- `properties`: Properties for the job.
- `args`: Arguments to be passed to the job.
- `name`: Name of the job. Used for labeling.
- `cluster_id`: ID of the cluster to run job in.
Will try to take the ID from Dataproc Hook object if it's specified. (templated)
- `connection_id`: ID of the Yandex.Cloud Airflow connection.
- `packages`: List of maven coordinates of jars to include on the driver and executor classpaths.
- `repositories`: List of additional remote repositories to search for the maven coordinates
given with --packages.
- `exclude_packages`: List of groupId:artifactId, to exclude while resolving the dependencies
provided in --packages to avoid dependency conflicts.

<a id="operators.yandexcloud_dataproc.DataprocCreatePysparkJobOperator"></a>

## DataprocCreatePysparkJobOperator Objects

```python
class DataprocCreatePysparkJobOperator(BaseOperator)
```

Runs Pyspark job in Data Proc cluster.

**Arguments**:

- `main_python_file_uri`: URI of python file with job. Can be placed in HDFS or S3.
- `python_file_uris`: URIs of python files used in the job. Can be placed in HDFS or S3.
- `file_uris`: URIs of files used in the job. Can be placed in HDFS or S3.
- `archive_uris`: URIs of archive files used in the job. Can be placed in HDFS or S3.
- `jar_file_uris`: URIs of JAR files used in the job. Can be placed in HDFS or S3.
- `properties`: Properties for the job.
- `args`: Arguments to be passed to the job.
- `name`: Name of the job. Used for labeling.
- `cluster_id`: ID of the cluster to run job in.
Will try to take the ID from Dataproc Hook object if it's specified. (templated)
- `connection_id`: ID of the Yandex.Cloud Airflow connection.
- `packages`: List of maven coordinates of jars to include on the driver and executor classpaths.
- `repositories`: List of additional remote repositories to search for the maven coordinates
given with --packages.
- `exclude_packages`: List of groupId:artifactId, to exclude while resolving the dependencies
provided in --packages to avoid dependency conflicts.

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_yandexcloud_dataproc"></a>

# example\_dags.example\_yandexcloud\_dataproc

<a id="hooks"></a>

# hooks

<a id="hooks.yandex"></a>

# hooks.yandex

<a id="hooks.yandex.YandexCloudBaseHook"></a>

## YandexCloudBaseHook Objects

```python
class YandexCloudBaseHook(BaseHook)
```

A base hook for Yandex.Cloud related tasks.

**Arguments**:

- `yandex_conn_id`: The connection ID to use when fetching connection info.

<a id="hooks.yandex.YandexCloudBaseHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="hooks.yandex.YandexCloudBaseHook.provider_user_agent"></a>

#### provider\_user\_agent

```python
@classmethod
def provider_user_agent(cls) -> Optional[str]
```

Construct User-Agent from Airflow core & provider package versions

<a id="hooks.yandex.YandexCloudBaseHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="hooks.yandexcloud_dataproc"></a>

# hooks.yandexcloud\_dataproc

<a id="hooks.yandexcloud_dataproc.DataprocHook"></a>

## DataprocHook Objects

```python
class DataprocHook(YandexCloudBaseHook)
```

A base hook for Yandex.Cloud Data Proc.

**Arguments**:

- `yandex_conn_id`: The connection ID to use when fetching connection info.

