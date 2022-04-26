---
title: "grpc"
linkTitle: "grpc"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     grpc Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.grpc"></a>

# operators.grpc

<a id="operators.grpc.GrpcOperator"></a>

## GrpcOperator Objects

```python
class GrpcOperator(BaseOperator)
```

Calls a gRPC endpoint to execute an action

**Arguments**:

- `stub_class`: The stub client to use for this gRPC call
- `call_func`: The client function name to call the gRPC endpoint
- `grpc_conn_id`: The connection to run the operator against
- `data`: The data to pass to the rpc call
- `interceptors`: A list of gRPC interceptor objects to be used on the channel
- `custom_connection_func`: The customized connection function to return channel object.
A callable that accepts the connection as its only arg.
- `streaming`: A flag to indicate if the call is a streaming call
- `response_callback`: The callback function to process the response from gRPC call,
takes in response object and context object, context object can be used to perform
push xcom or other after task actions
- `log_response`: A flag to indicate if we need to log the response

<a id="hooks"></a>

# hooks

<a id="hooks.grpc"></a>

# hooks.grpc

GRPC Hook

<a id="hooks.grpc.GrpcHook"></a>

## GrpcHook Objects

```python
class GrpcHook(BaseHook)
```

General interaction with gRPC servers.

**Arguments**:

- `grpc_conn_id`: The connection ID to use when fetching connection info.
- `interceptors`: a list of gRPC interceptor objects which would be applied
to the connected gRPC channel. None by default.
Each interceptor should based on or extends the four
official gRPC interceptors, eg, UnaryUnaryClientInterceptor,
UnaryStreamClientInterceptor, StreamUnaryClientInterceptor,
StreamStreamClientInterceptor.
- `custom_connection_func`: The customized connection function to return gRPC channel.
A callable that accepts the connection as its only arg.

<a id="hooks.grpc.GrpcHook.get_connection_form_widgets"></a>

#### get\_connection\_form\_widgets

```python
@staticmethod
def get_connection_form_widgets() -> Dict[str, Any]
```

Returns connection widgets to add to connection form

<a id="hooks.grpc.GrpcHook.run"></a>

#### run

```python
def run(stub_class: Callable,
        call_func: str,
        streaming: bool = False,
        data: Optional[dict] = None) -> Generator
```

Call gRPC function and yield response to caller

