---
title: "cncf"
linkTitle: "cncf"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     cncf Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="kubernetes"></a>

# kubernetes

<a id="kubernetes.sensors"></a>

# kubernetes.sensors

<a id="kubernetes.sensors.spark_kubernetes"></a>

# kubernetes.sensors.spark\_kubernetes

<a id="kubernetes.sensors.spark_kubernetes.SparkKubernetesSensor"></a>

## SparkKubernetesSensor Objects

```python
class SparkKubernetesSensor(BaseSensorOperator)
```

Checks sparkApplication object in kubernetes cluster:

.. seealso::
    For more detail about Spark Application Object have a look at the reference:
    https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/blob/v1beta2-1.1.0-2.4.5/docs/api-docs.md#sparkapplication

**Arguments**:

- `application_name`: spark Application resource name
- `namespace`: the kubernetes namespace where the sparkApplication reside in
- `kubernetes_conn_id`: The :ref:`kubernetes connection<howto/connection:kubernetes>`
to Kubernetes cluster.
- `attach_log`: determines whether logs for driver pod should be appended to the sensor log
- `api_group`: kubernetes api group of sparkApplication
- `api_version`: kubernetes api version of sparkApplication

<a id="kubernetes.operators"></a>

# kubernetes.operators

<a id="kubernetes.operators.spark_kubernetes"></a>

# kubernetes.operators.spark\_kubernetes

<a id="kubernetes.operators.spark_kubernetes.SparkKubernetesOperator"></a>

## SparkKubernetesOperator Objects

```python
class SparkKubernetesOperator(BaseOperator)
```

Creates sparkApplication object in kubernetes cluster:

.. seealso::
    For more detail about Spark Application Object have a look at the reference:
    https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/blob/v1beta2-1.1.0-2.4.5/docs/api-docs.md#sparkapplication

**Arguments**:

- `application_file`: Defines Kubernetes 'custom_resource_definition' of 'sparkApplication' as either a
path to a '.json' file or a JSON string.
- `namespace`: kubernetes namespace to put sparkApplication
- `kubernetes_conn_id`: The :ref:`kubernetes connection id <howto/connection:kubernetes>`
for the to Kubernetes cluster.
- `api_group`: kubernetes api group of sparkApplication
- `api_version`: kubernetes api version of sparkApplication

<a id="kubernetes.operators.kubernetes_pod"></a>

# kubernetes.operators.kubernetes\_pod

Executes task in a Kubernetes POD

<a id="kubernetes.operators.kubernetes_pod.PodReattachFailure"></a>

## PodReattachFailure Objects

```python
class PodReattachFailure(AirflowException)
```

When we expect to be able to find a pod but cannot.

<a id="kubernetes.operators.kubernetes_pod.KubernetesPodOperator"></a>

## KubernetesPodOperator Objects

```python
class KubernetesPodOperator(BaseOperator)
```

Execute a task in a Kubernetes Pod

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:KubernetesPodOperator`

.. note::
    If you use `Google Kubernetes Engine <https://cloud.google.com/kubernetes-engine/>`__
    and Airflow is not running in the same cluster, consider using
    :class:`~airflow.providers.google.cloud.operators.kubernetes_engine.GKEStartPodOperator`, which
    simplifies the authorization process.

**Arguments**:

- `namespace`: the namespace to run within kubernetes.
- `image`: Docker image you wish to launch. Defaults to hub.docker.com,
but fully qualified URLS will point to custom repositories. (templated)
- `name`: name of the pod in which the task will run, will be used (plus a random
suffix if random_name_suffix is True) to generate a pod id (DNS-1123 subdomain,
containing only [a-z0-9.-]).
- `random_name_suffix`: if True, will generate a random suffix.
- `cmds`: entrypoint of the container. (templated)
The docker images's entrypoint is used if this is not provided.
- `arguments`: arguments of the entrypoint. (templated)
The docker image's CMD is used if this is not provided.
- `ports`: ports for the launched pod.
- `volume_mounts`: volumeMounts for the launched pod.
- `volumes`: volumes for the launched pod. Includes ConfigMaps and PersistentVolumes.
- `env_vars`: Environment variables initialized in the container. (templated)
- `secrets`: Kubernetes secrets to inject in the container.
They can be exposed as environment vars or files in a volume.
- `in_cluster`: run kubernetes client with in_cluster configuration.
- `cluster_context`: context that points to kubernetes cluster.
Ignored when in_cluster is True. If None, current-context is used.
- `reattach_on_restart`: if the scheduler dies while the pod is running, reattach and monitor
- `labels`: labels to apply to the Pod. (templated)
- `startup_timeout_seconds`: timeout in seconds to startup the pod.
- `get_logs`: get the stdout of the container as logs of the tasks.
- `image_pull_policy`: Specify a policy to cache or always pull an image.
- `annotations`: non-identifying metadata you can attach to the Pod.
Can be a large range of data, and can include characters
that are not permitted by labels.
- `resources`: resources for the launched pod.
- `affinity`: affinity scheduling rules for the launched pod.
- `config_file`: The path to the Kubernetes config file. (templated)
If not specified, default value is ``~/.kube/config``
- `node_selector`: A dict containing a group of scheduling rules.
- `image_pull_secrets`: Any image pull secrets to be given to the pod.
If more than one secret is required, provide a
comma separated list: secret_a,secret_b
- `service_account_name`: Name of the service account
- `is_delete_operator_pod`: What to do when the pod reaches its final
state, or the execution is interrupted. If True (default), delete the
pod; if False, leave the pod.
- `hostnetwork`: If True enable host networking on the pod.
- `tolerations`: A list of kubernetes tolerations.
- `security_context`: security options the pod should run with (PodSecurityContext).
- `dnspolicy`: dnspolicy for the pod.
- `schedulername`: Specify a schedulername for the pod
- `full_pod_spec`: The complete podSpec
- `init_containers`: init container for the launched Pod
- `log_events_on_failure`: Log the pod's events if a failure occurs
- `do_xcom_push`: If True, the content of the file
/airflow/xcom/return.json in the container will also be pushed to an
XCom when the container completes.
- `pod_template_file`: path to pod template file (templated)
- `priority_class_name`: priority class name for the launched Pod
- `termination_grace_period`: Termination grace period if task killed in UI,
defaults to kubernetes default

<a id="kubernetes.operators.kubernetes_pod.KubernetesPodOperator.find_pod"></a>

#### find\_pod

```python
def find_pod(namespace, context) -> Optional[k8s.V1Pod]
```

Returns an already-running pod for this task instance if one exists.

<a id="kubernetes.operators.kubernetes_pod.KubernetesPodOperator.extract_xcom"></a>

#### extract\_xcom

```python
def extract_xcom(pod)
```

Retrieves xcom value and kills xcom sidecar container

<a id="kubernetes.operators.kubernetes_pod.KubernetesPodOperator.patch_already_checked"></a>

#### patch\_already\_checked

```python
def patch_already_checked(pod: k8s.V1Pod)
```

Add an "already checked" annotation to ensure we don't reattach on retries

<a id="kubernetes.operators.kubernetes_pod.KubernetesPodOperator.build_pod_request_obj"></a>

#### build\_pod\_request\_obj

```python
def build_pod_request_obj(context=None)
```

Returns V1Pod object based on pod template file, full pod spec, and other operator parameters.

The V1Pod attributes are derived (in order of precedence) from operator params, full pod spec, pod
template file.

<a id="kubernetes.operators.kubernetes_pod.KubernetesPodOperator.dry_run"></a>

#### dry\_run

```python
def dry_run() -> None
```

Prints out the pod definition that would be created by this operator.
Does not include labels specific to the task instance (since there isn't
one in a dry_run) and excludes all empty elements.

<a id="kubernetes.backcompat.volume_mount"></a>

# kubernetes.backcompat.volume\_mount

Classes for interacting with Kubernetes API

<a id="kubernetes.backcompat.volume_mount.VolumeMount"></a>

## VolumeMount Objects

```python
class VolumeMount()
```

Backward compatible VolumeMount

<a id="kubernetes.backcompat.volume_mount.VolumeMount.__init__"></a>

#### \_\_init\_\_

```python
def __init__(name, mount_path, sub_path, read_only)
```

Initialize a Kubernetes Volume Mount. Used to mount pod level volumes to

running container.

**Arguments**:

- `name`: the name of the volume mount
- `mount_path`: 
- `sub_path`: subpath within the volume mount
- `read_only`: whether to access pod with read-only mode

<a id="kubernetes.backcompat.volume_mount.VolumeMount.to_k8s_client_obj"></a>

#### to\_k8s\_client\_obj

```python
def to_k8s_client_obj() -> k8s.V1VolumeMount
```

Converts to k8s object.

**Returns**:

Volume Mount k8s object

<a id="kubernetes.backcompat.pod"></a>

# kubernetes.backcompat.pod

Classes for interacting with Kubernetes API.

This module is deprecated. Please use :mod:`kubernetes.client.models.V1ResourceRequirements`
and :mod:`kubernetes.client.models.V1ContainerPort`.

<a id="kubernetes.backcompat.pod.Resources"></a>

## Resources Objects

```python
class Resources()
```

backwards compat for Resources.

<a id="kubernetes.backcompat.pod.Resources.__slots__"></a>

#### \_\_slots\_\_

**Arguments**:

- `request_memory`: requested memory
- `request_cpu`: requested CPU number
- `request_ephemeral_storage`: requested ephemeral storage
- `limit_memory`: limit for memory usage
- `limit_cpu`: Limit for CPU used
- `limit_gpu`: Limits for GPU used
- `limit_ephemeral_storage`: Limit for ephemeral storage

<a id="kubernetes.backcompat.pod.Resources.to_k8s_client_obj"></a>

#### to\_k8s\_client\_obj

```python
def to_k8s_client_obj()
```

Converts to k8s object.

@rtype: object

<a id="kubernetes.backcompat.pod.Port"></a>

## Port Objects

```python
class Port()
```

POD port

<a id="kubernetes.backcompat.pod.Port.__init__"></a>

#### \_\_init\_\_

```python
def __init__(name=None, container_port=None)
```

Creates port

<a id="kubernetes.backcompat.pod.Port.to_k8s_client_obj"></a>

#### to\_k8s\_client\_obj

```python
def to_k8s_client_obj()
```

Converts to k8s object.


<a id="kubernetes.backcompat"></a>

# kubernetes.backcompat

<a id="kubernetes.backcompat.volume"></a>

# kubernetes.backcompat.volume

This module is deprecated. Please use :mod:`kubernetes.client.models.V1Volume`.

<a id="kubernetes.backcompat.volume.Volume"></a>

## Volume Objects

```python
class Volume()
```

Backward compatible Volume

<a id="kubernetes.backcompat.volume.Volume.__init__"></a>

#### \_\_init\_\_

```python
def __init__(name, configs)
```

Adds Kubernetes Volume to pod. allows pod to access features like ConfigMaps

and Persistent Volumes

**Arguments**:

- `name`: the name of the volume mount
- `configs`: dictionary of any features needed for volume. We purposely keep this
vague since there are multiple volume types with changing configs.

<a id="kubernetes.backcompat.volume.Volume.to_k8s_client_obj"></a>

#### to\_k8s\_client\_obj

```python
def to_k8s_client_obj() -> k8s.V1Volume
```

Converts to k8s object.

**Returns**:

Volume Mount k8s object

<a id="kubernetes.backcompat.pod_runtime_info_env"></a>

# kubernetes.backcompat.pod\_runtime\_info\_env

Classes for interacting with Kubernetes API.

This module is deprecated. Please use :mod:`kubernetes.client.models.V1EnvVar`.

<a id="kubernetes.backcompat.pod_runtime_info_env.PodRuntimeInfoEnv"></a>

## PodRuntimeInfoEnv Objects

```python
class PodRuntimeInfoEnv()
```

Defines Pod runtime information as environment variable.

<a id="kubernetes.backcompat.pod_runtime_info_env.PodRuntimeInfoEnv.__init__"></a>

#### \_\_init\_\_

```python
def __init__(name, field_path)
```

Adds Kubernetes pod runtime information as environment variables such as namespace, pod IP, pod name.

Full list of options can be found in kubernetes documentation.

**Arguments**:

- `name`: the name of the environment variable
- `field_path`: path to pod runtime info. Ex: metadata.namespace | status.podIP

<a id="kubernetes.backcompat.pod_runtime_info_env.PodRuntimeInfoEnv.to_k8s_client_obj"></a>

#### to\_k8s\_client\_obj

```python
def to_k8s_client_obj()
```

Converts to k8s object.

**Returns**:

kubernetes.client.models.V1EnvVar

<a id="kubernetes.backcompat.backwards_compat_converters"></a>

# kubernetes.backcompat.backwards\_compat\_converters

Executes task in a Kubernetes POD

<a id="kubernetes.backcompat.backwards_compat_converters.convert_volume"></a>

#### convert\_volume

```python
def convert_volume(volume) -> k8s.V1Volume
```

Converts an airflow Volume object into a k8s.V1Volume

**Arguments**:

- `volume`: 

**Returns**:

k8s.V1Volume

<a id="kubernetes.backcompat.backwards_compat_converters.convert_volume_mount"></a>

#### convert\_volume\_mount

```python
def convert_volume_mount(volume_mount) -> k8s.V1VolumeMount
```

Converts an airflow VolumeMount object into a k8s.V1VolumeMount

**Arguments**:

- `volume_mount`: 

**Returns**:

k8s.V1VolumeMount

<a id="kubernetes.backcompat.backwards_compat_converters.convert_resources"></a>

#### convert\_resources

```python
def convert_resources(resources) -> k8s.V1ResourceRequirements
```

Converts an airflow Resources object into a k8s.V1ResourceRequirements

**Arguments**:

- `resources`: 

**Returns**:

k8s.V1ResourceRequirements

<a id="kubernetes.backcompat.backwards_compat_converters.convert_port"></a>

#### convert\_port

```python
def convert_port(port) -> k8s.V1ContainerPort
```

Converts an airflow Port object into a k8s.V1ContainerPort

**Arguments**:

- `port`: 

**Returns**:

k8s.V1ContainerPort

<a id="kubernetes.backcompat.backwards_compat_converters.convert_env_vars"></a>

#### convert\_env\_vars

```python
def convert_env_vars(env_vars) -> List[k8s.V1EnvVar]
```

Converts a dictionary into a list of env_vars

**Arguments**:

- `env_vars`: 

<a id="kubernetes.backcompat.backwards_compat_converters.convert_pod_runtime_info_env"></a>

#### convert\_pod\_runtime\_info\_env

```python
def convert_pod_runtime_info_env(pod_runtime_info_envs) -> k8s.V1EnvVar
```

Converts a PodRuntimeInfoEnv into an k8s.V1EnvVar

**Arguments**:

- `pod_runtime_info_envs`: 

<a id="kubernetes.backcompat.backwards_compat_converters.convert_image_pull_secrets"></a>

#### convert\_image\_pull\_secrets

```python
def convert_image_pull_secrets(
        image_pull_secrets) -> List[k8s.V1LocalObjectReference]
```

Converts a PodRuntimeInfoEnv into an k8s.V1EnvVar

**Arguments**:

- `image_pull_secrets`: 

<a id="kubernetes.backcompat.backwards_compat_converters.convert_configmap"></a>

#### convert\_configmap

```python
def convert_configmap(configmaps) -> k8s.V1EnvFromSource
```

Converts a str into an k8s.V1EnvFromSource

**Arguments**:

- `configmaps`: 

<a id="kubernetes.backcompat.backwards_compat_converters.convert_affinity"></a>

#### convert\_affinity

```python
def convert_affinity(affinity) -> k8s.V1Affinity
```

Converts a dict into an k8s.V1Affinity

<a id="kubernetes.backcompat.backwards_compat_converters.convert_toleration"></a>

#### convert\_toleration

```python
def convert_toleration(toleration) -> k8s.V1Toleration
```

Converts a dict into an k8s.V1Toleration

<a id="kubernetes.utils.pod_manager"></a>

# kubernetes.utils.pod\_manager

Launches PODs

<a id="kubernetes.utils.pod_manager.PodLaunchFailedException"></a>

## PodLaunchFailedException Objects

```python
class PodLaunchFailedException(AirflowException)
```

When pod launching fails in KubernetesPodOperator.

<a id="kubernetes.utils.pod_manager.should_retry_start_pod"></a>

#### should\_retry\_start\_pod

```python
def should_retry_start_pod(exception: BaseException) -> bool
```

Check if an Exception indicates a transient error and warrants retrying

<a id="kubernetes.utils.pod_manager.PodPhase"></a>

## PodPhase Objects

```python
class PodPhase()
```

Possible pod phases
See https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/`pod`-phase.

<a id="kubernetes.utils.pod_manager.container_is_running"></a>

#### container\_is\_running

```python
def container_is_running(pod: V1Pod, container_name: str) -> bool
```

Examines V1Pod ``pod`` to determine whether ``container_name`` is running.
If that container is present and running, returns True.  Returns False otherwise.

<a id="kubernetes.utils.pod_manager.PodManager"></a>

## PodManager Objects

```python
class PodManager(LoggingMixin)
```

Helper class for creating, monitoring, and otherwise interacting with Kubernetes pods
for use with the KubernetesPodOperator

<a id="kubernetes.utils.pod_manager.PodManager.__init__"></a>

#### \_\_init\_\_

```python
def __init__(kube_client: client.CoreV1Api = None,
             in_cluster: bool = True,
             cluster_context: Optional[str] = None)
```

Creates the launcher.

**Arguments**:

- `kube_client`: kubernetes client
- `in_cluster`: whether we are in cluster
- `cluster_context`: context of the cluster

<a id="kubernetes.utils.pod_manager.PodManager.run_pod_async"></a>

#### run\_pod\_async

```python
def run_pod_async(pod: V1Pod, **kwargs) -> V1Pod
```

Runs POD asynchronously

<a id="kubernetes.utils.pod_manager.PodManager.delete_pod"></a>

#### delete\_pod

```python
def delete_pod(pod: V1Pod) -> None
```

Deletes POD

<a id="kubernetes.utils.pod_manager.PodManager.create_pod"></a>

#### create\_pod

```python
@tenacity.retry(
    stop=tenacity.stop_after_attempt(3),
    wait=tenacity.wait_random_exponential(),
    reraise=True,
    retry=tenacity.retry_if_exception(should_retry_start_pod),
)
def create_pod(pod: V1Pod) -> V1Pod
```

Launches the pod asynchronously.

<a id="kubernetes.utils.pod_manager.PodManager.await_pod_start"></a>

#### await\_pod\_start

```python
def await_pod_start(pod: V1Pod, startup_timeout: int = 120) -> None
```

Waits for the pod to reach phase other than ``Pending``

**Arguments**:

- `pod`: 
- `startup_timeout`: Timeout (in seconds) for startup of the pod
(if pod is pending for too long, fails task)

<a id="kubernetes.utils.pod_manager.PodManager.follow_container_logs"></a>

#### follow\_container\_logs

```python
def follow_container_logs(pod: V1Pod, container_name: str) -> None
```

Follows the logs of container and streams to airflow logging.
Returns when container exits.

.. note:: :meth:`read_pod_logs` follows the logs, so we shouldn't necessarily *need* to
    loop as we do here. But in a long-running process we might temporarily lose connectivity.
    So the looping logic is there to let us resume following the logs.

<a id="kubernetes.utils.pod_manager.PodManager.await_pod_completion"></a>

#### await\_pod\_completion

```python
def await_pod_completion(pod: V1Pod) -> V1Pod
```

Monitors a pod and returns the final state

**Arguments**:

- `pod`: pod spec that will be monitored

**Returns**:

Tuple[State, Optional[str]]

<a id="kubernetes.utils.pod_manager.PodManager.parse_log_line"></a>

#### parse\_log\_line

```python
def parse_log_line(line: str) -> Tuple[Optional[DateTime], str]
```

Parse K8s log line and returns the final state

**Arguments**:

- `line`: k8s log line

**Returns**:

`Tuple[str, str]`: timestamp and log message

<a id="kubernetes.utils.pod_manager.PodManager.container_is_running"></a>

#### container\_is\_running

```python
def container_is_running(pod: V1Pod, container_name: str) -> bool
```

Reads pod and checks if container is running

<a id="kubernetes.utils.pod_manager.PodManager.read_pod_logs"></a>

#### read\_pod\_logs

```python
@tenacity.retry(stop=tenacity.stop_after_attempt(3),
                wait=tenacity.wait_exponential(),
                reraise=True)
def read_pod_logs(pod: V1Pod,
                  container_name: str,
                  tail_lines: Optional[int] = None,
                  timestamps: bool = False,
                  since_seconds: Optional[int] = None) -> Iterable[bytes]
```

Reads log from the POD

<a id="kubernetes.utils.pod_manager.PodManager.read_pod_events"></a>

#### read\_pod\_events

```python
@tenacity.retry(stop=tenacity.stop_after_attempt(3),
                wait=tenacity.wait_exponential(),
                reraise=True)
def read_pod_events(pod: V1Pod) -> "CoreV1EventList"
```

Reads events from the POD

<a id="kubernetes.utils.pod_manager.PodManager.read_pod"></a>

#### read\_pod

```python
@tenacity.retry(stop=tenacity.stop_after_attempt(3),
                wait=tenacity.wait_exponential(),
                reraise=True)
def read_pod(pod: V1Pod) -> V1Pod
```

Read POD information

<a id="kubernetes.utils.pod_manager.PodManager.extract_xcom"></a>

#### extract\_xcom

```python
def extract_xcom(pod: V1Pod) -> str
```

Retrieves XCom value and kills xcom sidecar container

<a id="kubernetes.utils"></a>

# kubernetes.utils

<a id="kubernetes.utils.xcom_sidecar"></a>

# kubernetes.utils.xcom\_sidecar

This module handles all xcom functionality for the KubernetesPodOperator
by attaching a sidecar container that blocks the pod from completing until
Airflow has pulled result data into the worker for xcom serialization.

<a id="kubernetes.utils.xcom_sidecar.PodDefaults"></a>

## PodDefaults Objects

```python
class PodDefaults()
```

Static defaults for Pods

<a id="kubernetes.utils.xcom_sidecar.add_xcom_sidecar"></a>

#### add\_xcom\_sidecar

```python
def add_xcom_sidecar(pod: k8s.V1Pod) -> k8s.V1Pod
```

Adds sidecar

<a id="kubernetes.example_dags.example_kubernetes"></a>

# kubernetes.example\_dags.example\_kubernetes

This is an example dag for using the KubernetesPodOperator.

<a id="kubernetes.example_dags"></a>

# kubernetes.example\_dags

<a id="kubernetes.example_dags.example_spark_kubernetes"></a>

# kubernetes.example\_dags.example\_spark\_kubernetes

This is an example DAG which uses SparkKubernetesOperator and SparkKubernetesSensor.
In this example, we create two tasks which execute sequentially.
The first task is to submit sparkApplication on Kubernetes cluster(the example uses spark-pi application).
and the second task is to check the final state of the sparkApplication that submitted in the first state.

Spark-on-k8s operator is required to be already installed on Kubernetes
https://github.com/GoogleCloudPlatform/spark-on-k8s-operator

<a id="kubernetes.hooks"></a>

# kubernetes.hooks

<a id="kubernetes.hooks.kubernetes"></a>

# kubernetes.hooks.kubernetes

<a id="kubernetes.hooks.kubernetes.KubernetesHook"></a>

## KubernetesHook Objects

```python
class KubernetesHook(BaseHook)
```

Creates Kubernetes API connection.

- use in cluster configuration by using ``extra__kubernetes__in_cluster`` in connection
- use custom config by providing path to the file using ``extra__kubernetes__kube_config_path``
- use custom configuration by providing content of kubeconfig file via
    ``extra__kubernetes__kube_config`` in connection
- use default config by providing no extras

This hook check for configuration option in the above order. Once an option is present it will
use this configuration.

.. seealso::
    For more information about Kubernetes connection:
    :doc:`/connections/kubernetes`

**Arguments**:

- `conn_id`: The :ref:`kubernetes connection <howto/connection:kubernetes>`
to Kubernetes cluster.

<a id="kubernetes.hooks.kubernetes.KubernetesHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="kubernetes.hooks.kubernetes.KubernetesHook.get_ui_field_behaviour"></a>

#### get\_ui\_field\_behaviour

```python
@staticmethod
def get_ui_field_behaviour() -> Dict[str, Any]
```

Returns custom field behaviour

<a id="kubernetes.hooks.kubernetes.KubernetesHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Any
```

Returns kubernetes api session for use with requests

<a id="kubernetes.hooks.kubernetes.KubernetesHook.api_client"></a>

#### api\_client

```python
@cached_property
def api_client() -> Any
```

Cached Kubernetes API client

<a id="kubernetes.hooks.kubernetes.KubernetesHook.create_custom_object"></a>

#### create\_custom\_object

```python
def create_custom_object(group: str,
                         version: str,
                         plural: str,
                         body: Union[str, dict],
                         namespace: Optional[str] = None)
```

Creates custom resource definition object in Kubernetes

**Arguments**:

- `group`: api group
- `version`: api version
- `plural`: api plural
- `body`: crd object definition
- `namespace`: kubernetes namespace

<a id="kubernetes.hooks.kubernetes.KubernetesHook.get_custom_object"></a>

#### get\_custom\_object

```python
def get_custom_object(group: str,
                      version: str,
                      plural: str,
                      name: str,
                      namespace: Optional[str] = None)
```

Get custom resource definition object from Kubernetes

**Arguments**:

- `group`: api group
- `version`: api version
- `plural`: api plural
- `name`: crd object name
- `namespace`: kubernetes namespace

<a id="kubernetes.hooks.kubernetes.KubernetesHook.get_namespace"></a>

#### get\_namespace

```python
def get_namespace() -> Optional[str]
```

Returns the namespace that defined in the connection

<a id="kubernetes.hooks.kubernetes.KubernetesHook.get_pod_log_stream"></a>

#### get\_pod\_log\_stream

```python
def get_pod_log_stream(
    pod_name: str,
    container: Optional[str] = "",
    namespace: Optional[str] = None
) -> Tuple[watch.Watch, Generator[str, None, None]]
```

Retrieves a log stream for a container in a kubernetes pod.

**Arguments**:

- `pod_name`: pod name
- `container`: container name
- `namespace`: kubernetes namespace

<a id="kubernetes.hooks.kubernetes.KubernetesHook.get_pod_logs"></a>

#### get\_pod\_logs

```python
def get_pod_logs(pod_name: str,
                 container: Optional[str] = "",
                 namespace: Optional[str] = None)
```

Retrieves a container's log from the specified pod.

**Arguments**:

- `pod_name`: pod name
- `container`: container name
- `namespace`: kubernetes namespace

