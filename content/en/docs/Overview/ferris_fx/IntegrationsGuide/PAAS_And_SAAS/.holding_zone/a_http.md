---
title: "http"
linkTitle: "http"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     http Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.http"></a>

# sensors.http

<a id="sensors.http.HttpSensor"></a>

## HttpSensor Objects

```python
class HttpSensor(BaseSensorOperator)
```

Executes a HTTP GET statement and returns False on failure caused by

404 Not Found or `response_check` returning False.

HTTP Error codes other than 404 (like 403) or Connection Refused Error
would raise an exception and fail the sensor itself directly (no more poking).
To avoid failing the task for other codes than 404, the argument ``extra_option``
can be passed with the value ``{'check_response': False}``. It will make the ``response_check``
be execute for any http status code.

The response check can access the template context to the operator:

    def response_check(response, task_instance):
        # The task_instance is injected, so you can pull data form xcom
        # Other context variables such as dag, ds, execution_date are also available.
        xcom_data = task_instance.xcom_pull(task_ids='pushing_task')
        # In practice you would do something more sensible with this data..
        print(xcom_data)
        return True

    HttpSensor(task_id='my_http_sensor', ..., response_check=response_check)

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:HttpSensor`

**Arguments**:

- `http_conn_id`: The :ref:`http connection<howto/connection:http>` to run the
sensor against
- `method`: The HTTP request method to use
- `endpoint`: The relative part of the full url
- `request_params`: The parameters to be added to the GET url
- `headers`: The HTTP headers to be added to the GET request
- `response_check`: A check against the 'requests' response object.
The callable takes the response object as the first positional argument
and optionally any number of keyword arguments available in the context dictionary.
It should return True for 'pass' and False otherwise.
- `extra_options`: Extra options for the 'requests' library, see the
'requests' documentation (options to modify timeout, ssl, etc.)

<a id="operators"></a>

# operators

<a id="operators.http"></a>

# operators.http

<a id="operators.http.SimpleHttpOperator"></a>

## SimpleHttpOperator Objects

```python
class SimpleHttpOperator(BaseOperator)
```

Calls an endpoint on an HTTP system to execute an action

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:SimpleHttpOperator`

**Arguments**:

- `http_conn_id`: The :ref:`http connection<howto/connection:http>` to run
the operator against
- `endpoint`: The relative part of the full url. (templated)
- `method`: The HTTP method to use, default = "POST"
- `data`: The data to pass. POST-data in POST/PUT and params
in the URL for a GET request. (templated)
- `headers`: The HTTP headers to be added to the GET request
- `response_check`: A check against the 'requests' response object.
The callable takes the response object as the first positional argument
and optionally any number of keyword arguments available in the context dictionary.
It should return True for 'pass' and False otherwise.
- `response_filter`: A function allowing you to manipulate the response
text. e.g response_filter=lambda response: json.loads(response.text).
The callable takes the response object as the first positional argument
and optionally any number of keyword arguments available in the context dictionary.
- `extra_options`: Extra options for the 'requests' library, see the
'requests' documentation (options to modify timeout, ssl, etc.)
- `log_response`: Log the response (default: False)
- `auth_type`: The auth type for the service

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_http"></a>

# example\_dags.example\_http

Example HTTP operator and sensor

<a id="hooks"></a>

# hooks

<a id="hooks.http"></a>

# hooks.http

<a id="hooks.http.HttpHook"></a>

## HttpHook Objects

```python
class HttpHook(BaseHook)
```

Interact with HTTP servers.

**Arguments**:

- `method`: the API method to be called
- `http_conn_id`: :ref:`http connection<howto/connection:http>` that has the base
API url i.e https://www.google.com/ and optional authentication credentials. Default
headers can also be specified in the Extra field in json format.
- `auth_type`: The auth type for the service

<a id="hooks.http.HttpHook.get_conn"></a>

#### get\_conn

```python
def get_conn(headers: Optional[Dict[Any, Any]] = None) -> requests.Session
```

Returns http session for use with requests

**Arguments**:

- `headers`: additional headers to be passed through as a dictionary

<a id="hooks.http.HttpHook.check_response"></a>

#### check\_response

```python
def check_response(response: requests.Response) -> None
```

Checks the status code and raise an AirflowException exception on non 2XX or 3XX

status codes

**Arguments**:

- `response`: A requests response object

<a id="hooks.http.HttpHook.run_and_check"></a>

#### run\_and\_check

```python
def run_and_check(session: requests.Session,
                  prepped_request: requests.PreparedRequest,
                  extra_options: Dict[Any, Any]) -> Any
```

Grabs extra options like timeout and actually runs the request,

checking for the result

**Arguments**:

- `session`: the session to be used to execute the request
- `prepped_request`: the prepared request generated in run()
- `extra_options`: additional options to be used when executing the request
i.e. ``{'check_response': False}`` to avoid checking raising exceptions on non 2XX
or 3XX status codes

<a id="hooks.http.HttpHook.run_with_advanced_retry"></a>

#### run\_with\_advanced\_retry

```python
def run_with_advanced_retry(_retry_args: Dict[Any, Any], *args: Any,
                            **kwargs: Any) -> Any
```

Runs Hook.run() with a Tenacity decorator attached to it. This is useful for

connectors which might be disturbed by intermittent issues and should not
instantly fail.

**Arguments**:

- `_retry_args`: Arguments which define the retry behaviour.
See Tenacity documentation at https://github.com/jd/tenacity


.. code-block:: python

    hook = HttpHook(http_conn_id="my_conn", method="GET")
    retry_args = dict(
        wait=tenacity.wait_exponential(),
        stop=tenacity.stop_after_attempt(10),
        retry=requests.exceptions.ConnectionError,
    )
    hook.run_with_advanced_retry(endpoint="v1/test", _retry_args=retry_args)

<a id="hooks.http.HttpHook.url_from_endpoint"></a>

#### url\_from\_endpoint

```python
def url_from_endpoint(endpoint: Optional[str]) -> str
```

Combine base url with endpoint

<a id="hooks.http.HttpHook.test_connection"></a>

#### test\_connection

```python
def test_connection()
```

Test HTTP Connection

