---
title: "amazon"
linkTitle: "amazon"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     amazon Plugin.
---



<a id="__init__"></a>

# \_\_init\_\_

<a id="aws"></a>

# aws

<a id="aws.sensors.redshift"></a>

# aws.sensors.redshift

<a id="aws.sensors.s3_prefix"></a>

# aws.sensors.s3\_prefix

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.s3`.

<a id="aws.sensors.rds"></a>

# aws.sensors.rds

<a id="aws.sensors.rds.RdsBaseSensor"></a>

## RdsBaseSensor Objects

```python
class RdsBaseSensor(BaseSensorOperator)
```

Base operator that implements common functions for all sensors

<a id="aws.sensors.rds.RdsSnapshotExistenceSensor"></a>

## RdsSnapshotExistenceSensor Objects

```python
class RdsSnapshotExistenceSensor(RdsBaseSensor)
```

Waits for RDS snapshot with a specific status.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsSnapshotExistenceSensor`

**Arguments**:

- `db_type`: Type of the DB - either "instance" or "cluster"
- `db_snapshot_identifier`: The identifier for the DB snapshot
- `target_statuses`: Target status of snapshot

<a id="aws.sensors.rds.RdsExportTaskExistenceSensor"></a>

## RdsExportTaskExistenceSensor Objects

```python
class RdsExportTaskExistenceSensor(RdsBaseSensor)
```

Waits for RDS export task with a specific status.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsExportTaskExistenceSensor`

**Arguments**:

- `export_task_identifier`: A unique identifier for the snapshot export task.
- `target_statuses`: Target status of export task

<a id="aws.sensors.emr_job_flow"></a>

# aws.sensors.emr\_job\_flow

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.emr`.

<a id="aws.sensors.emr_containers"></a>

# aws.sensors.emr\_containers

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.emr`.

<a id="aws.sensors.emr_containers.EMRContainerSensor"></a>

## EMRContainerSensor Objects

```python
class EMRContainerSensor(EmrContainerSensor)
```

This class is deprecated.
Please use  :class:`airflow.providers.amazon.aws.sensors.emr.EmrContainerSensor`.

<a id="aws.sensors.dms"></a>

# aws.sensors.dms

<a id="aws.sensors.dms.DmsTaskBaseSensor"></a>

## DmsTaskBaseSensor Objects

```python
class DmsTaskBaseSensor(BaseSensorOperator)
```

Contains general sensor behavior for DMS task.

Subclasses should set ``target_statuses`` and ``termination_statuses`` fields.

**Arguments**:

- `replication_task_arn`: AWS DMS replication task ARN
- `aws_conn_id`: aws connection to uses
- `target_statuses`: the target statuses, sensor waits until
the task reaches any of these states
- `termination_statuses`: the termination statuses, sensor fails when
the task reaches any of these states

<a id="aws.sensors.dms.DmsTaskBaseSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> DmsHook
```

Get DmsHook

<a id="aws.sensors.dms.DmsTaskCompletedSensor"></a>

## DmsTaskCompletedSensor Objects

```python
class DmsTaskCompletedSensor(DmsTaskBaseSensor)
```

Pokes DMS task until it is completed.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/sensor:DmsTaskCompletedSensor`

**Arguments**:

- `replication_task_arn`: AWS DMS replication task ARN

<a id="aws.sensors.cloud_formation"></a>

# aws.sensors.cloud\_formation

This module contains sensors for AWS CloudFormation.

<a id="aws.sensors.cloud_formation.CloudFormationCreateStackSensor"></a>

## CloudFormationCreateStackSensor Objects

```python
class CloudFormationCreateStackSensor(BaseSensorOperator)
```

Waits for a stack to be created successfully on AWS CloudFormation.

**Arguments**:

- `stack_name`: The name of the stack to wait for (templated)
- `aws_conn_id`: ID of the Airflow connection where credentials and extra configuration are
stored
- `poke_interval`: Time in seconds that the job should wait between each try

<a id="aws.sensors.cloud_formation.CloudFormationCreateStackSensor.hook"></a>

#### hook

```python
@cached_property
def hook() -> CloudFormationHook
```

Create and return an CloudFormationHook

<a id="aws.sensors.cloud_formation.CloudFormationDeleteStackSensor"></a>

## CloudFormationDeleteStackSensor Objects

```python
class CloudFormationDeleteStackSensor(BaseSensorOperator)
```

Waits for a stack to be deleted successfully on AWS CloudFormation.

**Arguments**:

- `stack_name`: The name of the stack to wait for (templated)
- `aws_conn_id`: ID of the Airflow connection where credentials and extra configuration are
stored
- `poke_interval`: Time in seconds that the job should wait between each try

<a id="aws.sensors.cloud_formation.CloudFormationDeleteStackSensor.hook"></a>

#### hook

```python
@cached_property
def hook() -> CloudFormationHook
```

Create and return an CloudFormationHook

<a id="aws.sensors.s3_key"></a>

# aws.sensors.s3\_key

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.s3`.

<a id="aws.sensors.emr"></a>

# aws.sensors.emr

<a id="aws.sensors.emr.EmrBaseSensor"></a>

## EmrBaseSensor Objects

```python
class EmrBaseSensor(BaseSensorOperator)
```

Contains general sensor behavior for EMR.

Subclasses should implement following methods:
    - ``get_emr_response()``
    - ``state_from_response()``
    - ``failure_message_from_response()``

Subclasses should set ``target_states`` and ``failed_states`` fields.

**Arguments**:

- `aws_conn_id`: aws connection to uses

<a id="aws.sensors.emr.EmrBaseSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> EmrHook
```

Get EmrHook

<a id="aws.sensors.emr.EmrBaseSensor.get_emr_response"></a>

#### get\_emr\_response

```python
def get_emr_response() -> Dict[str, Any]
```

Make an API call with boto3 and get response.

**Returns**:

`dict[str, Any]`: response

<a id="aws.sensors.emr.EmrBaseSensor.state_from_response"></a>

#### state\_from\_response

```python
@staticmethod
def state_from_response(response: Dict[str, Any]) -> str
```

Get state from response dictionary.

**Arguments**:

- `response`: response from AWS API

**Returns**:

`str`: state

<a id="aws.sensors.emr.EmrBaseSensor.failure_message_from_response"></a>

#### failure\_message\_from\_response

```python
@staticmethod
def failure_message_from_response(response: Dict[str, Any]) -> Optional[str]
```

Get failure message from response dictionary.

**Arguments**:

- `response`: response from AWS API

**Returns**:

`Optional[str]`: failure message

<a id="aws.sensors.emr.EmrContainerSensor"></a>

## EmrContainerSensor Objects

```python
class EmrContainerSensor(BaseSensorOperator)
```

Asks for the state of the job run until it reaches a failure state or success state.

If the job run fails, the task will fail.

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/sensor:EmrContainerSensor`

**Arguments**:

- `job_id`: job_id to check the state of
- `max_retries`: Number of times to poll for query state before
returning the current state, defaults to None
- `aws_conn_id`: aws connection to use, defaults to 'aws_default'
- `poll_interval`: Time in seconds to wait between two consecutive call to
check query status on athena, defaults to 10

<a id="aws.sensors.emr.EmrContainerSensor.hook"></a>

#### hook

```python
@cached_property
def hook() -> EmrContainerHook
```

Create and return an EmrContainerHook

<a id="aws.sensors.emr.EmrJobFlowSensor"></a>

## EmrJobFlowSensor Objects

```python
class EmrJobFlowSensor(EmrBaseSensor)
```

Asks for the state of the EMR JobFlow (Cluster) until it reaches

any of the target states.
If it fails the sensor errors, failing the task.

With the default target states, sensor waits cluster to be terminated.
When target_states is set to ['RUNNING', 'WAITING'] sensor waits
until job flow to be ready (after 'STARTING' and 'BOOTSTRAPPING' states)

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/sensor:EmrJobFlowSensor`

**Arguments**:

- `job_flow_id`: job_flow_id to check the state of
- `target_states`: the target states, sensor waits until
job flow reaches any of these states
- `failed_states`: the failure states, sensor fails when
job flow reaches any of these states

<a id="aws.sensors.emr.EmrJobFlowSensor.get_emr_response"></a>

#### get\_emr\_response

```python
def get_emr_response() -> Dict[str, Any]
```

Make an API call with boto3 and get cluster-level details.

.. seealso::
    https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/emr.html#EMR.Client.describe_cluster

**Returns**:

`dict[str, Any]`: response

<a id="aws.sensors.emr.EmrJobFlowSensor.state_from_response"></a>

#### state\_from\_response

```python
@staticmethod
def state_from_response(response: Dict[str, Any]) -> str
```

Get state from response dictionary.

**Arguments**:

- `response`: response from AWS API

**Returns**:

`str`: current state of the cluster

<a id="aws.sensors.emr.EmrJobFlowSensor.failure_message_from_response"></a>

#### failure\_message\_from\_response

```python
@staticmethod
def failure_message_from_response(response: Dict[str, Any]) -> Optional[str]
```

Get failure message from response dictionary.

**Arguments**:

- `response`: response from AWS API

**Returns**:

`Optional[str]`: failure message

<a id="aws.sensors.emr.EmrStepSensor"></a>

## EmrStepSensor Objects

```python
class EmrStepSensor(EmrBaseSensor)
```

Asks for the state of the step until it reaches any of the target states.

If it fails the sensor errors, failing the task.

With the default target states, sensor waits step to be completed.

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/sensor:EmrStepSensor`

**Arguments**:

- `job_flow_id`: job_flow_id which contains the step check the state of
- `step_id`: step to check the state of
- `target_states`: the target states, sensor waits until
step reaches any of these states
- `failed_states`: the failure states, sensor fails when
step reaches any of these states

<a id="aws.sensors.emr.EmrStepSensor.get_emr_response"></a>

#### get\_emr\_response

```python
def get_emr_response() -> Dict[str, Any]
```

Make an API call with boto3 and get details about the cluster step.

.. seealso::
    https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/emr.html#EMR.Client.describe_step

**Returns**:

`dict[str, Any]`: response

<a id="aws.sensors.emr.EmrStepSensor.state_from_response"></a>

#### state\_from\_response

```python
@staticmethod
def state_from_response(response: Dict[str, Any]) -> str
```

Get state from response dictionary.

**Arguments**:

- `response`: response from AWS API

**Returns**:

`str`: execution state of the cluster step

<a id="aws.sensors.emr.EmrStepSensor.failure_message_from_response"></a>

#### failure\_message\_from\_response

```python
@staticmethod
def failure_message_from_response(response: Dict[str, Any]) -> Optional[str]
```

Get failure message from response dictionary.

**Arguments**:

- `response`: response from AWS API

**Returns**:

`Optional[str]`: failure message

<a id="aws.sensors.redshift_cluster"></a>

# aws.sensors.redshift\_cluster

<a id="aws.sensors.redshift_cluster.RedshiftClusterSensor"></a>

## RedshiftClusterSensor Objects

```python
class RedshiftClusterSensor(BaseSensorOperator)
```

Waits for a Redshift cluster to reach a specific status.

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/sensor:RedshiftClusterSensor`

**Arguments**:

- `cluster_identifier`: The identifier for the cluster being pinged.
- `target_status`: The cluster status desired.

<a id="aws.sensors.redshift_cluster.RedshiftClusterSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> RedshiftHook
```

Create and return a RedshiftHook

<a id="aws.sensors.sqs"></a>

# aws.sensors.sqs

Reads and then deletes the message from SQS queue

<a id="aws.sensors.sqs.SqsSensor"></a>

## SqsSensor Objects

```python
class SqsSensor(BaseSensorOperator)
```

Get messages from an SQS queue and then deletes  the message from the SQS queue.

If deletion of messages fails an AirflowException is thrown otherwise, the message
is pushed through XCom with the key ``messages``.

**Arguments**:

- `aws_conn_id`: AWS connection id
- `sqs_queue`: The SQS queue url (templated)
- `max_messages`: The maximum number of messages to retrieve for each poke (templated)
- `wait_time_seconds`: The time in seconds to wait for receiving messages (default: 1 second)
- `visibility_timeout`: Visibility timeout, a period of time during which
Amazon SQS prevents other consumers from receiving and processing the message.
- `message_filtering`: Specified how received messages should be filtered. Supported options are:
`None` (no filtering, default), `'literal'` (message Body literal match) or `'jsonpath'`
(message Body filtered using a JSONPath expression).
You may add further methods by overriding the relevant class methods.
- `message_filtering_match_values`: Optional value/s for the message filter to match on.
For example, with literal matching, if a message body matches any of the specified values
then it is included. For JSONPath matching, the result of the JSONPath expression is used
and may match any of the specified values.
- `message_filtering_config`: Additional configuration to pass to the message filter.
For example with JSONPath filtering you can pass a JSONPath expression string here,
such as `'foo[*].baz'`. Messages with a Body which does not match are ignored.
- `delete_message_on_reception`: Default to `True`, the messages are deleted from the queue
as soon as being consumed. Otherwise, the messages remain in the queue after consumption and
should be deleted manually.

<a id="aws.sensors.sqs.SqsSensor.poke"></a>

#### poke

```python
def poke(context: 'Context')
```

Check for message on subscribed queue and write to xcom the message with key ``messages``

**Arguments**:

- `context`: the context object

**Returns**:

``True`` if message is available or ``False``

<a id="aws.sensors.sqs.SqsSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> SqsHook
```

Create and return an SqsHook

<a id="aws.sensors.sqs.SQSSensor"></a>

## SQSSensor Objects

```python
class SQSSensor(SqsSensor)
```

This sensor is deprecated.
Please use :class:`airflow.providers.amazon.aws.sensors.sqs.SqsSensor`.

<a id="aws.sensors.eks"></a>

# aws.sensors.eks

Tracking the state of Amazon EKS Clusters, Amazon EKS managed node groups, and AWS Fargate profiles.

<a id="aws.sensors.eks.EksClusterStateSensor"></a>

## EksClusterStateSensor Objects

```python
class EksClusterStateSensor(BaseSensorOperator)
```

Check the state of an Amazon EKS Cluster until it reaches the target state or another terminal state.

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/sensor:EksClusterStateSensor`

**Arguments**:

- `cluster_name`: The name of the Cluster to watch. (templated)
- `target_state`: Target state of the Cluster. (templated)
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.sensors.eks.EksFargateProfileStateSensor"></a>

## EksFargateProfileStateSensor Objects

```python
class EksFargateProfileStateSensor(BaseSensorOperator)
```

Check the state of an AWS Fargate profile until it reaches the target state or another terminal state.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/sensor:EksFargateProfileStateSensor`

**Arguments**:

- `cluster_name`: The name of the Cluster which the AWS Fargate profile is attached to. (templated)
- `fargate_profile_name`: The name of the Fargate profile to watch. (templated)
- `target_state`: Target state of the Fargate profile. (templated)
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.sensors.eks.EksNodegroupStateSensor"></a>

## EksNodegroupStateSensor Objects

```python
class EksNodegroupStateSensor(BaseSensorOperator)
```

Check the state of an EKS managed node group until it reaches the target state or another terminal state.

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/sensor:EksNodegroupStateSensor`

**Arguments**:

- `cluster_name`: The name of the Cluster which the Nodegroup is attached to. (templated)
- `nodegroup_name`: The name of the Nodegroup to watch. (templated)
- `target_state`: Target state of the Nodegroup. (templated)
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.sensors.eks.EKSClusterStateSensor"></a>

## EKSClusterStateSensor Objects

```python
class EKSClusterStateSensor(EksClusterStateSensor)
```

This sensor is deprecated.
Please use :class:`airflow.providers.amazon.aws.sensors.eks.EksClusterStateSensor`.

<a id="aws.sensors.eks.EKSFargateProfileStateSensor"></a>

## EKSFargateProfileStateSensor Objects

```python
class EKSFargateProfileStateSensor(EksFargateProfileStateSensor)
```

This sensor is deprecated.
Please use :class:`airflow.providers.amazon.aws.sensors.eks.EksFargateProfileStateSensor`.

<a id="aws.sensors.eks.EKSNodegroupStateSensor"></a>

## EKSNodegroupStateSensor Objects

```python
class EKSNodegroupStateSensor(EksNodegroupStateSensor)
```

This sensor is deprecated.
Please use :class:`airflow.providers.amazon.aws.sensors.eks.EksNodegroupStateSensor`.

<a id="aws.sensors.glue_catalog_partition"></a>

# aws.sensors.glue\_catalog\_partition

<a id="aws.sensors.glue_catalog_partition.GlueCatalogPartitionSensor"></a>

## GlueCatalogPartitionSensor Objects

```python
class GlueCatalogPartitionSensor(BaseSensorOperator)
```

Waits for a partition to show up in AWS Glue Catalog.

**Arguments**:

- `table_name`: The name of the table to wait for, supports the dot
notation (my_database.my_table)
- `expression`: The partition clause to wait for. This is passed as
is to the AWS Glue Catalog API's get_partitions function,
and supports SQL like notation as in ``ds='2015-01-01'
AND type='value'`` and comparison operators as in ``"ds>=2015-01-01"``.
See https://docs.aws.amazon.com/glue/latest/dg/aws-glue-api-catalog-partitions.html
`aws`-glue-api-catalog-partitions-GetPartitions
- `aws_conn_id`: ID of the Airflow connection where
credentials and extra configuration are stored
- `region_name`: Optional aws region name (example: us-east-1). Uses region from connection
if not specified.
- `database_name`: The name of the catalog database where the partitions reside.
- `poke_interval`: Time in seconds that the job should wait in
between each tries

<a id="aws.sensors.glue_catalog_partition.GlueCatalogPartitionSensor.poke"></a>

#### poke

```python
def poke(context: 'Context')
```

Checks for existence of the partition in the AWS Glue Catalog table

<a id="aws.sensors.glue_catalog_partition.GlueCatalogPartitionSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> GlueCatalogHook
```

Gets the GlueCatalogHook

<a id="aws.sensors.glue_catalog_partition.AwsGlueCatalogPartitionSensor"></a>

## AwsGlueCatalogPartitionSensor Objects

```python
class AwsGlueCatalogPartitionSensor(GlueCatalogPartitionSensor)
```

This sensor is deprecated. Please use
:class:`airflow.providers.amazon.aws.sensors.glue_catalog_partition.GlueCatalogPartitionSensor`.

<a id="aws.sensors.sagemaker_base"></a>

# aws.sensors.sagemaker\_base

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.sagemaker`.

<a id="aws.sensors.ec2_instance_state"></a>

# aws.sensors.ec2\_instance\_state

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.ec2`.

<a id="aws.sensors.glacier"></a>

# aws.sensors.glacier

<a id="aws.sensors.glacier.JobStatus"></a>

## JobStatus Objects

```python
class JobStatus(Enum)
```

Glacier jobs description

<a id="aws.sensors.glacier.GlacierJobOperationSensor"></a>

## GlacierJobOperationSensor Objects

```python
class GlacierJobOperationSensor(BaseSensorOperator)
```

Glacier sensor for checking job state. This operator runs only in reschedule mode.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:GlacierJobOperationSensor`

**Arguments**:

- `aws_conn_id`: The reference to the AWS connection details
- `vault_name`: name of Glacier vault on which job is executed
- `job_id`: the job ID was returned by retrieve_inventory()
- `poke_interval`: Time in seconds that the job should wait in
between each tries
- `mode`: How the sensor operates.
Options are: ``{ poke | reschedule }``, default is ``poke``.
When set to ``poke`` the sensor is taking up a worker slot for its
whole execution time and sleeps between pokes. Use this mode if the
expected runtime of the sensor is short or if a short poke interval
is required. Note that the sensor will hold onto a worker slot and
a pool slot for the duration of the sensor's runtime in this mode.
When set to ``reschedule`` the sensor task frees the worker slot when
the criteria is not yet met and it's rescheduled at a later time. Use
this mode if the time before the criteria is met is expected to be
quite long. The poke interval should be more than one minute to
prevent too much load on the scheduler.

<a id="aws.sensors.s3_keys_unchanged"></a>

# aws.sensors.s3\_keys\_unchanged

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.s3`.

<a id="aws.sensors.batch"></a>

# aws.sensors.batch

<a id="aws.sensors.batch.BatchSensor"></a>

## BatchSensor Objects

```python
class BatchSensor(BaseSensorOperator)
```

Asks for the state of the Batch Job execution until it reaches a failure state or success state.

If the job fails, the task will fail.

.. seealso::
    For more information on how to use this sensor, take a look at the guide:
    :ref:`howto/sensor:BatchSensor`

**Arguments**:

- `job_id`: Batch job_id to check the state for
- `aws_conn_id`: aws connection to use, defaults to 'aws_default'

<a id="aws.sensors.batch.BatchSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> BatchClientHook
```

Create and return a BatchClientHook

<a id="aws.sensors"></a>

# aws.sensors

<a id="aws.sensors.dms_task"></a>

# aws.sensors.dms\_task

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.dms`.

<a id="aws.sensors.step_function_execution"></a>

# aws.sensors.step\_function\_execution

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.step_function`.

<a id="aws.sensors.emr_step"></a>

# aws.sensors.emr\_step

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.emr`.

<a id="aws.sensors.glue"></a>

# aws.sensors.glue

<a id="aws.sensors.glue.GlueJobSensor"></a>

## GlueJobSensor Objects

```python
class GlueJobSensor(BaseSensorOperator)
```

Waits for an AWS Glue Job to reach any of the status below

'FAILED', 'STOPPED', 'SUCCEEDED'

**Arguments**:

- `job_name`: The AWS Glue Job unique name
- `run_id`: The AWS Glue current running job identifier

<a id="aws.sensors.glue.AwsGlueJobSensor"></a>

## AwsGlueJobSensor Objects

```python
class AwsGlueJobSensor(GlueJobSensor)
```

This sensor is deprecated.
Please use :class:`airflow.providers.amazon.aws.sensors.glue.GlueJobSensor`.

<a id="aws.sensors.step_function"></a>

# aws.sensors.step\_function

<a id="aws.sensors.step_function.StepFunctionExecutionSensor"></a>

## StepFunctionExecutionSensor Objects

```python
class StepFunctionExecutionSensor(BaseSensorOperator)
```

Asks for the state of the Step Function State Machine Execution until it

reaches a failure state or success state.
If it fails, failing the task.

On successful completion of the Execution the Sensor will do an XCom Push
of the State Machine's output to `output`

**Arguments**:

- `execution_arn`: execution_arn to check the state of
- `aws_conn_id`: aws connection to use, defaults to 'aws_default'

<a id="aws.sensors.step_function.StepFunctionExecutionSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> StepFunctionHook
```

Create and return a StepFunctionHook

<a id="aws.sensors.sagemaker"></a>

# aws.sensors.sagemaker

<a id="aws.sensors.sagemaker.SageMakerBaseSensor"></a>

## SageMakerBaseSensor Objects

```python
class SageMakerBaseSensor(BaseSensorOperator)
```

Contains general sensor behavior for SageMaker.

Subclasses should implement get_sagemaker_response()
and state_from_response() methods.
Subclasses should also implement NON_TERMINAL_STATES and FAILED_STATE methods.

<a id="aws.sensors.sagemaker.SageMakerBaseSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> SageMakerHook
```

Get SageMakerHook.

<a id="aws.sensors.sagemaker.SageMakerBaseSensor.non_terminal_states"></a>

#### non\_terminal\_states

```python
def non_terminal_states() -> Set[str]
```

Placeholder for returning states with should not terminate.

<a id="aws.sensors.sagemaker.SageMakerBaseSensor.failed_states"></a>

#### failed\_states

```python
def failed_states() -> Set[str]
```

Placeholder for returning states with are considered failed.

<a id="aws.sensors.sagemaker.SageMakerBaseSensor.get_sagemaker_response"></a>

#### get\_sagemaker\_response

```python
def get_sagemaker_response() -> dict
```

Placeholder for checking status of a SageMaker task.

<a id="aws.sensors.sagemaker.SageMakerBaseSensor.get_failed_reason_from_response"></a>

#### get\_failed\_reason\_from\_response

```python
def get_failed_reason_from_response(response: dict) -> str
```

Placeholder for extracting the reason for failure from an AWS response.

<a id="aws.sensors.sagemaker.SageMakerBaseSensor.state_from_response"></a>

#### state\_from\_response

```python
def state_from_response(response: dict) -> str
```

Placeholder for extracting the state from an AWS response.

<a id="aws.sensors.sagemaker.SageMakerEndpointSensor"></a>

## SageMakerEndpointSensor Objects

```python
class SageMakerEndpointSensor(SageMakerBaseSensor)
```

Asks for the state of the endpoint state until it reaches a

terminal state.
If it fails the sensor errors, the task fails.

**Arguments**:

- `job_name`: job_name of the endpoint instance to check the state of

<a id="aws.sensors.sagemaker.SageMakerTransformSensor"></a>

## SageMakerTransformSensor Objects

```python
class SageMakerTransformSensor(SageMakerBaseSensor)
```

Asks for the state of the transform state until it reaches a

terminal state.
The sensor will error if the job errors, throwing a
AirflowException
containing the failure reason.

**Arguments**:

- `job_name`: job_name of the transform job instance to check the state of

<a id="aws.sensors.sagemaker.SageMakerTuningSensor"></a>

## SageMakerTuningSensor Objects

```python
class SageMakerTuningSensor(SageMakerBaseSensor)
```

Asks for the state of the tuning state until it reaches a terminal

state.
The sensor will error if the job errors, throwing a
AirflowException
containing the failure reason.

**Arguments**:

- `job_name` (`str`): job_name of the tuning instance to check the state of

<a id="aws.sensors.sagemaker.SageMakerTrainingSensor"></a>

## SageMakerTrainingSensor Objects

```python
class SageMakerTrainingSensor(SageMakerBaseSensor)
```

Asks for the state of the training state until it reaches a

terminal state.
If it fails the sensor errors, failing the task.

**Arguments**:

- `job_name`: name of the SageMaker training job to check the state of
- `print_log`: if the operator should print the cloudwatch log

<a id="aws.sensors.sagemaker.SageMakerTrainingSensor.init_log_resource"></a>

#### init\_log\_resource

```python
def init_log_resource(hook: SageMakerHook) -> None
```

Set tailing LogState for associated training job.

<a id="aws.sensors.ec2"></a>

# aws.sensors.ec2

<a id="aws.sensors.ec2.EC2InstanceStateSensor"></a>

## EC2InstanceStateSensor Objects

```python
class EC2InstanceStateSensor(BaseSensorOperator)
```

Check the state of the AWS EC2 instance until

state of the instance become equal to the target state.

**Arguments**:

- `target_state`: target state of instance
- `instance_id`: id of the AWS EC2 instance
- `region_name`: (optional) aws region name associated with the client

<a id="aws.sensors.sagemaker_endpoint"></a>

# aws.sensors.sagemaker\_endpoint

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.sagemaker`.

<a id="aws.sensors.sagemaker_transform"></a>

# aws.sensors.sagemaker\_transform

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.sagemaker`.

<a id="aws.sensors.sagemaker_tuning"></a>

# aws.sensors.sagemaker\_tuning

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.sagemaker`.

<a id="aws.sensors.glue_crawler"></a>

# aws.sensors.glue\_crawler

<a id="aws.sensors.glue_crawler.GlueCrawlerSensor"></a>

## GlueCrawlerSensor Objects

```python
class GlueCrawlerSensor(BaseSensorOperator)
```

Waits for an AWS Glue crawler to reach any of the statuses below

'FAILED', 'CANCELLED', 'SUCCEEDED'

**Arguments**:

- `crawler_name`: The AWS Glue crawler unique name
- `aws_conn_id`: aws connection to use, defaults to 'aws_default'

<a id="aws.sensors.glue_crawler.GlueCrawlerSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> GlueCrawlerHook
```

Returns a new or pre-existing GlueCrawlerHook

<a id="aws.sensors.glue_crawler.AwsGlueCrawlerSensor"></a>

## AwsGlueCrawlerSensor Objects

```python
class AwsGlueCrawlerSensor(GlueCrawlerSensor)
```

This sensor is deprecated. Please use
:class:`airflow.providers.amazon.aws.sensors.glue_crawler.GlueCrawlerSensor`.

<a id="aws.sensors.sagemaker_training"></a>

# aws.sensors.sagemaker\_training

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.sagemaker`.

<a id="aws.sensors.athena"></a>

# aws.sensors.athena

<a id="aws.sensors.athena.AthenaSensor"></a>

## AthenaSensor Objects

```python
class AthenaSensor(BaseSensorOperator)
```

Asks for the state of the Query until it reaches a failure state or success state.

If the query fails, the task will fail.

**Arguments**:

- `query_execution_id`: query_execution_id to check the state of
- `max_retries`: Number of times to poll for query state before
returning the current state, defaults to None
- `aws_conn_id`: aws connection to use, defaults to 'aws_default'
- `sleep_time`: Time in seconds to wait between two consecutive call to
check query status on athena, defaults to 10

<a id="aws.sensors.athena.AthenaSensor.hook"></a>

#### hook

```python
@cached_property
def hook() -> AthenaHook
```

Create and return an AthenaHook

<a id="aws.sensors.s3"></a>

# aws.sensors.s3

<a id="aws.sensors.s3.S3KeySensor"></a>

## S3KeySensor Objects

```python
class S3KeySensor(BaseSensorOperator)
```

Waits for a key (a file-like instance on S3) to be present in a S3 bucket.

S3 being a key/value it does not support folders. The path is just a key
a resource.

**Arguments**:

- `bucket_key`: The key being waited on. Supports full s3:// style url
or relative path from root level. When it's specified as a full s3://
url, please leave bucket_name as `None`.
- `bucket_name`: Name of the S3 bucket. Only needed when ``bucket_key``
is not provided as a full s3:// url.
- `wildcard_match`: whether the bucket_key should be interpreted as a
Unix wildcard pattern
- `aws_conn_id`: a reference to the s3 connection
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
You can provide the following values:

- ``False``: do not validate SSL certificates. SSL will still be used
         (unless use_ssl is False), but SSL certificates will not be
         verified.
- ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
         You can specify this argument if you want to use a different
         CA cert bundle than the one used by botocore.

<a id="aws.sensors.s3.S3KeySensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> S3Hook
```

Create and return an S3Hook

<a id="aws.sensors.s3.S3KeySizeSensor"></a>

## S3KeySizeSensor Objects

```python
class S3KeySizeSensor(S3KeySensor)
```

Waits for a key (a file-like instance on S3) to be present and be more than

some size in a S3 bucket.
S3 being a key/value it does not support folders. The path is just a key
a resource.

**Arguments**:

- `bucket_key`: The key being waited on. Supports full s3:// style url
or relative path from root level. When it's specified as a full s3://
url, please leave bucket_name as `None`.
- `bucket_name`: Name of the S3 bucket. Only needed when ``bucket_key``
is not provided as a full s3:// url.
- `wildcard_match`: whether the bucket_key should be interpreted as a
Unix wildcard pattern
- `aws_conn_id`: a reference to the s3 connection
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
You can provide the following values:

- ``False``: do not validate SSL certificates. SSL will still be used
         (unless use_ssl is False), but SSL certificates will not be
         verified.
- ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
         You can specify this argument if you want to use a different
         CA cert bundle than the one used by botocore.
- `check_fn`: Function that receives the list of the S3 objects,
and returns the boolean:
- ``True``: a certain criteria is met
- ``False``: the criteria isn't met
**Example**: Wait for any S3 object size more than 1 megabyte  ::

    def check_fn(self, data: List) -> bool:
        return any(f.get('Size', 0) > 1048576 for f in data if isinstance(f, dict))

<a id="aws.sensors.s3.S3KeySizeSensor.get_files"></a>

#### get\_files

```python
def get_files(s3_hook: S3Hook, delimiter: Optional[str] = '/') -> List
```

Gets a list of files in the bucket

<a id="aws.sensors.s3.S3KeySizeSensor.check_fn"></a>

#### check\_fn

```python
def check_fn(data: List,
             object_min_size: Optional[Union[int, float]] = 0) -> bool
```

Default function for checking that S3 Objects have size more than 0

**Arguments**:

- `data`: List of the objects in S3 bucket.
- `object_min_size`: Checks if the objects sizes are greater then this value.

<a id="aws.sensors.s3.S3KeysUnchangedSensor"></a>

## S3KeysUnchangedSensor Objects

```python
@poke_mode_only
class S3KeysUnchangedSensor(BaseSensorOperator)
```

Checks for changes in the number of objects at prefix in AWS S3

bucket and returns True if the inactivity period has passed with no
increase in the number of objects. Note, this sensor will not behave correctly
in reschedule mode, as the state of the listed objects in the S3 bucket will
be lost between rescheduled invocations.

**Arguments**:

- `bucket_name`: Name of the S3 bucket
- `prefix`: The prefix being waited on. Relative path from bucket root level.
- `aws_conn_id`: a reference to the s3 connection
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
You can provide the following values:

- ``False``: do not validate SSL certificates. SSL will still be used
         (unless use_ssl is False), but SSL certificates will not be
         verified.
- ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
         You can specify this argument if you want to use a different
         CA cert bundle than the one used by botocore.
- `inactivity_period`: The total seconds of inactivity to designate
keys unchanged. Note, this mechanism is not real time and
this operator may not return until a poke_interval after this period
has passed with no additional objects sensed.
- `min_objects`: The minimum number of objects needed for keys unchanged
sensor to be considered valid.
- `previous_objects`: The set of object ids found during the last poke.
- `allow_delete`: Should this sensor consider objects being deleted
between pokes valid behavior. If true a warning message will be logged
when this happens. If false an error will be raised.

<a id="aws.sensors.s3.S3KeysUnchangedSensor.hook"></a>

#### hook

```python
@cached_property
def hook()
```

Returns S3Hook.

<a id="aws.sensors.s3.S3KeysUnchangedSensor.is_keys_unchanged"></a>

#### is\_keys\_unchanged

```python
def is_keys_unchanged(current_objects: Set[str]) -> bool
```

Checks whether new objects have been uploaded and the inactivity_period

has passed and updates the state of the sensor accordingly.

**Arguments**:

- `current_objects`: set of object ids in bucket during last poke.

<a id="aws.sensors.s3.S3PrefixSensor"></a>

## S3PrefixSensor Objects

```python
class S3PrefixSensor(BaseSensorOperator)
```

Waits for a prefix or all prefixes to exist. A prefix is the first part of a key,

thus enabling checking of constructs similar to glob ``airfl*`` or
SQL LIKE ``'airfl%'``. There is the possibility to precise a delimiter to
indicate the hierarchy or keys, meaning that the match will stop at that
delimiter. Current code accepts sane delimiters, i.e. characters that
are NOT special characters in the Python regex engine.

**Arguments**:

- `bucket_name`: Name of the S3 bucket
- `prefix`: The prefix being waited on. Relative path from bucket root level.
- `delimiter`: The delimiter intended to show hierarchy.
Defaults to '/'.
- `aws_conn_id`: a reference to the s3 connection
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
You can provide the following values:

- ``False``: do not validate SSL certificates. SSL will still be used
         (unless use_ssl is False), but SSL certificates will not be
         verified.
- ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
         You can specify this argument if you want to use a different
         CA cert bundle than the one used by botocore.

<a id="aws.sensors.s3.S3PrefixSensor.get_hook"></a>

#### get\_hook

```python
def get_hook() -> S3Hook
```

Create and return an S3Hook

<a id="aws.sensors.emr_base"></a>

# aws.sensors.emr\_base

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.emr`.

<a id="aws.operators.redshift"></a>

# aws.operators.redshift

<a id="aws.operators.rds"></a>

# aws.operators.rds

<a id="aws.operators.rds.RdsBaseOperator"></a>

## RdsBaseOperator Objects

```python
class RdsBaseOperator(BaseOperator)
```

Base operator that implements common functions for all operators

<a id="aws.operators.rds.RdsBaseOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> str
```

Different implementations for snapshots, tasks and events

<a id="aws.operators.rds.RdsBaseOperator.on_kill"></a>

#### on\_kill

```python
def on_kill() -> None
```

Different implementations for snapshots, tasks and events

<a id="aws.operators.rds.RdsCreateDbSnapshotOperator"></a>

## RdsCreateDbSnapshotOperator Objects

```python
class RdsCreateDbSnapshotOperator(RdsBaseOperator)
```

Creates a snapshot of a DB instance or DB cluster.

The source DB instance or cluster must be in the available or storage-optimization state.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsCreateDbSnapshotOperator`

**Arguments**:

- `db_type`: Type of the DB - either "instance" or "cluster"
- `db_identifier`: The identifier of the instance or cluster that you want to create the snapshot of
- `db_snapshot_identifier`: The identifier for the DB snapshot
- `tags`: A list of tags in format `[{"Key": "something", "Value": "something"},]
`USER Tagging <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Tagging.html>`__

<a id="aws.operators.rds.RdsCopyDbSnapshotOperator"></a>

## RdsCopyDbSnapshotOperator Objects

```python
class RdsCopyDbSnapshotOperator(RdsBaseOperator)
```

Copies the specified DB instance or DB cluster snapshot

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsCopyDbSnapshotOperator`

**Arguments**:

- `db_type`: Type of the DB - either "instance" or "cluster"
- `source_db_snapshot_identifier`: The identifier of the source snapshot
- `target_db_snapshot_identifier`: The identifier of the target snapshot
- `kms_key_id`: The AWS KMS key identifier for an encrypted DB snapshot
- `tags`: A list of tags in format `[{"Key": "something", "Value": "something"},]
`USER Tagging <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Tagging.html>`__
- `copy_tags`: Whether to copy all tags from the source snapshot to the target snapshot (default False)
- `pre_signed_url`: The URL that contains a Signature Version 4 signed request
- `option_group_name`: The name of an option group to associate with the copy of the snapshot
Only when db_type='instance'
- `target_custom_availability_zone`: The external custom Availability Zone identifier for the target
Only when db_type='instance'
- `source_region`: The ID of the region that contains the snapshot to be copied

<a id="aws.operators.rds.RdsDeleteDbSnapshotOperator"></a>

## RdsDeleteDbSnapshotOperator Objects

```python
class RdsDeleteDbSnapshotOperator(RdsBaseOperator)
```

Deletes a DB instance or cluster snapshot or terminating the copy operation

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsDeleteDbSnapshotOperator`

**Arguments**:

- `db_type`: Type of the DB - either "instance" or "cluster"
- `db_snapshot_identifier`: The identifier for the DB instance or DB cluster snapshot

<a id="aws.operators.rds.RdsStartExportTaskOperator"></a>

## RdsStartExportTaskOperator Objects

```python
class RdsStartExportTaskOperator(RdsBaseOperator)
```

Starts an export of a snapshot to Amazon S3. The provided IAM role must have access to the S3 bucket.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsStartExportTaskOperator`

**Arguments**:

- `export_task_identifier`: A unique identifier for the snapshot export task.
- `source_arn`: The Amazon Resource Name (ARN) of the snapshot to export to Amazon S3.
- `s3_bucket_name`: The name of the Amazon S3 bucket to export the snapshot to.
- `iam_role_arn`: The name of the IAM role to use for writing to the Amazon S3 bucket.
- `kms_key_id`: The ID of the Amazon Web Services KMS key to use to encrypt the snapshot.
- `s3_prefix`: The Amazon S3 bucket prefix to use as the file name and path of the exported snapshot.
- `export_only`: The data to be exported from the snapshot.

<a id="aws.operators.rds.RdsCancelExportTaskOperator"></a>

## RdsCancelExportTaskOperator Objects

```python
class RdsCancelExportTaskOperator(RdsBaseOperator)
```

Cancels an export task in progress that is exporting a snapshot to Amazon S3

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsCancelExportTaskOperator`

**Arguments**:

- `export_task_identifier`: The identifier of the snapshot export task to cancel

<a id="aws.operators.rds.RdsCreateEventSubscriptionOperator"></a>

## RdsCreateEventSubscriptionOperator Objects

```python
class RdsCreateEventSubscriptionOperator(RdsBaseOperator)
```

Creates an RDS event notification subscription

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsCreateEventSubscriptionOperator`

**Arguments**:

- `subscription_name`: The name of the subscription (must be less than 255 characters)
- `sns_topic_arn`: The ARN of the SNS topic created for event notification
- `source_type`: The type of source that is generating the events. Valid values: db-instance |
db-cluster | db-parameter-group | db-security-group | db-snapshot | db-cluster-snapshot | db-proxy
- `event_categories`: A list of event categories for a source type that you want to subscribe to
`USER Events <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.Messages.html>`__
- `source_ids`: The list of identifiers of the event sources for which events are returned
- `enabled`: A value that indicates whether to activate the subscription (default True)l
- `tags`: A list of tags in format `[{"Key": "something", "Value": "something"},]
`USER Tagging <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Tagging.html>`__

<a id="aws.operators.rds.RdsDeleteEventSubscriptionOperator"></a>

## RdsDeleteEventSubscriptionOperator Objects

```python
class RdsDeleteEventSubscriptionOperator(RdsBaseOperator)
```

Deletes an RDS event notification subscription

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RdsDeleteEventSubscriptionOperator`

**Arguments**:

- `subscription_name`: The name of the RDS event notification subscription you want to delete

<a id="aws.operators.step_function_get_execution_output"></a>

# aws.operators.step\_function\_get\_execution\_output

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.sensors.step_function`.

<a id="aws.operators.emr_containers"></a>

# aws.operators.emr\_containers

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.emr`.

<a id="aws.operators.emr_containers.EMRContainerOperator"></a>

## EMRContainerOperator Objects

```python
class EMRContainerOperator(EmrContainerOperator)
```

This class is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.emr.EmrContainerOperator`.

<a id="aws.operators.dms"></a>

# aws.operators.dms

<a id="aws.operators.dms.DmsCreateTaskOperator"></a>

## DmsCreateTaskOperator Objects

```python
class DmsCreateTaskOperator(BaseOperator)
```

Creates AWS DMS replication task.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:DmsCreateTaskOperator`

**Arguments**:

- `replication_task_id`: Replication task id
- `source_endpoint_arn`: Source endpoint ARN
- `target_endpoint_arn`: Target endpoint ARN
- `replication_instance_arn`: Replication instance ARN
- `table_mappings`: Table mappings
- `migration_type`: Migration type ('full-load'|'cdc'|'full-load-and-cdc'), full-load by default.
- `create_task_kwargs`: Extra arguments for DMS replication task creation.
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.dms.DmsCreateTaskOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Creates AWS DMS replication task from Airflow

**Returns**:

replication task arn

<a id="aws.operators.dms.DmsDeleteTaskOperator"></a>

## DmsDeleteTaskOperator Objects

```python
class DmsDeleteTaskOperator(BaseOperator)
```

Deletes AWS DMS replication task.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:DmsDeleteTaskOperator`

**Arguments**:

- `replication_task_arn`: Replication task ARN
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.dms.DmsDeleteTaskOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Deletes AWS DMS replication task from Airflow

**Returns**:

replication task arn

<a id="aws.operators.dms.DmsDescribeTasksOperator"></a>

## DmsDescribeTasksOperator Objects

```python
class DmsDescribeTasksOperator(BaseOperator)
```

Describes AWS DMS replication tasks.

**Arguments**:

- `describe_tasks_kwargs`: Describe tasks command arguments
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.dms.DmsDescribeTasksOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Describes AWS DMS replication tasks from Airflow

**Returns**:

`(Optional[str], list)`: Marker and list of replication tasks

<a id="aws.operators.dms.DmsStartTaskOperator"></a>

## DmsStartTaskOperator Objects

```python
class DmsStartTaskOperator(BaseOperator)
```

Starts AWS DMS replication task.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:DmsStartTaskOperator`

**Arguments**:

- `replication_task_arn`: Replication task ARN
- `start_replication_task_type`: Replication task start type (default='start-replication')
('start-replication'|'resume-processing'|'reload-target')
- `start_task_kwargs`: Extra start replication task arguments
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.dms.DmsStartTaskOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Starts AWS DMS replication task from Airflow

**Returns**:

replication task arn

<a id="aws.operators.dms.DmsStopTaskOperator"></a>

## DmsStopTaskOperator Objects

```python
class DmsStopTaskOperator(BaseOperator)
```

Stops AWS DMS replication task.

**Arguments**:

- `replication_task_arn`: Replication task ARN
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.dms.DmsStopTaskOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Stops AWS DMS replication task from Airflow

**Returns**:

replication task arn

<a id="aws.operators.cloud_formation"></a>

# aws.operators.cloud\_formation

This module contains CloudFormation create/delete stack operators.

<a id="aws.operators.cloud_formation.CloudFormationCreateStackOperator"></a>

## CloudFormationCreateStackOperator Objects

```python
class CloudFormationCreateStackOperator(BaseOperator)
```

An operator that creates a CloudFormation stack.

**Arguments**:

- `stack_name`: stack name (templated)
- `cloudformation_parameters`: parameters to be passed to CloudFormation.
.. seealso::
    https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/cloudformation.html#CloudFormation.Client.create_stack
- `aws_conn_id`: aws connection to uses

<a id="aws.operators.cloud_formation.CloudFormationDeleteStackOperator"></a>

## CloudFormationDeleteStackOperator Objects

```python
class CloudFormationDeleteStackOperator(BaseOperator)
```

An operator that deletes a CloudFormation stack.

**Arguments**:

- `stack_name`: stack name (templated)
- `cloudformation_parameters`: parameters to be passed to CloudFormation.
.. seealso::
    https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/cloudformation.html#CloudFormation.Client.delete_stack
- `aws_conn_id`: aws connection to uses

<a id="aws.operators.emr"></a>

# aws.operators.emr

<a id="aws.operators.emr.EmrAddStepsOperator"></a>

## EmrAddStepsOperator Objects

```python
class EmrAddStepsOperator(BaseOperator)
```

An operator that adds steps to an existing EMR job_flow.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EmrAddStepsOperator`

**Arguments**:

- `job_flow_id`: id of the JobFlow to add steps to. (templated)
- `job_flow_name`: name of the JobFlow to add steps to. Use as an alternative to passing
job_flow_id. will search for id of JobFlow with matching name in one of the states in
param cluster_states. Exactly one cluster like this should exist or will fail. (templated)
- `cluster_states`: Acceptable cluster states when searching for JobFlow id by job_flow_name.
(templated)
- `aws_conn_id`: aws connection to uses
- `steps`: boto3 style steps or reference to a steps file (must be '.json') to
be added to the jobflow. (templated)
- `do_xcom_push`: if True, job_flow_id is pushed to XCom with key job_flow_id.

<a id="aws.operators.emr.EmrContainerOperator"></a>

## EmrContainerOperator Objects

```python
class EmrContainerOperator(BaseOperator)
```

An operator that submits jobs to EMR on EKS virtual clusters.

**Arguments**:

- `name`: The name of the job run.
- `virtual_cluster_id`: The EMR on EKS virtual cluster ID
- `execution_role_arn`: The IAM role ARN associated with the job run.
- `release_label`: The Amazon EMR release version to use for the job run.
- `job_driver`: Job configuration details, e.g. the Spark job parameters.
- `configuration_overrides`: The configuration overrides for the job run,
specifically either application configuration or monitoring configuration.
- `client_request_token`: The client idempotency token of the job run request.
Use this if you want to specify a unique ID to prevent two jobs from getting started.
If no token is provided, a UUIDv4 token will be generated for you.
- `aws_conn_id`: The Airflow connection used for AWS credentials.
- `poll_interval`: Time (in seconds) to wait between two consecutive calls to check query status on EMR
- `max_tries`: Maximum number of times to wait for the job run to finish.
Defaults to None, which will poll until the job is *not* in a pending, submitted, or running state.

<a id="aws.operators.emr.EmrContainerOperator.hook"></a>

#### hook

```python
@cached_property
def hook() -> EmrContainerHook
```

Create and return an EmrContainerHook.

<a id="aws.operators.emr.EmrContainerOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> Optional[str]
```

Run job on EMR Containers

<a id="aws.operators.emr.EmrContainerOperator.on_kill"></a>

#### on\_kill

```python
def on_kill() -> None
```

Cancel the submitted job run

<a id="aws.operators.emr.EmrClusterLink"></a>

## EmrClusterLink Objects

```python
class EmrClusterLink(BaseOperatorLink)
```

Operator link for EmrCreateJobFlowOperator. It allows users to access the EMR Cluster

<a id="aws.operators.emr.EmrClusterLink.get_link"></a>

#### get\_link

```python
def get_link(operator,
             dttm: Optional[datetime] = None,
             ti_key: Optional["TaskInstanceKey"] = None) -> str
```

Get link to EMR cluster.

**Arguments**:

- `operator`: operator
- `dttm`: datetime

**Returns**:

url link

<a id="aws.operators.emr.EmrCreateJobFlowOperator"></a>

## EmrCreateJobFlowOperator Objects

```python
class EmrCreateJobFlowOperator(BaseOperator)
```

Creates an EMR JobFlow, reading the config from the EMR connection.

A dictionary of JobFlow overrides can be passed that override
the config from the connection.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EmrCreateJobFlowOperator`

**Arguments**:

- `aws_conn_id`: aws connection to uses
- `emr_conn_id`: emr connection to use
- `job_flow_overrides`: boto3 style arguments or reference to an arguments file
(must be '.json') to override emr_connection extra. (templated)
- `region_name`: Region named passed to EmrHook

<a id="aws.operators.emr.EmrModifyClusterOperator"></a>

## EmrModifyClusterOperator Objects

```python
class EmrModifyClusterOperator(BaseOperator)
```

An operator that modifies an existing EMR cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EmrModifyClusterOperator`

**Arguments**:

- `cluster_id`: cluster identifier
- `step_concurrency_level`: Concurrency of the cluster
- `aws_conn_id`: aws connection to uses
- `do_xcom_push`: if True, cluster_id is pushed to XCom with key cluster_id.

<a id="aws.operators.emr.EmrTerminateJobFlowOperator"></a>

## EmrTerminateJobFlowOperator Objects

```python
class EmrTerminateJobFlowOperator(BaseOperator)
```

Operator to terminate EMR JobFlows.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EmrTerminateJobFlowOperator`

**Arguments**:

- `job_flow_id`: id of the JobFlow to terminate. (templated)
- `aws_conn_id`: aws connection to uses

<a id="aws.operators.s3_bucket"></a>

# aws.operators.s3\_bucket

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.s3`.

<a id="aws.operators.aws_lambda"></a>

# aws.operators.aws\_lambda

<a id="aws.operators.aws_lambda.AwsLambdaInvokeFunctionOperator"></a>

## AwsLambdaInvokeFunctionOperator Objects

```python
class AwsLambdaInvokeFunctionOperator(BaseOperator)
```

Invokes an AWS Lambda function.

You can invoke a function synchronously (and wait for the response),
or asynchronously.
To invoke a function asynchronously,
set `invocation_type` to `Event`. For more details,
review the boto3 Lambda invoke docs.

**Arguments**:

- `function_name`: The name of the AWS Lambda function, version, or alias.
- `payload`: The JSON string that you want to provide to your Lambda function as input.
- `log_type`: Set to Tail to include the execution log in the response. Otherwise, set to "None".
- `qualifier`: Specify a version or alias to invoke a published version of the function.
- `aws_conn_id`: The AWS connection ID to use
.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AwsLambdaInvokeFunctionOperator`

<a id="aws.operators.aws_lambda.AwsLambdaInvokeFunctionOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Invokes the target AWS Lambda function from Airflow.

**Returns**:

The response payload from the function, or an error object.

<a id="aws.operators.redshift_cluster"></a>

# aws.operators.redshift\_cluster

<a id="aws.operators.redshift_cluster.RedshiftResumeClusterOperator"></a>

## RedshiftResumeClusterOperator Objects

```python
class RedshiftResumeClusterOperator(BaseOperator)
```

Resume a paused AWS Redshift Cluster

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RedshiftResumeClusterOperator`

**Arguments**:

- `cluster_identifier`: id of the AWS Redshift Cluster
- `aws_conn_id`: aws connection to use

<a id="aws.operators.redshift_cluster.RedshiftPauseClusterOperator"></a>

## RedshiftPauseClusterOperator Objects

```python
class RedshiftPauseClusterOperator(BaseOperator)
```

Pause an AWS Redshift Cluster if it has status `available`.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RedshiftPauseClusterOperator`

**Arguments**:

- `cluster_identifier`: id of the AWS Redshift Cluster
- `aws_conn_id`: aws connection to use

<a id="aws.operators.sagemaker_processing"></a>

# aws.operators.sagemaker\_processing

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.s3_copy_object"></a>

# aws.operators.s3\_copy\_object

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.s3`.

<a id="aws.operators.sqs"></a>

# aws.operators.sqs

Publish message to SQS queue

<a id="aws.operators.sqs.SqsPublishOperator"></a>

## SqsPublishOperator Objects

```python
class SqsPublishOperator(BaseOperator)
```

Publish message to a SQS queue.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SqsPublishOperator`

**Arguments**:

- `sqs_queue`: The SQS queue url (templated)
- `message_content`: The message content (templated)
- `message_attributes`: additional attributes for the message (default: None)
For details of the attributes parameter see :py:meth:`botocore.client.SQS.send_message`
- `delay_seconds`: message delay (templated) (default: 1 second)
- `aws_conn_id`: AWS connection id (default: aws_default)

<a id="aws.operators.sqs.SqsPublishOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Publish the message to SQS queue

**Arguments**:

- `context`: the context object

**Returns**:

`dict`: dict with information about the message sent
For details of the returned dict see :py:meth:`botocore.client.SQS.send_message`

<a id="aws.operators.sqs.SQSPublishOperator"></a>

## SQSPublishOperator Objects

```python
class SQSPublishOperator(SqsPublishOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.sqs.SqsPublishOperator`.

<a id="aws.operators.eks"></a>

# aws.operators.eks

This module contains Amazon EKS operators.

<a id="aws.operators.eks.EksCreateClusterOperator"></a>

## EksCreateClusterOperator Objects

```python
class EksCreateClusterOperator(BaseOperator)
```

Creates an Amazon EKS Cluster control plane.

Optionally, can also create the supporting compute architecture:

 - If argument 'compute' is provided with a value of 'nodegroup', will also
     attempt to create an Amazon EKS Managed Nodegroup for the cluster.
     See :class:`~airflow.providers.amazon.aws.operators.EksCreateNodegroupOperator`
     documentation for requirements.

-  If argument 'compute' is provided with a value of 'fargate', will also attempt to create an AWS
     Fargate profile for the cluster.
     See :class:`~airflow.providers.amazon.aws.operators.EksCreateFargateProfileOperator`
     documentation for requirements.


.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EksCreateClusterOperator`

**Arguments**:

- `cluster_name`: The unique name to give to your Amazon EKS Cluster. (templated)
- `cluster_role_arn`: The Amazon Resource Name (ARN) of the IAM role that provides permissions for the
Kubernetes control plane to make calls to AWS API operations on your behalf. (templated)
- `resources_vpc_config`: The VPC configuration used by the cluster control plane. (templated)
- `compute`: The type of compute architecture to generate along with the cluster. (templated)
Defaults to 'nodegroup' to generate an EKS Managed Nodegroup.
- `create_cluster_kwargs`: Optional parameters to pass to the CreateCluster API (templated)
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.

If compute is assigned the value of 'nodegroup':
- `nodegroup_name`: *REQUIRED* The unique name to give your Amazon EKS managed node group. (templated)
- `nodegroup_role_arn`: *REQUIRED* The Amazon Resource Name (ARN) of the IAM role to associate with
the Amazon EKS managed node group. (templated)
- `create_nodegroup_kwargs`: Optional parameters to pass to the CreateNodegroup API (templated)
If compute is assigned the value of 'fargate':
- `fargate_profile_name`: *REQUIRED* The unique name to give your AWS Fargate profile. (templated)
- `fargate_pod_execution_role_arn`: *REQUIRED* The Amazon Resource Name (ARN) of the pod execution
role to use for pods that match the selectors in the AWS Fargate profile. (templated)
- `fargate_selectors`: The selectors to match for pods to use this AWS Fargate profile. (templated)
- `create_fargate_profile_kwargs`: Optional parameters to pass to the CreateFargateProfile API
(templated)

<a id="aws.operators.eks.EksCreateNodegroupOperator"></a>

## EksCreateNodegroupOperator Objects

```python
class EksCreateNodegroupOperator(BaseOperator)
```

Creates an Amazon EKS managed node group for an existing Amazon EKS Cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EksCreateNodegroupOperator`

**Arguments**:

- `cluster_name`: The name of the Amazon EKS Cluster to create the managed nodegroup in. (templated)
- `nodegroup_name`: The unique name to give your managed nodegroup. (templated)
- `nodegroup_subnets`: The subnets to use for the Auto Scaling group that is created for the managed nodegroup. (templated)
- `nodegroup_role_arn`: The Amazon Resource Name (ARN) of the IAM role to associate with the managed nodegroup. (templated)
- `create_nodegroup_kwargs`: Optional parameters to pass to the Create Nodegroup API (templated)
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.

<a id="aws.operators.eks.EksCreateFargateProfileOperator"></a>

## EksCreateFargateProfileOperator Objects

```python
class EksCreateFargateProfileOperator(BaseOperator)
```

Creates an AWS Fargate profile for an Amazon EKS cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EksCreateFargateProfileOperator`

**Arguments**:

- `cluster_name`: The name of the Amazon EKS cluster to apply the AWS Fargate profile to. (templated)
- `pod_execution_role_arn`: The Amazon Resource Name (ARN) of the pod execution role to
use for pods that match the selectors in the AWS Fargate profile. (templated)
- `selectors`: The selectors to match for pods to use this AWS Fargate profile. (templated)
- `fargate_profile_name`: The unique name to give your AWS Fargate profile. (templated)
- `create_fargate_profile_kwargs`: Optional parameters to pass to the CreateFargate Profile API
(templated)
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.

<a id="aws.operators.eks.EksDeleteClusterOperator"></a>

## EksDeleteClusterOperator Objects

```python
class EksDeleteClusterOperator(BaseOperator)
```

Deletes the Amazon EKS Cluster control plane and all nodegroups attached to it.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EksDeleteClusterOperator`

**Arguments**:

- `cluster_name`: The name of the Amazon EKS Cluster to delete. (templated)
- `force_delete_compute`: If True, will delete any attached resources. (templated)
Defaults to False.
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.

<a id="aws.operators.eks.EksDeleteClusterOperator.delete_any_nodegroups"></a>

#### delete\_any\_nodegroups

```python
def delete_any_nodegroups(eks_hook) -> None
```

Deletes all Amazon EKS managed node groups for a provided Amazon EKS Cluster.

Amazon EKS managed node groups can be deleted in parallel, so we can send all
of the delete commands in bulk and move on once the count of nodegroups is zero.

<a id="aws.operators.eks.EksDeleteClusterOperator.delete_any_fargate_profiles"></a>

#### delete\_any\_fargate\_profiles

```python
def delete_any_fargate_profiles(eks_hook) -> None
```

Deletes all EKS Fargate profiles for a provided Amazon EKS Cluster.

EKS Fargate profiles must be deleted one at a time, so we must wait
for one to be deleted before sending the next delete command.

<a id="aws.operators.eks.EksDeleteNodegroupOperator"></a>

## EksDeleteNodegroupOperator Objects

```python
class EksDeleteNodegroupOperator(BaseOperator)
```

Deletes an Amazon EKS managed node group from an Amazon EKS Cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EksDeleteNodegroupOperator`

**Arguments**:

- `cluster_name`: The name of the Amazon EKS Cluster associated with your nodegroup. (templated)
- `nodegroup_name`: The name of the nodegroup to delete. (templated)
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used.  If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.

<a id="aws.operators.eks.EksDeleteFargateProfileOperator"></a>

## EksDeleteFargateProfileOperator Objects

```python
class EksDeleteFargateProfileOperator(BaseOperator)
```

Deletes an AWS Fargate profile from an Amazon EKS Cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EksDeleteFargateProfileOperator`

**Arguments**:

- `cluster_name`: The name of the Amazon EKS cluster associated with your Fargate profile. (templated)
- `fargate_profile_name`: The name of the AWS Fargate profile to delete. (templated)
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used.  If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.

<a id="aws.operators.eks.EksPodOperator"></a>

## EksPodOperator Objects

```python
class EksPodOperator(KubernetesPodOperator)
```

Executes a task in a Kubernetes pod on the specified Amazon EKS Cluster.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EksPodOperator`

**Arguments**:

- `cluster_name`: The name of the Amazon EKS Cluster to execute the task on. (templated)
- `cluster_role_arn`: The Amazon Resource Name (ARN) of the IAM role that provides permissions
for the Kubernetes control plane to make calls to AWS API operations on your behalf. (templated)
- `in_cluster`: If True, look for config inside the cluster; if False look for a local file path.
- `namespace`: The namespace in which to execute the pod. (templated)
- `pod_name`: The unique name to give the pod. (templated)
- `aws_profile`: The named profile containing the credentials for the AWS CLI tool to use.
- `aws_profile`: str
- `region`: Which AWS region the connection should use. (templated)
If this is None or empty then the default boto3 behaviour is used.
- `aws_conn_id`: The Airflow connection used for AWS credentials. (templated)
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).
- `is_delete_operator_pod`: What to do when the pod reaches its final
state, or the execution is interrupted. If True, delete the
pod; if False, leave the pod.  Current default is False, but this will be
changed in the next major release of this provider.

<a id="aws.operators.eks.EKSCreateClusterOperator"></a>

## EKSCreateClusterOperator Objects

```python
class EKSCreateClusterOperator(EksCreateClusterOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.eks.EksCreateClusterOperator`.

<a id="aws.operators.eks.EKSCreateNodegroupOperator"></a>

## EKSCreateNodegroupOperator Objects

```python
class EKSCreateNodegroupOperator(EksCreateNodegroupOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.eks.EksCreateNodegroupOperator`.

<a id="aws.operators.eks.EKSCreateFargateProfileOperator"></a>

## EKSCreateFargateProfileOperator Objects

```python
class EKSCreateFargateProfileOperator(EksCreateFargateProfileOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.eks.EksCreateFargateProfileOperator`.

<a id="aws.operators.eks.EKSDeleteClusterOperator"></a>

## EKSDeleteClusterOperator Objects

```python
class EKSDeleteClusterOperator(EksDeleteClusterOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.eks.EksDeleteClusterOperator`.

<a id="aws.operators.eks.EKSDeleteNodegroupOperator"></a>

## EKSDeleteNodegroupOperator Objects

```python
class EKSDeleteNodegroupOperator(EksDeleteNodegroupOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.eks.EksDeleteNodegroupOperator`.

<a id="aws.operators.eks.EKSDeleteFargateProfileOperator"></a>

## EKSDeleteFargateProfileOperator Objects

```python
class EKSDeleteFargateProfileOperator(EksDeleteFargateProfileOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.eks.EksDeleteFargateProfileOperator`.

<a id="aws.operators.eks.EKSPodOperator"></a>

## EKSPodOperator Objects

```python
class EKSPodOperator(EksPodOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.eks.EksPodOperator`.

<a id="aws.operators.dms_delete_task"></a>

# aws.operators.dms\_delete\_task

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.dms`.

<a id="aws.operators.emr_terminate_job_flow"></a>

# aws.operators.emr\_terminate\_job\_flow

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.emr`.

<a id="aws.operators.sagemaker_base"></a>

# aws.operators.sagemaker\_base

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.glacier"></a>

# aws.operators.glacier

<a id="aws.operators.glacier.GlacierCreateJobOperator"></a>

## GlacierCreateJobOperator Objects

```python
class GlacierCreateJobOperator(BaseOperator)
```

Initiate an Amazon Glacier inventory-retrieval job

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:GlacierCreateJobOperator`

**Arguments**:

- `aws_conn_id`: The reference to the AWS connection details
- `vault_name`: the Glacier vault on which job is executed

<a id="aws.operators.batch"></a>

# aws.operators.batch

An Airflow operator for AWS Batch services

.. seealso::

    - http://boto3.readthedocs.io/en/latest/guide/configuration.html
    - http://boto3.readthedocs.io/en/latest/reference/services/batch.html
    - https://docs.aws.amazon.com/batch/latest/APIReference/Welcome.html

<a id="aws.operators.batch.BatchOperator"></a>

## BatchOperator Objects

```python
class BatchOperator(BaseOperator)
```

Execute a job on AWS Batch

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:BatchOperator`

**Arguments**:

- `job_name`: the name for the job that will run on AWS Batch (templated)
- `job_definition`: the job definition name on AWS Batch
- `job_queue`: the queue name on AWS Batch
- `overrides`: the `containerOverrides` parameter for boto3 (templated)
- `array_properties`: the `arrayProperties` parameter for boto3
- `parameters`: the `parameters` for boto3 (templated)
- `job_id`: the job ID, usually unknown (None) until the
submit_job operation gets the jobId defined by AWS Batch
- `waiters`: an :py:class:`.BatchWaiters` object (see note below);
if None, polling is used with max_retries and status_retries.
- `max_retries`: exponential back-off retries, 4200 = 48 hours;
polling is only used when waiters is None
- `status_retries`: number of HTTP retries to get job status, 10;
polling is only used when waiters is None
- `aws_conn_id`: connection id of AWS credentials / region name. If None,
credential boto3 strategy will be used.
- `region_name`: region name to use in AWS Hook.
Override the region_name in connection (if provided)
- `tags`: collection of tags to apply to the AWS Batch job submission
if None, no tags are submitted

.. note::
    Any custom waiters must return a waiter for these calls:
    .. code-block:: python

        waiter = waiters.get_waiter("JobExists")
        waiter = waiters.get_waiter("JobRunning")
        waiter = waiters.get_waiter("JobComplete")

<a id="aws.operators.batch.BatchOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Submit and monitor an AWS Batch job

**Raises**:

- `None`: AirflowException

<a id="aws.operators.batch.BatchOperator.submit_job"></a>

#### submit\_job

```python
def submit_job(context: 'Context')
```

Submit an AWS Batch job

**Raises**:

- `None`: AirflowException

<a id="aws.operators.batch.BatchOperator.monitor_job"></a>

#### monitor\_job

```python
def monitor_job(context: 'Context')
```

Monitor an AWS Batch job

monitor_job can raise an exception or an AirflowTaskTimeout can be raised if execution_timeout
is given while creating the task. These exceptions should be handled in taskinstance.py
instead of here like it was previously done

**Raises**:

- `None`: AirflowException

<a id="aws.operators.batch.AwsBatchOperator"></a>

## AwsBatchOperator Objects

```python
class AwsBatchOperator(BatchOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.batch.BatchOperator`.

<a id="aws.operators.emr_add_steps"></a>

# aws.operators.emr\_add\_steps

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.emr`.

<a id="aws.operators.ec2_start_instance"></a>

# aws.operators.ec2\_start\_instance

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.ec2`.

<a id="aws.operators.ec2_stop_instance"></a>

# aws.operators.ec2\_stop\_instance

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.ec2`.

<a id="aws.operators"></a>

# aws.operators

<a id="aws.operators.redshift_sql"></a>

# aws.operators.redshift\_sql

<a id="aws.operators.redshift_sql.RedshiftSQLOperator"></a>

## RedshiftSQLOperator Objects

```python
class RedshiftSQLOperator(BaseOperator)
```

Executes SQL Statements against an Amazon Redshift cluster

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RedshiftSQLOperator`

**Arguments**:

- `sql`: the SQL code to be executed as a single string, or
a list of str (sql statements), or a reference to a template file.
Template references are recognized by str ending in '.sql'
- `redshift_conn_id`: reference to
:ref:`Amazon Redshift connection id<howto/connection:redshift>`
- `parameters`: (optional) the parameters to render the SQL query with.
- `autocommit`: if True, each command is automatically committed.
(default value: False)

<a id="aws.operators.redshift_sql.RedshiftSQLOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> RedshiftSQLHook
```

Create and return RedshiftSQLHook.

**Returns**:

`RedshiftSQLHook`: A RedshiftSQLHook instance.

<a id="aws.operators.redshift_sql.RedshiftSQLOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Execute a statement against Amazon Redshift

<a id="aws.operators.sagemaker_endpoint_config"></a>

# aws.operators.sagemaker\_endpoint\_config

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.s3_list"></a>

# aws.operators.s3\_list

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.s3`.

<a id="aws.operators.s3_list_prefixes"></a>

# aws.operators.s3\_list\_prefixes

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.s3`.

<a id="aws.operators.glue"></a>

# aws.operators.glue

<a id="aws.operators.glue.GlueJobOperator"></a>

## GlueJobOperator Objects

```python
class GlueJobOperator(BaseOperator)
```

Creates an AWS Glue Job. AWS Glue is a serverless Spark

ETL service for running Spark Jobs on the AWS cloud.
Language support: Python and Scala

**Arguments**:

- `job_name`: unique job name per AWS Account
- `script_location`: location of ETL script. Must be a local or S3 path
- `job_desc`: job description details
- `concurrent_run_limit`: The maximum number of concurrent runs allowed for a job
- `script_args`: etl script arguments and AWS Glue arguments (templated)
- `retry_limit`: The maximum number of times to retry this job if it fails
- `num_of_dpus`: Number of AWS Glue DPUs to allocate to this Job.
- `region_name`: aws region name (example: us-east-1)
- `s3_bucket`: S3 bucket where logs and local etl script will be uploaded
- `iam_role_name`: AWS IAM Role for Glue Job Execution
- `create_job_kwargs`: Extra arguments for Glue Job Creation
- `run_job_kwargs`: Extra arguments for Glue Job Run
- `wait_for_completion`: Whether or not wait for job run completion. (default: True)

<a id="aws.operators.glue.GlueJobOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Executes AWS Glue Job from Airflow

**Returns**:

the id of the current glue job.

<a id="aws.operators.glue.AwsGlueJobOperator"></a>

## AwsGlueJobOperator Objects

```python
class AwsGlueJobOperator(GlueJobOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.glue.GlueJobOperator`.

<a id="aws.operators.step_function"></a>

# aws.operators.step\_function

<a id="aws.operators.step_function.StepFunctionStartExecutionOperator"></a>

## StepFunctionStartExecutionOperator Objects

```python
class StepFunctionStartExecutionOperator(BaseOperator)
```

An Operator that begins execution of an Step Function State Machine

Additional arguments may be specified and are passed down to the underlying BaseOperator.

.. seealso::
    :class:`~airflow.models.BaseOperator`

**Arguments**:

- `state_machine_arn`: ARN of the Step Function State Machine
- `name`: The name of the execution.
- `state_machine_input`: JSON data input to pass to the State Machine
- `aws_conn_id`: aws connection to uses
- `do_xcom_push`: if True, execution_arn is pushed to XCom with key execution_arn.

<a id="aws.operators.step_function.StepFunctionGetExecutionOutputOperator"></a>

## StepFunctionGetExecutionOutputOperator Objects

```python
class StepFunctionGetExecutionOutputOperator(BaseOperator)
```

An Operator that begins execution of an Step Function State Machine

Additional arguments may be specified and are passed down to the underlying BaseOperator.

.. seealso::
    :class:`~airflow.models.BaseOperator`

**Arguments**:

- `execution_arn`: ARN of the Step Function State Machine Execution
- `aws_conn_id`: aws connection to use, defaults to 'aws_default'

<a id="aws.operators.step_function_start_execution"></a>

# aws.operators.step\_function\_start\_execution

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.step_function`.

<a id="aws.operators.sagemaker"></a>

# aws.operators.sagemaker

<a id="aws.operators.sagemaker.SageMakerBaseOperator"></a>

## SageMakerBaseOperator Objects

```python
class SageMakerBaseOperator(BaseOperator)
```

This is the base operator for all SageMaker operators.

**Arguments**:

- `config`: The configuration necessary to start a training job (templated)
- `aws_conn_id`: The AWS connection ID to use.

<a id="aws.operators.sagemaker.SageMakerBaseOperator.parse_integer"></a>

#### parse\_integer

```python
def parse_integer(config, field)
```

Recursive method for parsing string fields holding integer values to integers.

<a id="aws.operators.sagemaker.SageMakerBaseOperator.parse_config_integers"></a>

#### parse\_config\_integers

```python
def parse_config_integers()
```

Parse the integer fields of training config to integers in case the config is rendered by Jinja and
all fields are str

<a id="aws.operators.sagemaker.SageMakerBaseOperator.expand_role"></a>

#### expand\_role

```python
def expand_role()
```

Placeholder for calling boto3's `expand_role`, which expands an IAM role name into an ARN.

<a id="aws.operators.sagemaker.SageMakerBaseOperator.preprocess_config"></a>

#### preprocess\_config

```python
def preprocess_config()
```

Process the config into a usable form.

<a id="aws.operators.sagemaker.SageMakerBaseOperator.hook"></a>

#### hook

```python
@cached_property
def hook()
```

Return SageMakerHook

<a id="aws.operators.sagemaker.SageMakerProcessingOperator"></a>

## SageMakerProcessingOperator Objects

```python
class SageMakerProcessingOperator(SageMakerBaseOperator)
```

Initiate a SageMaker processing job.

This operator returns The ARN of the processing job created in Amazon SageMaker.

**Arguments**:

- `config`: The configuration necessary to start a processing job (templated).
For details of the configuration parameter see :py:meth:`SageMaker.Client.create_processing_job`
- `aws_conn_id`: The AWS connection ID to use.
- `wait_for_completion`: If wait is set to True, the time interval, in seconds,
that the operation waits to check the status of the processing job.
- `print_log`: if the operator should print the cloudwatch log during processing
- `check_interval`: if wait is set to be true, this is the time interval
in seconds which the operator will check the status of the processing job
- `max_ingestion_time`: If wait is set to True, the operation fails if the processing job
doesn't finish within max_ingestion_time seconds. If you set this parameter to None,
the operation does not timeout.
- `action_if_job_exists`: Behaviour if the job name already exists. Possible options are "increment"
(default) and "fail".

<a id="aws.operators.sagemaker.SageMakerEndpointConfigOperator"></a>

## SageMakerEndpointConfigOperator Objects

```python
class SageMakerEndpointConfigOperator(SageMakerBaseOperator)
```

Create a SageMaker endpoint config.

This operator returns The ARN of the endpoint config created in Amazon SageMaker

**Arguments**:

- `config`: The configuration necessary to create an endpoint config.
For details of the configuration parameter see :py:meth:`SageMaker.Client.create_endpoint_config`
- `aws_conn_id`: The AWS connection ID to use.

<a id="aws.operators.sagemaker.SageMakerEndpointOperator"></a>

## SageMakerEndpointOperator Objects

```python
class SageMakerEndpointOperator(SageMakerBaseOperator)
```

Create a SageMaker endpoint.

This operator returns The ARN of the endpoint created in Amazon SageMaker

**Arguments**:

- `config`: The configuration necessary to create an endpoint.
If you need to create a SageMaker endpoint based on an existed
SageMaker model and an existed SageMaker endpoint config::

    config = endpoint_configuration;

If you need to create all of SageMaker model, SageMaker endpoint-config and SageMaker endpoint::

    config = {
        'Model': model_configuration,
        'EndpointConfig': endpoint_config_configuration,
        'Endpoint': endpoint_configuration
    }

For details of the configuration parameter of model_configuration see
:py:meth:`SageMaker.Client.create_model`

For details of the configuration parameter of endpoint_config_configuration see
:py:meth:`SageMaker.Client.create_endpoint_config`

For details of the configuration parameter of endpoint_configuration see
:py:meth:`SageMaker.Client.create_endpoint`
- `aws_conn_id`: The AWS connection ID to use.
- `wait_for_completion`: Whether the operator should wait until the endpoint creation finishes.
- `check_interval`: If wait is set to True, this is the time interval, in seconds, that this operation
waits before polling the status of the endpoint creation.
- `max_ingestion_time`: If wait is set to True, this operation fails if the endpoint creation doesn't
finish within max_ingestion_time seconds. If you set this parameter to None it never times out.
- `operation`: Whether to create an endpoint or update an endpoint. Must be either 'create or 'update'.

<a id="aws.operators.sagemaker.SageMakerEndpointOperator.create_integer_fields"></a>

#### create\_integer\_fields

```python
def create_integer_fields() -> None
```

Set fields which should be casted to integers.

<a id="aws.operators.sagemaker.SageMakerTransformOperator"></a>

## SageMakerTransformOperator Objects

```python
class SageMakerTransformOperator(SageMakerBaseOperator)
```

Initiate a SageMaker transform job.

This operator returns The ARN of the model created in Amazon SageMaker.

**Arguments**:

- `config`: The configuration necessary to start a transform job (templated).
If you need to create a SageMaker transform job based on an existed SageMaker model::

    config = transform_config

If you need to create both SageMaker model and SageMaker Transform job::

    config = {
        'Model': model_config,
        'Transform': transform_config
    }

For details of the configuration parameter of transform_config see
:py:meth:`SageMaker.Client.create_transform_job`

For details of the configuration parameter of model_config, See:
:py:meth:`SageMaker.Client.create_model`
- `aws_conn_id`: The AWS connection ID to use.
- `wait_for_completion`: Set to True to wait until the transform job finishes.
- `check_interval`: If wait is set to True, the time interval, in seconds,
that this operation waits to check the status of the transform job.
- `max_ingestion_time`: If wait is set to True, the operation fails
if the transform job doesn't finish within max_ingestion_time seconds. If you
set this parameter to None, the operation does not timeout.

<a id="aws.operators.sagemaker.SageMakerTransformOperator.create_integer_fields"></a>

#### create\_integer\_fields

```python
def create_integer_fields() -> None
```

Set fields which should be casted to integers.

<a id="aws.operators.sagemaker.SageMakerTuningOperator"></a>

## SageMakerTuningOperator Objects

```python
class SageMakerTuningOperator(SageMakerBaseOperator)
```

Initiate a SageMaker hyperparameter tuning job.

This operator returns The ARN of the tuning job created in Amazon SageMaker.

**Arguments**:

- `config`: The configuration necessary to start a tuning job (templated).
For details of the configuration parameter see
:py:meth:`SageMaker.Client.create_hyper_parameter_tuning_job`
- `aws_conn_id`: The AWS connection ID to use.
- `wait_for_completion`: Set to True to wait until the tuning job finishes.
- `check_interval`: If wait is set to True, the time interval, in seconds,
that this operation waits to check the status of the tuning job.
- `max_ingestion_time`: If wait is set to True, the operation fails
if the tuning job doesn't finish within max_ingestion_time seconds. If you
set this parameter to None, the operation does not timeout.

<a id="aws.operators.sagemaker.SageMakerModelOperator"></a>

## SageMakerModelOperator Objects

```python
class SageMakerModelOperator(SageMakerBaseOperator)
```

Create a SageMaker model.

This operator returns The ARN of the model created in Amazon SageMaker

**Arguments**:

- `config`: The configuration necessary to create a model.
For details of the configuration parameter see :py:meth:`SageMaker.Client.create_model`
- `aws_conn_id`: The AWS connection ID to use.

<a id="aws.operators.sagemaker.SageMakerTrainingOperator"></a>

## SageMakerTrainingOperator Objects

```python
class SageMakerTrainingOperator(SageMakerBaseOperator)
```

Initiate a SageMaker training job.

This operator returns The ARN of the training job created in Amazon SageMaker.

**Arguments**:

- `config`: The configuration necessary to start a training job (templated).
For details of the configuration parameter see :py:meth:`SageMaker.Client.create_training_job`
- `aws_conn_id`: The AWS connection ID to use.
- `wait_for_completion`: If wait is set to True, the time interval, in seconds,
that the operation waits to check the status of the training job.
- `print_log`: if the operator should print the cloudwatch log during training
- `check_interval`: if wait is set to be true, this is the time interval
in seconds which the operator will check the status of the training job
- `max_ingestion_time`: If wait is set to True, the operation fails if the training job
doesn't finish within max_ingestion_time seconds. If you set this parameter to None,
the operation does not timeout.
- `check_if_job_exists`: If set to true, then the operator will check whether a training job
already exists for the name in the config.
- `action_if_job_exists`: Behaviour if the job name already exists. Possible options are "increment"
(default) and "fail".
This is only relevant if check_if

<a id="aws.operators.sagemaker.SageMakerDeleteModelOperator"></a>

## SageMakerDeleteModelOperator Objects

```python
class SageMakerDeleteModelOperator(SageMakerBaseOperator)
```

Deletes a SageMaker model.

This operator deletes the Model entry created in SageMaker.

**Arguments**:

- `config`: The configuration necessary to delete the model.
For details of the configuration parameter see :py:meth:`SageMaker.Client.delete_model`
- `aws_conn_id`: The AWS connection ID to use.

<a id="aws.operators.ec2"></a>

# aws.operators.ec2

<a id="aws.operators.ec2.EC2StartInstanceOperator"></a>

## EC2StartInstanceOperator Objects

```python
class EC2StartInstanceOperator(BaseOperator)
```

Start AWS EC2 instance using boto3.

**Arguments**:

- `instance_id`: id of the AWS EC2 instance
- `aws_conn_id`: aws connection to use
- `region_name`: (optional) aws region name associated with the client
- `check_interval`: time in seconds that the job should wait in
between each instance state checks until operation is completed

<a id="aws.operators.ec2.EC2StopInstanceOperator"></a>

## EC2StopInstanceOperator Objects

```python
class EC2StopInstanceOperator(BaseOperator)
```

Stop AWS EC2 instance using boto3.

**Arguments**:

- `instance_id`: id of the AWS EC2 instance
- `aws_conn_id`: aws connection to use
- `region_name`: (optional) aws region name associated with the client
- `check_interval`: time in seconds that the job should wait in
between each instance state checks until operation is completed

<a id="aws.operators.sagemaker_endpoint"></a>

# aws.operators.sagemaker\_endpoint

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.s3_delete_objects"></a>

# aws.operators.s3\_delete\_objects

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.s3`.

<a id="aws.operators.sagemaker_transform"></a>

# aws.operators.sagemaker\_transform

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.dms_start_task"></a>

# aws.operators.dms\_start\_task

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.dms`.

<a id="aws.operators.dms_stop_task"></a>

# aws.operators.dms\_stop\_task

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.dms`.

<a id="aws.operators.sagemaker_tuning"></a>

# aws.operators.sagemaker\_tuning

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.datasync"></a>

# aws.operators.datasync

Create, get, update, execute and delete an AWS DataSync Task.

<a id="aws.operators.datasync.DataSyncOperator"></a>

## DataSyncOperator Objects

```python
class DataSyncOperator(BaseOperator)
```

<a id="aws.operators.datasync.DataSyncOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> DataSyncHook
```

Create and return DataSyncHook.

**Returns**:

`DataSyncHook`: An DataSyncHook instance.

<a id="aws.operators.datasync.DataSyncOperator.choose_task"></a>

#### choose\_task

```python
def choose_task(task_arn_list: list) -> Optional[str]
```

Select 1 DataSync TaskArn from a list

<a id="aws.operators.datasync.DataSyncOperator.choose_location"></a>

#### choose\_location

```python
def choose_location(location_arn_list: Optional[List[str]]) -> Optional[str]
```

Select 1 DataSync LocationArn from a list

<a id="aws.operators.datasync.AWSDataSyncOperator"></a>

## AWSDataSyncOperator Objects

```python
class AWSDataSyncOperator(DataSyncOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.datasync.DataSyncOperator`.

<a id="aws.operators.sagemaker_model"></a>

# aws.operators.sagemaker\_model

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.glue_crawler"></a>

# aws.operators.glue\_crawler

<a id="aws.operators.glue_crawler.GlueCrawlerOperator"></a>

## GlueCrawlerOperator Objects

```python
class GlueCrawlerOperator(BaseOperator)
```

Creates, updates and triggers an AWS Glue Crawler. AWS Glue Crawler is a serverless

service that manages a catalog of metadata tables that contain the inferred
schema, format and data types of data stores within the AWS cloud.

**Arguments**:

- `config`: Configurations for the AWS Glue crawler
- `aws_conn_id`: aws connection to use
- `poll_interval`: Time (in seconds) to wait between two consecutive calls to check crawler status

<a id="aws.operators.glue_crawler.GlueCrawlerOperator.hook"></a>

#### hook

```python
@cached_property
def hook() -> GlueCrawlerHook
```

Create and return an GlueCrawlerHook.

<a id="aws.operators.glue_crawler.GlueCrawlerOperator.execute"></a>

#### execute

```python
def execute(context: 'Context')
```

Executes AWS Glue Crawler from Airflow

**Returns**:

the name of the current glue crawler.

<a id="aws.operators.glue_crawler.AwsGlueCrawlerOperator"></a>

## AwsGlueCrawlerOperator Objects

```python
class AwsGlueCrawlerOperator(GlueCrawlerOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.glue_crawler.GlueCrawlerOperator`.

<a id="aws.operators.s3_bucket_tagging"></a>

# aws.operators.s3\_bucket\_tagging

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.s3`.

<a id="aws.operators.emr_create_job_flow"></a>

# aws.operators.emr\_create\_job\_flow

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.emr`.

<a id="aws.operators.dms_create_task"></a>

# aws.operators.dms\_create\_task

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.dms`.

<a id="aws.operators.sagemaker_training"></a>

# aws.operators.sagemaker\_training

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.sagemaker`.

<a id="aws.operators.s3_file_transform"></a>

# aws.operators.s3\_file\_transform

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.s3`.

<a id="aws.operators.athena"></a>

# aws.operators.athena

<a id="aws.operators.athena.AthenaOperator"></a>

## AthenaOperator Objects

```python
class AthenaOperator(BaseOperator)
```

An operator that submits a presto query to athena.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AthenaOperator`

**Arguments**:

- `query`: Presto to be run on athena. (templated)
- `database`: Database to select. (templated)
- `output_location`: s3 path to write the query results into. (templated)
- `aws_conn_id`: aws connection to use
- `client_request_token`: Unique token created by user to avoid multiple executions of same query
- `workgroup`: Athena workgroup in which query will be run
- `query_execution_context`: Context in which query need to be run
- `result_configuration`: Dict with path to store results in and config related to encryption
- `sleep_time`: Time (in seconds) to wait between two consecutive calls to check query status on Athena
- `max_tries`: Number of times to poll for query state before function exits

<a id="aws.operators.athena.AthenaOperator.hook"></a>

#### hook

```python
@cached_property
def hook() -> AthenaHook
```

Create and return an AthenaHook.

<a id="aws.operators.athena.AthenaOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> Optional[str]
```

Run Presto Query on Athena

<a id="aws.operators.athena.AthenaOperator.on_kill"></a>

#### on\_kill

```python
def on_kill() -> None
```

Cancel the submitted athena query

<a id="aws.operators.athena.AWSAthenaOperator"></a>

## AWSAthenaOperator Objects

```python
class AWSAthenaOperator(AthenaOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.athena.AthenaOperator`.

<a id="aws.operators.emr_modify_cluster"></a>

# aws.operators.emr\_modify\_cluster

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.emr`.

<a id="aws.operators.s3"></a>

# aws.operators.s3

This module contains AWS S3 operators.

<a id="aws.operators.s3.S3CreateBucketOperator"></a>

## S3CreateBucketOperator Objects

```python
class S3CreateBucketOperator(BaseOperator)
```

This operator creates an S3 bucket

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:S3CreateBucketOperator`

**Arguments**:

- `bucket_name`: This is bucket name you want to create
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).
- `region_name`: AWS region_name. If not specified fetched from connection.

<a id="aws.operators.s3.S3DeleteBucketOperator"></a>

## S3DeleteBucketOperator Objects

```python
class S3DeleteBucketOperator(BaseOperator)
```

This operator deletes an S3 bucket

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:S3DeleteBucketOperator`

**Arguments**:

- `bucket_name`: This is bucket name you want to delete
- `force_delete`: Forcibly delete all objects in the bucket before deleting the bucket
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.s3.S3GetBucketTaggingOperator"></a>

## S3GetBucketTaggingOperator Objects

```python
class S3GetBucketTaggingOperator(BaseOperator)
```

This operator gets tagging from an S3 bucket

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:S3GetBucketTaggingOperator`

**Arguments**:

- `bucket_name`: This is bucket name you want to reference
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.s3.S3PutBucketTaggingOperator"></a>

## S3PutBucketTaggingOperator Objects

```python
class S3PutBucketTaggingOperator(BaseOperator)
```

This operator puts tagging for an S3 bucket.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:S3PutBucketTaggingOperator`

**Arguments**:

- `bucket_name`: The name of the bucket to add tags to.
- `key`: The key portion of the key/value pair for a tag to be added.
If a key is provided, a value must be provided as well.
- `value`: The value portion of the key/value pair for a tag to be added.
If a value is provided, a key must be provided as well.
- `tag_set`: A List of key/value pairs.
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then the default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.s3.S3DeleteBucketTaggingOperator"></a>

## S3DeleteBucketTaggingOperator Objects

```python
class S3DeleteBucketTaggingOperator(BaseOperator)
```

This operator deletes tagging from an S3 bucket.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:S3DeleteBucketTaggingOperator`

**Arguments**:

- `bucket_name`: This is the name of the bucket to delete tags from.
- `aws_conn_id`: The Airflow connection used for AWS credentials.
If this is None or empty then the default boto3 behaviour is used. If
running Airflow in a distributed manner and aws_conn_id is None or
empty, then default boto3 configuration would be used (and must be
maintained on each worker node).

<a id="aws.operators.s3.S3CopyObjectOperator"></a>

## S3CopyObjectOperator Objects

```python
class S3CopyObjectOperator(BaseOperator)
```

Creates a copy of an object that is already stored in S3.

Note: the S3 connection used here needs to have access to both
source and destination bucket/key.

**Arguments**:

- `source_bucket_key`: The key of the source object. (templated)
It can be either full s3:// style url or relative path from root level.

When it's specified as a full s3:// url, please omit source_bucket_name.
- `dest_bucket_key`: The key of the object to copy to. (templated)
The convention to specify `dest_bucket_key` is the same as `source_bucket_key`.
- `source_bucket_name`: Name of the S3 bucket where the source object is in. (templated)
It should be omitted when `source_bucket_key` is provided as a full s3:// url.
- `dest_bucket_name`: Name of the S3 bucket to where the object is copied. (templated)
It should be omitted when `dest_bucket_key` is provided as a full s3:// url.
- `source_version_id`: Version ID of the source object (OPTIONAL)
- `aws_conn_id`: Connection id of the S3 connection to use
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.

You can provide the following values:

- False: do not validate SSL certificates. SSL will still be used,
         but SSL certificates will not be
         verified.
- path/to/cert/bundle.pem: A filename of the CA cert bundle to uses.
         You can specify this argument if you want to use a different
         CA cert bundle than the one used by botocore.
- `acl_policy`: String specifying the canned ACL policy for the file being
uploaded to the S3 bucket.

<a id="aws.operators.s3.S3DeleteObjectsOperator"></a>

## S3DeleteObjectsOperator Objects

```python
class S3DeleteObjectsOperator(BaseOperator)
```

To enable users to delete single object or multiple objects from

a bucket using a single HTTP request.

**Arguments**:

- `bucket`: Name of the bucket in which you are going to delete object(s). (templated)
- `keys`: The key(s) to delete from S3 bucket. (templated)
When ``keys`` is a string, it's supposed to be the key name of
the single object to delete.

When ``keys`` is a list, it's supposed to be the list of the
keys to delete.
- `prefix`: Prefix of objects to delete. (templated)
All objects matching this prefix in the bucket will be deleted.
- `aws_conn_id`: Connection id of the S3 connection to use
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.

You can provide the following values:

- ``False``: do not validate SSL certificates. SSL will still be used,
         but SSL certificates will not be
         verified.
- ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
         You can specify this argument if you want to use a different
         CA cert bundle than the one used by botocore.

<a id="aws.operators.s3.S3FileTransformOperator"></a>

## S3FileTransformOperator Objects

```python
class S3FileTransformOperator(BaseOperator)
```

Copies data from a source S3 location to a temporary location on the

local filesystem. Runs a transformation on this file as specified by
the transformation script and uploads the output to a destination S3
location.

The locations of the source and the destination files in the local
filesystem is provided as an first and second arguments to the
transformation script. The transformation script is expected to read the
data from source, transform it and write the output to the local
destination file. The operator then takes over control and uploads the
local destination file to S3.

S3 Select is also available to filter the source contents. Users can
omit the transformation script if S3 Select expression is specified.

**Arguments**:

- `source_s3_key`: The key to be retrieved from S3. (templated)
- `dest_s3_key`: The key to be written from S3. (templated)
- `transform_script`: location of the executable transformation script
- `select_expression`: S3 Select expression
- `script_args`: arguments for transformation script (templated)
- `source_aws_conn_id`: source s3 connection
- `source_verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
You can provide the following values:

- ``False``: do not validate SSL certificates. SSL will still be used
     (unless use_ssl is False), but SSL certificates will not be
     verified.
- ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
     You can specify this argument if you want to use a different
     CA cert bundle than the one used by botocore.

This is also applicable to ``dest_verify``.
- `dest_aws_conn_id`: destination s3 connection
- `dest_verify`: Whether or not to verify SSL certificates for S3 connection.
See: ``source_verify``
- `replace`: Replace dest S3 key if it already exists

<a id="aws.operators.s3.S3ListOperator"></a>

## S3ListOperator Objects

```python
class S3ListOperator(BaseOperator)
```

List all objects from the bucket with the given string prefix in name.

This operator returns a python list with the name of objects which can be
used by `xcom` in the downstream task.

**Arguments**:

- `bucket`: The S3 bucket where to find the objects. (templated)
- `prefix`: Prefix string to filters the objects whose name begin with
such prefix. (templated)
- `delimiter`: the delimiter marks key hierarchy. (templated)
- `aws_conn_id`: The connection ID to use when connecting to S3 storage.
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
    You can provide the following values:

    - ``False``: do not validate SSL certificates. SSL will still be used
             (unless use_ssl is False), but SSL certificates will not be
             verified.
    - ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
             You can specify this argument if you want to use a different
             CA cert bundle than the one used by botocore.


**Example**:
    The following operator would list all the files
    (excluding subfolders) from the S3
    ``customers/2018/04/`` key in the ``data`` bucket. ::

        s3_file = S3ListOperator(
            task_id='list_3s_files',
            bucket='data',
            prefix='customers/2018/04/',
            delimiter='/',
            aws_conn_id='aws_customers_conn'
        )

<a id="aws.operators.s3.S3ListPrefixesOperator"></a>

## S3ListPrefixesOperator Objects

```python
class S3ListPrefixesOperator(BaseOperator)
```

List all subfolders from the bucket with the given string prefix in name.

This operator returns a python list with the name of all subfolders which
can be used by `xcom` in the downstream task.

**Arguments**:

- `bucket`: The S3 bucket where to find the subfolders. (templated)
- `prefix`: Prefix string to filter the subfolders whose name begin with
such prefix. (templated)
- `delimiter`: the delimiter marks subfolder hierarchy. (templated)
- `aws_conn_id`: The connection ID to use when connecting to S3 storage.
- `verify`: Whether or not to verify SSL certificates for S3 connection.
By default SSL certificates are verified.
    You can provide the following values:

    - ``False``: do not validate SSL certificates. SSL will still be used
             (unless use_ssl is False), but SSL certificates will not be
             verified.
    - ``path/to/cert/bundle.pem``: A filename of the CA cert bundle to uses.
             You can specify this argument if you want to use a different
             CA cert bundle than the one used by botocore.


**Example**:
    The following operator would list all the subfolders
    from the S3 ``customers/2018/04/`` prefix in the ``data`` bucket. ::

        s3_file = S3ListPrefixesOperator(
            task_id='list_s3_prefixes',
            bucket='data',
            prefix='customers/2018/04/',
            delimiter='/',
            aws_conn_id='aws_customers_conn'
        )

<a id="aws.operators.redshift_data"></a>

# aws.operators.redshift\_data

<a id="aws.operators.redshift_data.RedshiftDataOperator"></a>

## RedshiftDataOperator Objects

```python
class RedshiftDataOperator(BaseOperator)
```

Executes SQL Statements against an Amazon Redshift cluster using Redshift Data

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:RedshiftDataOperator`

**Arguments**:

- `database`: the name of the database
- `sql`: the SQL statement text to run
- `cluster_identifier`: unique identifier of a cluster
- `db_user`: the database username
- `parameters`: the parameters for the SQL statement
- `secret_arn`: the name or ARN of the secret that enables db access
- `statement_name`: the name of the SQL statement
- `with_event`: indicates whether to send an event to EventBridge
- `await_result`: indicates whether to wait for a result, if True wait, if False don't wait
- `poll_interval`: how often in seconds to check the query status
- `aws_conn_id`: aws connection to use
- `region`: aws region to use

<a id="aws.operators.redshift_data.RedshiftDataOperator.hook"></a>

#### hook

```python
@cached_property
def hook() -> RedshiftDataHook
```

Create and return an RedshiftDataHook.

<a id="aws.operators.redshift_data.RedshiftDataOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Execute a statement against Amazon Redshift

<a id="aws.operators.redshift_data.RedshiftDataOperator.on_kill"></a>

#### on\_kill

```python
def on_kill() -> None
```

Cancel the submitted redshift query

<a id="aws.operators.dms_describe_tasks"></a>

# aws.operators.dms\_describe\_tasks

This module is deprecated. Please use :mod:`airflow.providers.amazon.aws.operators.dms`.

<a id="aws.operators.ecs"></a>

# aws.operators.ecs

<a id="aws.operators.ecs.should_retry"></a>

#### should\_retry

```python
def should_retry(exception: Exception)
```

Check if exception is related to ECS resource quota (CPU, MEM).

<a id="aws.operators.ecs.should_retry_eni"></a>

#### should\_retry\_eni

```python
def should_retry_eni(exception: Exception)
```

Check if exception is related to ENI (Elastic Network Interfaces).

<a id="aws.operators.ecs.EcsProtocol"></a>

## EcsProtocol Objects

```python
@runtime_checkable
class EcsProtocol(Protocol)
```

A structured Protocol for ``boto3.client('ecs')``. This is used for type hints on
:py:meth:`.EcsOperator.client`.

.. seealso::

    - https://mypy.readthedocs.io/en/latest/protocols.html
    - https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html

<a id="aws.operators.ecs.EcsProtocol.run_task"></a>

#### run\_task

```python
def run_task(**kwargs) -> Dict
```

https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.run_task

<a id="aws.operators.ecs.EcsProtocol.get_waiter"></a>

#### get\_waiter

```python
def get_waiter(x: str) -> Waiter
```

https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.get_waiter

<a id="aws.operators.ecs.EcsProtocol.describe_tasks"></a>

#### describe\_tasks

```python
def describe_tasks(cluster: str, tasks) -> Dict
```

https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.describe_tasks

<a id="aws.operators.ecs.EcsProtocol.stop_task"></a>

#### stop\_task

```python
def stop_task(cluster, task, reason: str) -> Dict
```

https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.stop_task

<a id="aws.operators.ecs.EcsProtocol.describe_task_definition"></a>

#### describe\_task\_definition

```python
def describe_task_definition(taskDefinition: str) -> Dict
```

https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.describe_task_definition

<a id="aws.operators.ecs.EcsProtocol.list_tasks"></a>

#### list\_tasks

```python
def list_tasks(cluster: str, launchType: str, desiredStatus: str,
               family: str) -> Dict
```

https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.list_tasks

<a id="aws.operators.ecs.EcsTaskLogFetcher"></a>

## EcsTaskLogFetcher Objects

```python
class EcsTaskLogFetcher(Thread)
```

Fetches Cloudwatch log events with specific interval as a thread
and sends the log events to the info channel of the provided logger.

<a id="aws.operators.ecs.EcsOperator"></a>

## EcsOperator Objects

```python
class EcsOperator(BaseOperator)
```

Execute a task on AWS ECS (Elastic Container Service)

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:EcsOperator`

**Arguments**:

- `task_definition`: the task definition name on Elastic Container Service
- `cluster`: the cluster name on Elastic Container Service
- `overrides`: the same parameter that boto3 will receive (templated):
https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.run_task
- `aws_conn_id`: connection id of AWS credentials / region name. If None,
credential boto3 strategy will be used
(http://boto3.readthedocs.io/en/latest/guide/configuration.html).
- `region_name`: region name to use in AWS Hook.
Override the region_name in connection (if provided)
- `launch_type`: the launch type on which to run your task ('EC2', 'EXTERNAL', or 'FARGATE')
- `capacity_provider_strategy`: the capacity provider strategy to use for the task.
When capacity_provider_strategy is specified, the launch_type parameter is omitted.
If no capacity_provider_strategy or launch_type is specified,
the default capacity provider strategy for the cluster is used.
- `group`: the name of the task group associated with the task
- `placement_constraints`: an array of placement constraint objects to use for
the task
- `placement_strategy`: an array of placement strategy objects to use for
the task
- `platform_version`: the platform version on which your task is running
- `network_configuration`: the network configuration for the task
- `tags`: a dictionary of tags in the form of {'tagKey': 'tagValue'}.
- `awslogs_group`: the CloudWatch group where your ECS container logs are stored.
Only required if you want logs to be shown in the Airflow UI after your job has
finished.
- `awslogs_region`: the region in which your CloudWatch logs are stored.
If None, this is the same as the `region_name` parameter. If that is also None,
this is the default AWS region based on your connection settings.
- `awslogs_stream_prefix`: the stream prefix that is used for the CloudWatch logs.
This is usually based on some custom name combined with the name of the container.
Only required if you want logs to be shown in the Airflow UI after your job has
finished.
- `awslogs_fetch_interval`: the interval that the ECS task log fetcher should wait
in between each Cloudwatch logs fetches.
- `quota_retry`: Config if and how to retry the launch of a new ECS task, to handle
transient errors.
- `reattach`: If set to True, will check if the task previously launched by the task_instance
is already running. If so, the operator will attach to it instead of starting a new task.
This is to avoid relaunching a new task when the connection drops between Airflow and ECS while
the task is running (when the Airflow worker is restarted for example).
- `number_logs_exception`: Number of lines from the last Cloudwatch logs to return in the
AirflowException if an ECS task is stopped (to receive Airflow alerts with the logs of what
failed in the code running in ECS).

<a id="aws.operators.ecs.EcsOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> AwsBaseHook
```

Create and return an AwsHook.

<a id="aws.operators.ecs.ECSOperator"></a>

## ECSOperator Objects

```python
class ECSOperator(EcsOperator)
```

This operator is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.ecs.EcsOperator`.

<a id="aws.operators.ecs.ECSTaskLogFetcher"></a>

## ECSTaskLogFetcher Objects

```python
class ECSTaskLogFetcher(EcsTaskLogFetcher)
```

This class is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.ecs.EcsTaskLogFetcher`.

<a id="aws.operators.ecs.ECSProtocol"></a>

## ECSProtocol Objects

```python
class ECSProtocol(EcsProtocol)
```

This class is deprecated.
Please use :class:`airflow.providers.amazon.aws.operators.ecs.EcsProtocol`.

<a id="aws.operators.sns"></a>

# aws.operators.sns

Publish message to SNS queue

<a id="aws.operators.sns.SnsPublishOperator"></a>

## SnsPublishOperator Objects

```python
class SnsPublishOperator(BaseOperator)
```

Publish a message to Amazon SNS.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SnsPublishOperator`

**Arguments**:

- `aws_conn_id`: aws connection to use
- `target_arn`: either a TopicArn or an EndpointArn
- `message`: the default message you want to send (templated)
- `subject`: the message subject you want to send (templated)
- `message_attributes`: the message attributes you want to send as a flat dict (data type will be
determined automatically)

<a id="aws.secrets.secrets_manager"></a>

# aws.secrets.secrets\_manager

Objects relating to sourcing secrets from AWS Secrets Manager

<a id="aws.secrets.secrets_manager.SecretsManagerBackend"></a>

## SecretsManagerBackend Objects

```python
class SecretsManagerBackend(BaseSecretsBackend, LoggingMixin)
```

Retrieves Connection or Variables from AWS Secrets Manager

Configurable via ``airflow.cfg`` like so:

.. code-block:: ini

    [secrets]
    backend = airflow.providers.amazon.aws.secrets.secrets_manager.SecretsManagerBackend
    backend_kwargs = {"connections_prefix": "airflow/connections"}

For example, if secrets prefix is ``airflow/connections/smtp_default``, this would be accessible
if you provide ``{"connections_prefix": "airflow/connections"}`` and request conn_id ``smtp_default``.
If variables prefix is ``airflow/variables/hello``, this would be accessible
if you provide ``{"variables_prefix": "airflow/variables"}`` and request variable key ``hello``.
And if config_prefix is ``airflow/config/sql_alchemy_conn``, this would be accessible
if you provide ``{"config_prefix": "airflow/config"}`` and request config
key ``sql_alchemy_conn``.

You can also pass additional keyword arguments like ``aws_secret_access_key``, ``aws_access_key_id``
or ``region_name`` to this class and they would be passed on to Boto3 client.

There are two ways of storing secrets in Secret Manager for using them with this operator:
storing them as a conn URI in one field, or taking advantage of native approach of Secrets Manager
and storing them in multiple fields. There are certain words that will be searched in the name
of fields for trying to retrieve a connection part. Those words are:

.. code-block:: python

    possible_words_for_conn_fields = {
        "user": ["user", "username", "login", "user_name"],
        "password": ["password", "pass", "key"],
        "host": ["host", "remote_host", "server"],
        "port": ["port"],
        "schema": ["database", "schema"],
        "conn_type": ["conn_type", "conn_id", "connection_type", "engine"],
    }

However, these lists can be extended using the configuration parameter ``extra_conn_words``. Also,
you can have a field named extra for extra parameters for the conn. Please note that this extra field
must be a valid JSON.

**Arguments**:

- `connections_prefix`: Specifies the prefix of the secret to read to get Connections.
If set to None (null value in the configuration), requests for connections will not be
sent to AWS Secrets Manager. If you don't want a connections_prefix, set it as an empty string
- `variables_prefix`: Specifies the prefix of the secret to read to get Variables.
If set to None (null value in the configuration), requests for variables will not be sent to
AWS Secrets Manager. If you don't want a variables_prefix, set it as an empty string
- `config_prefix`: Specifies the prefix of the secret to read to get Configurations.
If set to None (null value in the configuration), requests for configurations will not be sent to
AWS Secrets Manager. If you don't want a config_prefix, set it as an empty string
- `profile_name`: The name of a profile to use. If not given, then the default profile is used.
- `sep`: separator used to concatenate secret_prefix and secret_id. Default: "/"
- `full_url_mode`: if True, the secrets must be stored as one conn URI in just one field per secret.
If False (set it as false in backend_kwargs), you can store the secret using different
fields (password, user...).
- `extra_conn_words`: for using just when you set full_url_mode as false and store
the secrets in different fields of secrets manager. You can add more words for each connection
part beyond the default ones. The extra words to be searched should be passed as a dict of lists,
each list corresponding to a connection part. The optional keys of the dict must be: user,
password, host, schema, conn_type.

<a id="aws.secrets.secrets_manager.SecretsManagerBackend.client"></a>

#### client

```python
@cached_property
def client()
```

Create a Secrets Manager client

<a id="aws.secrets.secrets_manager.SecretsManagerBackend.get_conn_uri"></a>

#### get\_conn\_uri

```python
def get_conn_uri(conn_id: str)
```

Get Connection Value

**Arguments**:

- `conn_id`: connection id

<a id="aws.secrets.secrets_manager.SecretsManagerBackend.get_variable"></a>

#### get\_variable

```python
def get_variable(key: str) -> Optional[str]
```

Get Airflow Variable from Environment Variable

**Arguments**:

- `key`: Variable Key

**Returns**:

Variable Value

<a id="aws.secrets.secrets_manager.SecretsManagerBackend.get_config"></a>

#### get\_config

```python
def get_config(key: str) -> Optional[str]
```

Get Airflow Configuration

**Arguments**:

- `key`: Configuration Option Key

**Returns**:

Configuration Option Value

<a id="aws.secrets.systems_manager"></a>

# aws.secrets.systems\_manager

Objects relating to sourcing connections from AWS SSM Parameter Store

<a id="aws.secrets.systems_manager.SystemsManagerParameterStoreBackend"></a>

## SystemsManagerParameterStoreBackend Objects

```python
class SystemsManagerParameterStoreBackend(BaseSecretsBackend, LoggingMixin)
```

Retrieves Connection or Variables from AWS SSM Parameter Store

Configurable via ``airflow.cfg`` like so:

.. code-block:: ini

    [secrets]
    backend = airflow.providers.amazon.aws.secrets.systems_manager.SystemsManagerParameterStoreBackend
    backend_kwargs = {"connections_prefix": "/airflow/connections", "profile_name": null}

For example, if ssm path is ``/airflow/connections/smtp_default``, this would be accessible
if you provide ``{"connections_prefix": "/airflow/connections"}`` and request conn_id ``smtp_default``.
And if ssm path is ``/airflow/variables/hello``, this would be accessible
if you provide ``{"variables_prefix": "/airflow/variables"}`` and request conn_id ``hello``.

**Arguments**:

- `connections_prefix`: Specifies the prefix of the secret to read to get Connections.
If set to None (null), requests for connections will not be sent to AWS SSM Parameter Store.
- `variables_prefix`: Specifies the prefix of the secret to read to get Variables.
If set to None (null), requests for variables will not be sent to AWS SSM Parameter Store.
- `config_prefix`: Specifies the prefix of the secret to read to get Variables.
If set to None (null), requests for configurations will not be sent to AWS SSM Parameter Store.
- `profile_name`: The name of a profile to use. If not given, then the default profile is used.

<a id="aws.secrets.systems_manager.SystemsManagerParameterStoreBackend.client"></a>

#### client

```python
@cached_property
def client()
```

Create a SSM client

<a id="aws.secrets.systems_manager.SystemsManagerParameterStoreBackend.get_conn_uri"></a>

#### get\_conn\_uri

```python
def get_conn_uri(conn_id: str) -> Optional[str]
```

Get param value

**Arguments**:

- `conn_id`: connection id

<a id="aws.secrets.systems_manager.SystemsManagerParameterStoreBackend.get_variable"></a>

#### get\_variable

```python
def get_variable(key: str) -> Optional[str]
```

Get Airflow Variable from Environment Variable

**Arguments**:

- `key`: Variable Key

**Returns**:

Variable Value

<a id="aws.secrets.systems_manager.SystemsManagerParameterStoreBackend.get_config"></a>

#### get\_config

```python
def get_config(key: str) -> Optional[str]
```

Get Airflow Configuration

**Arguments**:

- `key`: Configuration Option Key

**Returns**:

Configuration Option Value

<a id="aws.secrets"></a>

# aws.secrets

<a id="aws.utils.redshift"></a>

# aws.utils.redshift

<a id="aws.utils.redshift.build_credentials_block"></a>

#### build\_credentials\_block

```python
def build_credentials_block(credentials: ReadOnlyCredentials) -> str
```

Generate AWS credentials block for Redshift COPY and UNLOAD

commands, as noted in AWS docs
https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-authorization.html#copy-credentials

**Arguments**:

- `credentials`: ReadOnlyCredentials object from `botocore`

**Returns**:

str

<a id="aws.utils.rds"></a>

# aws.utils.rds

<a id="aws.utils.rds.RdsDbType"></a>

## RdsDbType Objects

```python
class RdsDbType(Enum)
```

Only available types for the RDS

<a id="aws.utils"></a>

# aws.utils

<a id="aws.utils.emailer"></a>

# aws.utils.emailer

Airflow module for email backend using AWS SES

<a id="aws.utils.emailer.send_email"></a>

#### send\_email

