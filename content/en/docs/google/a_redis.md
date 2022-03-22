---
title: "redis"
linkTitle: "redis"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     redis Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.redis_pub_sub"></a>

# sensors.redis\_pub\_sub

<a id="sensors.redis_pub_sub.RedisPubSubSensor"></a>

## RedisPubSubSensor Objects

```python
class RedisPubSubSensor(BaseSensorOperator)
```

Redis sensor for reading a message from pub sub channels

**Arguments**:

- `channels`: The channels to be subscribed to (templated)
- `redis_conn_id`: the redis connection id

<a id="sensors.redis_pub_sub.RedisPubSubSensor.poke"></a>

#### poke

```python
def poke(context: 'Context') -> bool
```

Check for message on subscribed channels and write to xcom the message with key ``message``

An example of message ``{'type': 'message', 'pattern': None, 'channel': b'test', 'data': b'hello'}``

**Arguments**:

- `context`: the context object

**Returns**:

``True`` if message (with type 'message') is available or ``False`` if not

<a id="sensors.redis_key"></a>

# sensors.redis\_key

<a id="sensors.redis_key.RedisKeySensor"></a>

## RedisKeySensor Objects

```python
class RedisKeySensor(BaseSensorOperator)
```

Checks for the existence of a key in a Redis

<a id="operators"></a>

# operators

<a id="operators.redis_publish"></a>

# operators.redis\_publish

<a id="operators.redis_publish.RedisPublishOperator"></a>

## RedisPublishOperator Objects

```python
class RedisPublishOperator(BaseOperator)
```

Publish a message to Redis.

**Arguments**:

- `channel`: redis channel to which the message is published (templated)
- `message`: the message to publish (templated)
- `redis_conn_id`: redis connection to use

<a id="operators.redis_publish.RedisPublishOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Publish the message to Redis channel

**Arguments**:

- `context`: the context object

<a id="hooks"></a>

# hooks

<a id="hooks.redis"></a>

# hooks.redis

RedisHook module

<a id="hooks.redis.RedisHook"></a>

## RedisHook Objects

```python
class RedisHook(BaseHook)
```

Wrapper for connection to interact with Redis in-memory data structure store

You can set your db in the extra field of your connection as ``{"db": 3}``.
Also you can set ssl parameters as:
``{"ssl": true, "ssl_cert_reqs": "require", "ssl_cert_file": "/path/to/cert.pem", etc}``.

<a id="hooks.redis.RedisHook.__init__"></a>

#### \_\_init\_\_

```python
def __init__(redis_conn_id: str = default_conn_name) -> None
```

Prepares hook to connect to a Redis database.

**Arguments**:

- `conn_id`: the name of the connection that has the parameters
we need to connect to Redis.

<a id="hooks.redis.RedisHook.get_conn"></a>

#### get\_conn

```python
def get_conn()
```

Returns a Redis connection.

