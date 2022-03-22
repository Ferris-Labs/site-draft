---
title: "jenkins"
linkTitle: "jenkins"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     jenkins Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.jenkins_job_trigger"></a>

# operators.jenkins\_job\_trigger

<a id="operators.jenkins_job_trigger.jenkins_request_with_headers"></a>

#### jenkins\_request\_with\_headers

```python
def jenkins_request_with_headers(jenkins_server: Jenkins,
                                 req: Request) -> Optional[JenkinsRequest]
```

We need to get the headers in addition to the body answer

to get the location from them
This function uses jenkins_request method from python-jenkins library
with just the return call changed

**Arguments**:

- `jenkins_server`: The server to query
- `req`: The request to execute

**Returns**:

Dict containing the response body (key body)
and the headers coming along (headers)

<a id="operators.jenkins_job_trigger.JenkinsJobTriggerOperator"></a>

## JenkinsJobTriggerOperator Objects

```python
class JenkinsJobTriggerOperator(BaseOperator)
```

Trigger a Jenkins Job and monitor it's execution.

This operator depend on python-jenkins library,
version >= 0.4.15 to communicate with jenkins server.
You'll also need to configure a Jenkins connection in the connections screen.

**Arguments**:

- `jenkins_connection_id`: The jenkins connection to use for this job
- `job_name`: The name of the job to trigger
- `parameters`: The parameters block provided to jenkins for use in
the API call when triggering a build. (templated)
- `sleep_time`: How long will the operator sleep between each status
request for the job (min 1, default 10)
- `max_try_before_job_appears`: The maximum number of requests to make
while waiting for the job to appears on jenkins server (default 10)
- `allowed_jenkins_states`: Iterable of allowed result jenkins states, default is ``['SUCCESS']``

<a id="operators.jenkins_job_trigger.JenkinsJobTriggerOperator.build_job"></a>

#### build\_job

```python
def build_job(jenkins_server: Jenkins,
              params: ParamType = None) -> Optional[JenkinsRequest]
```

This function makes an API call to Jenkins to trigger a build for 'job_name'

It returned a dict with 2 keys : body and headers.
headers contains also a dict-like object which can be queried to get
the location to poll in the queue.

**Arguments**:

- `jenkins_server`: The jenkins server where the job should be triggered
- `params`: The parameters block to provide to jenkins API call.

**Returns**:

Dict containing the response body (key body)
and the headers coming along (headers)

<a id="operators.jenkins_job_trigger.JenkinsJobTriggerOperator.poll_job_in_queue"></a>

#### poll\_job\_in\_queue

```python
def poll_job_in_queue(location: str, jenkins_server: Jenkins) -> int
```

This method poll the jenkins queue until the job is executed.

When we trigger a job through an API call,
the job is first put in the queue without having a build number assigned.
Thus we have to wait the job exit the queue to know its build number.
To do so, we have to add /api/json (or /api/xml) to the location
returned by the build_job call and poll this file.
When a 'executable' block appears in the json, it means the job execution started
and the field 'number' then contains the build number.

**Arguments**:

- `location`: Location to poll, returned in the header of the build_job call
- `jenkins_server`: The jenkins server to poll

**Returns**:

The build_number corresponding to the triggered job

<a id="operators.jenkins_job_trigger.JenkinsJobTriggerOperator.get_hook"></a>

#### get\_hook

```python
def get_hook() -> JenkinsHook
```

Instantiate jenkins hook

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_jenkins_job_trigger"></a>

# example\_dags.example\_jenkins\_job\_trigger

<a id="hooks"></a>

# hooks

<a id="hooks.jenkins"></a>

# hooks.jenkins

<a id="hooks.jenkins.JenkinsHook"></a>

## JenkinsHook Objects

```python
class JenkinsHook(BaseHook)
```

Hook to manage connection to jenkins server

<a id="hooks.jenkins.JenkinsHook.get_jenkins_server"></a>

#### get\_jenkins\_server

```python
def get_jenkins_server() -> jenkins.Jenkins
```

Get jenkins server

