---
title: "microsoft"
linkTitle: "microsoft"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     microsoft Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="winrm"></a>

# winrm

<a id="winrm.operators"></a>

# winrm.operators

<a id="winrm.operators.winrm"></a>

# winrm.operators.winrm

<a id="winrm.operators.winrm.WinRMOperator"></a>

## WinRMOperator Objects

```python
class WinRMOperator(BaseOperator)
```

WinRMOperator to execute commands on given remote host using the winrm_hook.

**Arguments**:

- `winrm_hook`: predefined ssh_hook to use for remote execution
- `ssh_conn_id`: connection id from airflow Connections
- `remote_host`: remote host to connect
- `command`: command to execute on remote host. (templated)
- `ps_path`: path to powershell, `powershell` for v5.1- and `pwsh` for v6+.
If specified, it will execute the command as powershell script.
- `output_encoding`: the encoding used to decode stout and stderr
- `timeout`: timeout for executing the command.

<a id="winrm.example_dags"></a>

# winrm.example\_dags

<a id="winrm.example_dags.example_winrm"></a>

# winrm.example\_dags.example\_winrm

This is an example dag for using the WinRMOperator.

<a id="winrm.hooks"></a>

# winrm.hooks

<a id="winrm.hooks.winrm"></a>

# winrm.hooks.winrm

Hook for winrm remote execution.

<a id="winrm.hooks.winrm.WinRMHook"></a>

## WinRMHook Objects

```python
class WinRMHook(BaseHook)
```

Hook for winrm remote execution using pywinrm.

**Arguments**:

- `ssh_conn_id`: connection id from airflow Connections from where
all the required parameters can be fetched like username and password.
Thought the priority is given to the param passed during init
- `endpoint`: When not set, endpoint will be constructed like this:
'http://{remote_host}:{remote_port}/wsman'
- `remote_host`: Remote host to connect to. Ignored if `endpoint` is set.
- `remote_port`: Remote port to connect to. Ignored if `endpoint` is set.
- `transport`: transport type, one of 'plaintext' (default), 'kerberos', 'ssl', 'ntlm', 'credssp'
- `username`: username to connect to the remote_host
- `password`: password of the username to connect to the remote_host
- `service`: the service name, default is HTTP
- `keytab`: the path to a keytab file if you are using one
- `ca_trust_path`: Certification Authority trust path
- `cert_pem`: client authentication certificate file path in PEM format
- `cert_key_pem`: client authentication certificate key file path in PEM format
- `server_cert_validation`: whether server certificate should be validated on
Python versions that support it; one of 'validate' (default), 'ignore'
- `kerberos_delegation`: if True, TGT is sent to target server to
allow multiple hops
- `read_timeout_sec`: maximum seconds to wait before an HTTP connect/read times out (default 30).
This value should be slightly higher than operation_timeout_sec,
as the server can block *at least* that long.
- `operation_timeout_sec`: maximum allowed time in seconds for any single wsman
HTTP operation (default 20). Note that operation timeouts while receiving output
(the only wsman operation that should take any significant time,
and where these timeouts are expected) will be silently retried indefinitely.
- `kerberos_hostname_override`: the hostname to use for the kerberos exchange
(defaults to the hostname in the endpoint URL)
- `message_encryption`: Will encrypt the WinRM messages if set
and the transport auth supports message encryption. (Default 'auto')
- `credssp_disable_tlsv1_2`: Whether to disable TLSv1.2 support and work with older
protocols like TLSv1.0, default is False
- `send_cbt`: Will send the channel bindings over a HTTPS channel (Default: True)

<a id="azure"></a>

# azure

<a id="azure.sensors.data_factory"></a>

# azure.sensors.data\_factory

<a id="azure.sensors.data_factory.AzureDataFactoryPipelineRunStatusSensor"></a>

## AzureDataFactoryPipelineRunStatusSensor Objects

```python
class AzureDataFactoryPipelineRunStatusSensor(BaseSensorOperator)
```

Checks the status of a pipeline run.

**Arguments**:

- `azure_data_factory_conn_id`: The connection identifier for connecting to Azure Data Factory.
- `run_id`: The pipeline run identifier.
- `resource_group_name`: The resource group name.
- `factory_name`: The data factory name.

<a id="azure.sensors"></a>

# azure.sensors

<a id="azure.sensors.azure_cosmos"></a>

# azure.sensors.azure\_cosmos

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.sensors.cosmos`.

<a id="azure.sensors.cosmos"></a>

# azure.sensors.cosmos

<a id="azure.sensors.cosmos.AzureCosmosDocumentSensor"></a>

## AzureCosmosDocumentSensor Objects

```python
class AzureCosmosDocumentSensor(BaseSensorOperator)
```

Checks for the existence of a document which

matches the given query in CosmosDB. Example:

.. code-block::

azure_cosmos_sensor = AzureCosmosDocumentSensor(
    database_name="somedatabase_name",
    collection_name="somecollection_name",
    document_id="unique-doc-id",
    azure_cosmos_conn_id="azure_cosmos_default",
    task_id="azure_cosmos_sensor")

**Arguments**:

- `database_name`: Target CosmosDB database_name.
- `collection_name`: Target CosmosDB collection_name.
- `document_id`: The ID of the target document.
- `azure_cosmos_conn_id`: Reference to the
:ref:`Azure CosmosDB connection<howto/connection:azure_cosmos>`.

<a id="azure.sensors.wasb"></a>

# azure.sensors.wasb

<a id="azure.sensors.wasb.WasbBlobSensor"></a>

## WasbBlobSensor Objects

```python
class WasbBlobSensor(BaseSensorOperator)
```

Waits for a blob to arrive on Azure Blob Storage.

**Arguments**:

- `container_name`: Name of the container.
- `blob_name`: Name of the blob.
- `wasb_conn_id`: Reference to the :ref:`wasb connection <howto/connection:wasb>`.
- `check_options`: Optional keyword arguments that
`WasbHook.check_for_blob()` takes.

<a id="azure.sensors.wasb.WasbPrefixSensor"></a>

## WasbPrefixSensor Objects

```python
class WasbPrefixSensor(BaseSensorOperator)
```

Waits for blobs matching a prefix to arrive on Azure Blob Storage.

**Arguments**:

- `container_name`: Name of the container.
- `prefix`: Prefix of the blob.
- `wasb_conn_id`: Reference to the wasb connection.
- `check_options`: Optional keyword arguments that
`WasbHook.check_for_prefix()` takes.

<a id="azure.operators.adx"></a>

# azure.operators.adx

This module contains Azure Data Explorer operators

<a id="azure.operators.adx.AzureDataExplorerQueryOperator"></a>

## AzureDataExplorerQueryOperator Objects

```python
class AzureDataExplorerQueryOperator(BaseOperator)
```

Operator for querying Azure Data Explorer (Kusto).

**Arguments**:

- `query`: KQL query to run (templated).
- `database`: Database to run the query on (templated).
- `options`: Optional query options. See:
https://docs.microsoft.com/en-us/azure/kusto/api/netfx/request-properties#list-of-clientrequestproperties
- `azure_data_explorer_conn_id`: Reference to the
:ref:`Azure Data Explorer connection<howto/connection:adx>`.

<a id="azure.operators.adx.AzureDataExplorerQueryOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> AzureDataExplorerHook
```

Returns new instance of AzureDataExplorerHook

<a id="azure.operators.adx.AzureDataExplorerQueryOperator.execute"></a>

#### execute

```python
def execute(context: "Context") -> Union[KustoResultTable, str]
```

Run KQL Query on Azure Data Explorer (Kusto).
Returns `PrimaryResult` of Query v2 HTTP response contents
(https://docs.microsoft.com/en-us/azure/kusto/api/rest/response2)

<a id="azure.operators.adls_list"></a>

# azure.operators.adls\_list

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.operators.adls`.

<a id="azure.operators.adls_list.AzureDataLakeStorageListOperator"></a>

## AzureDataLakeStorageListOperator Objects

```python
class AzureDataLakeStorageListOperator(ADLSListOperator)
```

This class is deprecated.
Please use `airflow.providers.microsoft.azure.operators.adls.ADLSListOperator`.

<a id="azure.operators.batch"></a>

# azure.operators.batch

<a id="azure.operators.batch.AzureBatchOperator"></a>

## AzureBatchOperator Objects

```python
class AzureBatchOperator(BaseOperator)
```

Executes a job on Azure Batch Service

**Arguments**:

- `batch_pool_id`: A string that uniquely identifies the Pool within the Account.
- `batch_pool_vm_size`: The size of virtual machines in the Pool
- `batch_job_id`: A string that uniquely identifies the Job within the Account.
- `batch_task_command_line`: The command line of the Task
- `batch_task_id`: A string that uniquely identifies the task within the Job.
- `batch_pool_display_name`: The display name for the Pool.
The display name need not be unique
- `batch_job_display_name`: The display name for the Job.
The display name need not be unique
- `batch_job_manager_task`: Details of a Job Manager Task to be launched when the Job is started.
- `batch_job_preparation_task`: The Job Preparation Task. If set, the Batch service will
run the Job Preparation Task on a Node before starting any Tasks of that
Job on that Compute Node. Required if batch_job_release_task is set.
- `batch_job_release_task`: The Job Release Task. Use to undo changes to Compute Nodes
made by the Job Preparation Task
- `batch_task_display_name`: The display name for the task.
The display name need not be unique
- `batch_task_container_settings`: The settings for the container under which the Task runs
- `batch_start_task`: A Task specified to run on each Compute Node as it joins the Pool.
The Task runs when the Compute Node is added to the Pool or
when the Compute Node is restarted.
- `batch_max_retries`: The number of times to retry this batch operation before it's
considered a failed operation. Default is 3
- `batch_task_resource_files`: A list of files that the Batch service will
download to the Compute Node before running the command line.
- `batch_task_output_files`: A list of files that the Batch service will upload
from the Compute Node after running the command line.
- `batch_task_user_identity`: The user identity under which the Task runs.
If omitted, the Task runs as a non-administrative user unique to the Task.
- `target_low_priority_nodes`: The desired number of low-priority Compute Nodes in the Pool.
This property must not be specified if enable_auto_scale is set to true.
- `target_dedicated_nodes`: The desired number of dedicated Compute Nodes in the Pool.
This property must not be specified if enable_auto_scale is set to true.
- `enable_auto_scale`: Whether the Pool size should automatically adjust over time. Default is false
- `auto_scale_formula`: A formula for the desired number of Compute Nodes in the Pool.
This property must not be specified if enableAutoScale is set to false.
It is required if enableAutoScale is set to true.
- `azure_batch_conn_id`: The :ref:`Azure Batch connection id<howto/connection:azure_batch>`
- `use_latest_verified_vm_image_and_sku`: Whether to use the latest verified virtual
machine image and sku in the batch account. Default is false.
- `vm_publisher`: The publisher of the Azure Virtual Machines Marketplace Image.
For example, Canonical or MicrosoftWindowsServer. Required if
use_latest_image_and_sku is set to True
- `vm_offer`: The offer type of the Azure Virtual Machines Marketplace Image.
For example, UbuntuServer or WindowsServer. Required if
use_latest_image_and_sku is set to True
- `sku_starts_with`: The starting string of the Virtual Machine SKU. Required if
use_latest_image_and_sku is set to True
- `vm_sku`: The name of the virtual machine sku to use
- `vm_version`: The version of the virtual machine
- `vm_version`: Optional[str]
- `vm_node_agent_sku_id`: The node agent sku id of the virtual machine
- `os_family`: The Azure Guest OS family to be installed on the virtual machines in the Pool.
- `os_version`: The OS family version
- `timeout`: The amount of time to wait for the job to complete in minutes. Default is 25
- `should_delete_job`: Whether to delete job after execution. Default is False
- `should_delete_pool`: Whether to delete pool after execution of jobs. Default is False

<a id="azure.operators.batch.AzureBatchOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> AzureBatchHook
```

Create and return an AzureBatchHook.

<a id="azure.operators.batch.AzureBatchOperator.clean_up"></a>

#### clean\_up

```python
def clean_up(pool_id: Optional[str] = None,
             job_id: Optional[str] = None) -> None
```

Delete the given pool and job in the batch account

**Arguments**:

- `pool_id`: The id of the pool to delete
- `job_id`: The id of the job to delete

<a id="azure.operators.data_factory"></a>

# azure.operators.data\_factory

<a id="azure.operators.data_factory.AzureDataFactoryPipelineRunLink"></a>

## AzureDataFactoryPipelineRunLink Objects

```python
class AzureDataFactoryPipelineRunLink(BaseOperatorLink)
```

Constructs a link to monitor a pipeline run in Azure Data Factory.

<a id="azure.operators.data_factory.AzureDataFactoryRunPipelineOperator"></a>

## AzureDataFactoryRunPipelineOperator Objects

```python
class AzureDataFactoryRunPipelineOperator(BaseOperator)
```

Executes a data factory pipeline.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AzureDataFactoryRunPipelineOperator`

**Arguments**:

- `azure_data_factory_conn_id`: The connection identifier for connecting to Azure Data Factory.
- `pipeline_name`: The name of the pipeline to execute.
- `wait_for_termination`: Flag to wait on a pipeline run's termination.  By default, this feature is
enabled but could be disabled to perform an asynchronous wait for a long-running pipeline execution
using the ``AzureDataFactoryPipelineRunSensor``.
- `resource_group_name`: The resource group name. If a value is not passed in to the operator, the
``AzureDataFactoryHook`` will attempt to use the resource group name provided in the corresponding
connection.
- `factory_name`: The data factory name. If a value is not passed in to the operator, the
``AzureDataFactoryHook`` will attempt to use the factory name name provided in the corresponding
connection.
- `reference_pipeline_run_id`: The pipeline run identifier. If this run ID is specified the parameters
of the specified run will be used to create a new run.
- `is_recovery`: Recovery mode flag. If recovery mode is set to `True`, the specified referenced
pipeline run and the new run will be grouped under the same ``groupId``.
- `start_activity_name`: In recovery mode, the rerun will start from this activity. If not specified,
all activities will run.
- `start_from_failure`: In recovery mode, if set to true, the rerun will start from failed activities.
The property will be used only if ``start_activity_name`` is not specified.
- `parameters`: Parameters of the pipeline run. These parameters are referenced in a pipeline via
``@pipeline().parameters.parameterName`` and will be used only if the ``reference_pipeline_run_id`` is
not specified.
- `timeout`: Time in seconds to wait for a pipeline to reach a terminal status for non-asynchronous
waits. Used only if ``wait_for_termination`` is True.
- `check_interval`: Time in seconds to check on a pipeline run's status for non-asynchronous waits.
Used only if ``wait_for_termination`` is True.

<a id="azure.operators"></a>

# azure.operators

<a id="azure.operators.azure_batch"></a>

# azure.operators.azure\_batch

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.operators.batch`.

<a id="azure.operators.adls_delete"></a>

# azure.operators.adls\_delete

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.operators.adls`.

<a id="azure.operators.adls_delete.AzureDataLakeStorageDeleteOperator"></a>

## AzureDataLakeStorageDeleteOperator Objects

```python
class AzureDataLakeStorageDeleteOperator(ADLSDeleteOperator)
```

This class is deprecated.
Please use `airflow.providers.microsoft.azure.operators.adls.ADLSDeleteOperator`.

<a id="azure.operators.adls"></a>

# azure.operators.adls

<a id="azure.operators.adls.ADLSDeleteOperator"></a>

## ADLSDeleteOperator Objects

```python
class ADLSDeleteOperator(BaseOperator)
```

Delete files in the specified path.

.. seealso::
        For more information on how to use this operator, take a look at the guide:
        :ref:`howto/operator:ADLSDeleteOperator`

**Arguments**:

- `path`: A directory or file to remove
- `recursive`: Whether to loop into directories in the location and remove the files
- `ignore_not_found`: Whether to raise error if file to delete is not found
- `azure_data_lake_conn_id`: Reference to the :ref:`Azure Data Lake connection<howto/connection:adl>`.

<a id="azure.operators.adls.ADLSListOperator"></a>

## ADLSListOperator Objects

```python
class ADLSListOperator(BaseOperator)
```

List all files from the specified path

This operator returns a python list with the names of files which can be used by
 `xcom` in the downstream tasks.

**Arguments**:

- `path`: The Azure Data Lake path to find the objects. Supports glob
strings (templated)
- `azure_data_lake_conn_id`: Reference to the :ref:`Azure Data Lake connection<howto/connection:adl>`.
**Example**:
    The following Operator would list all the Parquet files from ``folder/output/``
    folder in the specified ADLS account ::

        adls_files = ADLSListOperator(
            task_id='adls_files',
            path='folder/output/*.parquet',
            azure_data_lake_conn_id='azure_data_lake_default'
        )

<a id="azure.operators.azure_container_instances"></a>

# azure.operators.azure\_container\_instances

This module is deprecated.
Please use :mod:`airflow.providers.microsoft.azure.operators.container_instances`.

<a id="azure.operators.azure_cosmos"></a>

# azure.operators.azure\_cosmos

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.operators.cosmos`.

<a id="azure.operators.container_instances"></a>

# azure.operators.container\_instances

<a id="azure.operators.container_instances.AzureContainerInstancesOperator"></a>

## AzureContainerInstancesOperator Objects

```python
class AzureContainerInstancesOperator(BaseOperator)
```

Start a container on Azure Container Instances

**Arguments**:

- `ci_conn_id`: connection id of a service principal which will be used
to start the container instance
- `registry_conn_id`: connection id of a user which can login to a
private docker registry. For Azure use :ref:`Azure connection id<howto/connection:azure>`
- `resource_group`: name of the resource group wherein this container
instance should be started
- `name`: name of this container instance. Please note this name has
to be unique in order to run containers in parallel.
- `image`: the docker image to be used
- `region`: the region wherein this container instance should be started
- `environment_variables`: key,value pairs containing environment
variables which will be passed to the running container
- `secured_variables`: names of environmental variables that should not
be exposed outside the container (typically passwords).
- `volumes`: list of ``Volume`` tuples to be mounted to the container.
Currently only Azure Fileshares are supported.
- `memory_in_gb`: the amount of memory to allocate to this container
- `cpu`: the number of cpus to allocate to this container
- `gpu`: GPU Resource for the container.
- `command`: the command to run inside the container
- `container_timeout`: max time allowed for the execution of
the container instance.
- `tags`: azure tags as dict of str:str
- `os_type`: The operating system type required by the containers
in the container group. Possible values include: 'Windows', 'Linux'
- `restart_policy`: Restart policy for all containers within the container group.
Possible values include: 'Always', 'OnFailure', 'Never'
- `ip_address`: The IP address type of the container group.
**Example**::

            AzureContainerInstancesOperator(
                ci_conn_id = "azure_service_principal",
                registry_conn_id = "azure_registry_user",
                resource_group = "my-resource-group",
                name = "my-container-name-{{ ds }}",
                image = "myprivateregistry.azurecr.io/my_container:latest",
                region = "westeurope",
                environment_variables = {"MODEL_PATH":  "my_value",
                 "POSTGRES_LOGIN": "{{ macros.connection('postgres_default').login }}",
                 "POSTGRES_PASSWORD": "{{ macros.connection('postgres_default').password }}",
                 "JOB_GUID": "{{ ti.xcom_pull(task_ids='task1', key='guid') }}" },
                secured_variables = ['POSTGRES_PASSWORD'],
                volumes = [("azure_container_instance_conn_id",
                        "my_storage_container",
                        "my_fileshare",
                        "/input-data",
                    True),],
                memory_in_gb=14.0,
                cpu=4.0,
                gpu=GpuResource(count=1, sku='K80'),
                command=["/bin/echo", "world"],
                task_id="start_container"
            )

<a id="azure.operators.cosmos"></a>

# azure.operators.cosmos

<a id="azure.operators.cosmos.AzureCosmosInsertDocumentOperator"></a>

## AzureCosmosInsertDocumentOperator Objects

```python
class AzureCosmosInsertDocumentOperator(BaseOperator)
```

Inserts a new document into the specified Cosmos database and collection

It will create both the database and collection if they do not already exist

**Arguments**:

- `database_name`: The name of the database. (templated)
- `collection_name`: The name of the collection. (templated)
- `document`: The document to insert
- `azure_cosmos_conn_id`: Reference to the
:ref:`Azure CosmosDB connection<howto/connection:azure_cosmos>`.

<a id="azure.operators.wasb_delete_blob"></a>

# azure.operators.wasb\_delete\_blob

<a id="azure.operators.wasb_delete_blob.WasbDeleteBlobOperator"></a>

## WasbDeleteBlobOperator Objects

```python
class WasbDeleteBlobOperator(BaseOperator)
```

Deletes blob(s) on Azure Blob Storage.

**Arguments**:

- `container_name`: Name of the container. (templated)
- `blob_name`: Name of the blob. (templated)
- `wasb_conn_id`: Reference to the :ref:`wasb connection <howto/connection:wasb>`.
- `check_options`: Optional keyword arguments that
`WasbHook.check_for_blob()` takes.
- `is_prefix`: If blob_name is a prefix, delete all files matching prefix.
- `ignore_if_missing`: if True, then return success even if the
blob does not exist.

<a id="azure.secrets"></a>

# azure.secrets

<a id="azure.secrets.key_vault"></a>

# azure.secrets.key\_vault

<a id="azure.secrets.key_vault.AzureKeyVaultBackend"></a>

## AzureKeyVaultBackend Objects

```python
class AzureKeyVaultBackend(BaseSecretsBackend, LoggingMixin)
```

Retrieves Airflow Connections or Variables from Azure Key Vault secrets.

The Azure Key Vault can be configured as a secrets backend in the ``airflow.cfg``:

.. code-block:: ini

    [secrets]
    backend = airflow.providers.microsoft.azure.secrets.key_vault.AzureKeyVaultBackend
    backend_kwargs = {"connections_prefix": "airflow-connections", "vault_url": "<azure_key_vault_uri>"}

For example, if the secrets prefix is ``airflow-connections-smtp-default``, this would be accessible
if you provide ``{"connections_prefix": "airflow-connections"}`` and request conn_id ``smtp-default``.
And if variables prefix is ``airflow-variables-hello``, this would be accessible
if you provide ``{"variables_prefix": "airflow-variables"}`` and request variable key ``hello``.

For client authentication, the ``DefaultAzureCredential`` from the Azure Python SDK is used as
credential provider, which supports service principal, managed identity and user credentials

For example, to specify a service principal with secret you can set the environment variables
``AZURE_TENANT_ID``, ``AZURE_CLIENT_ID`` and ``AZURE_CLIENT_SECRET``.

.. seealso::
    For more details on client authentication refer to the ``DefaultAzureCredential`` Class reference:
    https://docs.microsoft.com/en-us/python/api/azure-identity/azure.identity.defaultazurecredential?view=azure-python

**Arguments**:

- `connections_prefix`: Specifies the prefix of the secret to read to get Connections
If set to None (null), requests for connections will not be sent to Azure Key Vault
- `variables_prefix`: Specifies the prefix of the secret to read to get Variables
If set to None (null), requests for variables will not be sent to Azure Key Vault
- `config_prefix`: Specifies the prefix of the secret to read to get Variables.
If set to None (null), requests for configurations will not be sent to Azure Key Vault
- `vault_url`: The URL of an Azure Key Vault to use
- `sep`: separator used to concatenate secret_prefix and secret_id. Default: "-"

<a id="azure.secrets.key_vault.AzureKeyVaultBackend.client"></a>

#### client

```python
@cached_property
def client() -> SecretClient
```

Create a Azure Key Vault client.

<a id="azure.secrets.key_vault.AzureKeyVaultBackend.get_conn_uri"></a>

#### get\_conn\_uri

```python
def get_conn_uri(conn_id: str) -> Optional[str]
```

Get an Airflow Connection URI from an Azure Key Vault secret

**Arguments**:

- `conn_id`: The Airflow connection id to retrieve

<a id="azure.secrets.key_vault.AzureKeyVaultBackend.get_variable"></a>

#### get\_variable

```python
def get_variable(key: str) -> Optional[str]
```

Get an Airflow Variable from an Azure Key Vault secret.

**Arguments**:

- `key`: Variable Key

**Returns**:

Variable Value

<a id="azure.secrets.key_vault.AzureKeyVaultBackend.get_config"></a>

#### get\_config

```python
def get_config(key: str) -> Optional[str]
```

Get Airflow Configuration

**Arguments**:

- `key`: Configuration Option Key

**Returns**:

Configuration Option Value

<a id="azure.secrets.key_vault.AzureKeyVaultBackend.build_path"></a>

#### build\_path

```python
@staticmethod
def build_path(path_prefix: str, secret_id: str, sep: str = '-') -> str
```

Given a path_prefix and secret_id, build a valid secret name for the Azure Key Vault Backend.

Also replaces underscore in the path with dashes to support easy switching between
environment variables, so ``connection_default`` becomes ``connection-default``.

**Arguments**:

- `path_prefix`: The path prefix of the secret to retrieve
- `secret_id`: Name of the secret
- `sep`: Separator used to concatenate path_prefix and secret_id

<a id="azure.secrets.azure_key_vault"></a>

# azure.secrets.azure\_key\_vault

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.secrets.key_vault`.

<a id="azure.transfers.azure_blob_to_gcs"></a>

# azure.transfers.azure\_blob\_to\_gcs

<a id="azure.transfers.azure_blob_to_gcs.AzureBlobStorageToGCSOperator"></a>

## AzureBlobStorageToGCSOperator Objects

```python
class AzureBlobStorageToGCSOperator(BaseOperator)
```

Operator transfers data from Azure Blob Storage to specified bucket in Google Cloud Storage

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:AzureBlobStorageToGCSOperator`

**Arguments**:

- `wasb_conn_id`: Reference to the wasb connection.
- `gcp_conn_id`: The connection ID to use when fetching connection info.
- `blob_name`: Name of the blob
- `file_path`: Path to the file to download
- `container_name`: Name of the container
- `bucket_name`: The bucket to upload to
- `object_name`: The object name to set when uploading the file
- `filename`: The local file path to the file to be uploaded
- `gzip`: Option to compress local file or file data for upload
- `delegate_to`: The account to impersonate using domain-wide delegation of authority,
if any. For this to work, the service account making the request must have
domain-wide delegation enabled.
- `impersonation_chain`: Optional service account to impersonate using short-term
credentials, or chained list of accounts required to get the access_token
of the last account in the list, which will be impersonated in the request.
If set as a string, the account must grant the originating account
the Service Account Token Creator IAM role.
If set as a sequence, the identities from the list must grant
Service Account Token Creator IAM role to the directly preceding identity, with first
account from the list granting this role to the originating account.

<a id="azure.transfers.oracle_to_azure_data_lake"></a>

# azure.transfers.oracle\_to\_azure\_data\_lake

<a id="azure.transfers.oracle_to_azure_data_lake.OracleToAzureDataLakeOperator"></a>

## OracleToAzureDataLakeOperator Objects

```python
class OracleToAzureDataLakeOperator(BaseOperator)
```

Moves data from Oracle to Azure Data Lake. The operator runs the query against

Oracle and stores the file locally before loading it into Azure Data Lake.

**Arguments**:

- `filename`: file name to be used by the csv file.
- `azure_data_lake_conn_id`: destination azure data lake connection.
- `azure_data_lake_path`: destination path in azure data lake to put the file.
- `oracle_conn_id`: :ref:`Source Oracle connection <howto/connection:oracle>`.
- `sql`: SQL query to execute against the Oracle database. (templated)
- `sql_params`: Parameters to use in sql query. (templated)
- `delimiter`: field delimiter in the file.
- `encoding`: encoding type for the file.
- `quotechar`: Character to use in quoting.
- `quoting`: Quoting strategy. See unicodecsv quoting for more information.

<a id="azure.transfers.sftp_to_wasb"></a>

# azure.transfers.sftp\_to\_wasb

This module contains SFTP to Azure Blob Storage operator.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator"></a>

## SFTPToWasbOperator Objects

```python
class SFTPToWasbOperator(BaseOperator)
```

Transfer files to Azure Blob Storage from SFTP server.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SFTPToWasbOperator`

**Arguments**:

- `sftp_source_path`: The sftp remote path. This is the specified file path
for downloading the single file or multiple files from the SFTP server.
You can use only one wildcard within your path. The wildcard can appear
inside the path or at the end of the path.
- `container_name`: Name of the container.
- `blob_prefix`: Prefix to name a blob.
- `sftp_conn_id`: The sftp connection id. The name or identifier for
establishing a connection to the SFTP server.
- `wasb_conn_id`: Reference to the wasb connection.
- `load_options`: Optional keyword arguments that
``WasbHook.load_file()`` takes.
- `move_object`: When move object is True, the object is moved instead
of copied to the new location. This is the equivalent of a mv command
as opposed to a cp command.
- `wasb_overwrite_object`: Whether the blob to be uploaded
should overwrite the current data.
When wasb_overwrite_object is True, it will overwrite the existing data.
If set to False, the operation might fail with
ResourceExistsError in case a blob object already exists.
- `create_container`: Attempt to create the target container prior to uploading the blob. This is
useful if the target container may not exist yet. Defaults to False.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Upload a file from SFTP to Azure Blob Storage.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.get_sftp_files_map"></a>

#### get\_sftp\_files\_map

```python
def get_sftp_files_map() -> List[SftpFile]
```

Get SFTP files from the source path, it may use a WILDCARD to this end.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.get_tree_behavior"></a>

#### get\_tree\_behavior

```python
def get_tree_behavior() -> Tuple[str, Optional[str], Optional[str]]
```

Extracts from source path the tree behavior to interact with the remote folder

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.check_wildcards_limit"></a>

#### check\_wildcards\_limit

```python
def check_wildcards_limit() -> None
```

Check if there are multiple wildcards used in the SFTP source path.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.source_path_contains_wildcard"></a>

#### source\_path\_contains\_wildcard

```python
@property
def source_path_contains_wildcard() -> bool
```

Checks if the SFTP source path contains a wildcard.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.sftp_hook"></a>

#### sftp\_hook

```python
@cached_property
def sftp_hook() -> SFTPHook
```

Property of sftp hook to be re-used.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.get_full_path_blob"></a>

#### get\_full\_path\_blob

```python
def get_full_path_blob(file: str) -> str
```

Get a blob name based on the previous name and a blob_prefix variable

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.copy_files_to_wasb"></a>

#### copy\_files\_to\_wasb

```python
def copy_files_to_wasb(sftp_files: List[SftpFile]) -> List[str]
```

Upload a list of files from sftp_files to Azure Blob Storage with a new Blob Name.

<a id="azure.transfers.sftp_to_wasb.SFTPToWasbOperator.delete_files"></a>

#### delete\_files

```python
def delete_files(uploaded_files: List[str]) -> None
```

Delete files at SFTP which have been moved to Azure Blob Storage.

<a id="azure.transfers"></a>

# azure.transfers

<a id="azure.transfers.local_to_adls"></a>

# azure.transfers.local\_to\_adls

<a id="azure.transfers.local_to_adls.LocalFilesystemToADLSOperator"></a>

## LocalFilesystemToADLSOperator Objects

```python
class LocalFilesystemToADLSOperator(BaseOperator)
```

Upload file(s) to Azure Data Lake

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:LocalFilesystemToADLSOperator`

**Arguments**:

- `local_path`: local path. Can be single file, directory (in which case,
upload recursively) or glob pattern. Recursive glob patterns using `**`
are not supported
- `remote_path`: Remote path to upload to; if multiple files, this is the
directory root to write within
- `nthreads`: Number of threads to use. If None, uses the number of cores.
- `overwrite`: Whether to forcibly overwrite existing files/directories.
If False and remote path is a directory, will quit regardless if any files
would be overwritten or not. If True, only matching filenames are actually
overwritten
- `buffersize`: int [2**22]
Number of bytes for internal buffer. This block cannot be bigger than
a chunk and cannot be smaller than a block
- `blocksize`: int [2**22]
Number of bytes for a block. Within each chunk, we write a smaller
block for each API call. This block cannot be bigger than a chunk
- `extra_upload_options`: Extra upload options to add to the hook upload method
- `azure_data_lake_conn_id`: Reference to the Azure Data Lake connection

<a id="azure.transfers.local_to_adls.LocalToAzureDataLakeStorageOperator"></a>

## LocalToAzureDataLakeStorageOperator Objects

```python
class LocalToAzureDataLakeStorageOperator(LocalFilesystemToADLSOperator)
```

This class is deprecated.
Please use `airflow.providers.microsoft.azure.transfers.local_to_adls.LocalFilesystemToADLSOperator`.

<a id="azure.transfers.file_to_wasb"></a>

# azure.transfers.file\_to\_wasb

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.transfers.local_to_wasb`.

<a id="azure.transfers.local_to_wasb"></a>

# azure.transfers.local\_to\_wasb

<a id="azure.transfers.local_to_wasb.LocalFilesystemToWasbOperator"></a>

## LocalFilesystemToWasbOperator Objects

```python
class LocalFilesystemToWasbOperator(BaseOperator)
```

Uploads a file to Azure Blob Storage.

**Arguments**:

- `file_path`: Path to the file to load. (templated)
- `container_name`: Name of the container. (templated)
- `blob_name`: Name of the blob. (templated)
- `wasb_conn_id`: Reference to the wasb connection.
- `create_container`: Attempt to create the target container prior to uploading the blob. This is
useful if the target container may not exist yet. Defaults to False.
- `load_options`: Optional keyword arguments that
`WasbHook.load_file()` takes.

<a id="azure.transfers.local_to_wasb.LocalFilesystemToWasbOperator.execute"></a>

#### execute

```python
def execute(context: "Context") -> None
```

Upload a file to Azure Blob Storage.

<a id="azure.example_dags.example_adls_delete"></a>

# azure.example\_dags.example\_adls\_delete

<a id="azure.example_dags.example_local_to_wasb"></a>

# azure.example\_dags.example\_local\_to\_wasb

<a id="azure.example_dags.example_azure_container_instances"></a>

# azure.example\_dags.example\_azure\_container\_instances

This is an example dag for using the AzureContainerInstancesOperator.

<a id="azure.example_dags.example_local_to_adls"></a>

# azure.example\_dags.example\_local\_to\_adls

<a id="azure.example_dags.example_azure_cosmosdb"></a>

# azure.example\_dags.example\_azure\_cosmosdb

This is only an example DAG to highlight usage of AzureCosmosDocumentSensor to detect
if a document now exists.

You can trigger this manually with `airflow dags trigger example_cosmosdb_sensor`.

*Note: Make sure that connection `azure_cosmos_default` is properly set before running
this example.*

<a id="azure.example_dags"></a>

# azure.example\_dags

<a id="azure.example_dags.example_adf_run_pipeline"></a>

# azure.example\_dags.example\_adf\_run\_pipeline

<a id="azure.example_dags.example_sftp_to_wasb"></a>

# azure.example\_dags.example\_sftp\_to\_wasb

<a id="azure.example_dags.example_sftp_to_wasb.delete_sftp_file"></a>

#### delete\_sftp\_file

```python
@task
def delete_sftp_file()
```

Delete a file at SFTP SERVER

<a id="azure.example_dags.example_azure_blob_to_gcs"></a>

# azure.example\_dags.example\_azure\_blob\_to\_gcs

<a id="azure.example_dags.example_fileshare"></a>

# azure.example\_dags.example\_fileshare

<a id="azure.example_dags.example_fileshare.create_fileshare"></a>

#### create\_fileshare

```python
@task
def create_fileshare()
```

Create a fileshare with directory

<a id="azure.example_dags.example_fileshare.delete_fileshare"></a>

#### delete\_fileshare

```python
@task
def delete_fileshare()
```

Delete a fileshare

<a id="azure.hooks.azure_data_factory"></a>

# azure.hooks.azure\_data\_factory

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.hooks.data_factory`.

<a id="azure.hooks.adx"></a>

# azure.hooks.adx

This module contains Azure Data Explorer hook.

.. spelling::

    KustoResponseDataSetV
    kusto

<a id="azure.hooks.adx.AzureDataExplorerHook"></a>

## AzureDataExplorerHook Objects

```python
class AzureDataExplorerHook(BaseHook)
```

Interacts with Azure Data Explorer (Kusto).

**Cluster**:

Azure Data Explorer cluster is specified by a URL, for example: "https://help.kusto.windows.net".
The parameter must be provided through the Data Explorer Cluster URL connection detail.

**Tenant ID**:

To learn about tenants refer to: https://docs.microsoft.com/en-us/onedrive/find-your-office-365-tenant-id

**Authentication methods**:

Available authentication methods are:

  - AAD_APP: Authentication with AAD application certificate. A Tenant ID is required when using this
    method. Provide application ID and application key through Username and Password parameters.

  - AAD_APP_CERT: Authentication with AAD application certificate. Tenant ID, Application PEM Certificate,
    and Application Certificate Thumbprint are required when using this method.

  - AAD_CREDS: Authentication with AAD username and password. A Tenant ID is required when using this
    method. Username and Password parameters are used for authentication with AAD.

  - AAD_DEVICE: Authenticate with AAD device code. Please note that if you choose this option, you'll need
    to authenticate for every new instance that is initialized. It is highly recommended to create one
    instance and use it for all queries.

**Arguments**:

- `azure_data_explorer_conn_id`: Reference to the
:ref:`Azure Data Explorer connection<howto/connection:adx>`.

<a id="azure.hooks.adx.AzureDataExplorerHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="azure.hooks.adx.AzureDataExplorerHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="azure.hooks.adx.AzureDataExplorerHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> KustoClient
```

Return a KustoClient object.

<a id="azure.hooks.adx.AzureDataExplorerHook.run_query"></a>

#### run\_query

```python
def run_query(query: str,
              database: str,
              options: Optional[Dict] = None) -> KustoResponseDataSetV2
```

Run KQL query using provided configuration, and return

`azure.kusto.data.response.KustoResponseDataSet` instance.
If query is unsuccessful AirflowException is raised.

**Arguments**:

- `query`: KQL query to run
- `database`: Database to run the query on.
- `options`: Optional query options. See:
https://docs.microsoft.com/en-us/azure/kusto/api/netfx/request-properties#list-of-clientrequestproperties

**Returns**:

dict

<a id="azure.hooks.azure_container_instance"></a>

# azure.hooks.azure\_container\_instance

This module is deprecated. Please use :mod:`airflow.providers.microsoft.azure.hooks.container_instance`.

<a id="azure.hooks.batch"></a>

# azure.hooks.batch

<a id="azure.hooks.batch.AzureBatchHook"></a>

## AzureBatchHook Objects

```python
class AzureBatchHook(BaseHook)
```

Hook for Azure Batch APIs

**Arguments**:

- `azure_batch_conn_id`: :ref:`Azure Batch connection id<howto/connection:azure_batch>`
of a service principal which will be used to start the container instance.

<a id="azure.hooks.batch.AzureBatchHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="azure.hooks.batch.AzureBatchHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="azure.hooks.batch.AzureBatchHook.get_conn"></a>

#### get\_conn

```python
def get_conn()
```

Get the Batch client connection

**Returns**:

Azure Batch client

<a id="azure.hooks.batch.AzureBatchHook.configure_pool"></a>

#### configure\_pool

