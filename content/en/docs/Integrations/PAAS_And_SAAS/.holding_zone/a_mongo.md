---
title: "mongo"
linkTitle: "mongo"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     mongo Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.mongo"></a>

# sensors.mongo

<a id="sensors.mongo.MongoSensor"></a>

## MongoSensor Objects

```python
class MongoSensor(BaseSensorOperator)
```

Checks for the existence of a document which

matches the given query in MongoDB. Example:

>>> mongo_sensor = MongoSensor(collection="coll",
...                            query={"key": "value"},
...                            mongo_conn_id="mongo_default",
...                            mongo_db="admin",
...                            task_id="mongo_sensor")

**Arguments**:

- `collection`: Target MongoDB collection.
- `query`: The query to find the target document.
- `mongo_conn_id`: The :ref:`Mongo connection id <howto/connection:mongo>` to use
when connecting to MongoDB.
- `mongo_db`: Target MongoDB name.

<a id="hooks"></a>

# hooks

<a id="hooks.mongo"></a>

# hooks.mongo

Hook for Mongo DB

<a id="hooks.mongo.MongoHook"></a>

## MongoHook Objects

```python
class MongoHook(BaseHook)
```

Interact with Mongo. This hook uses the Mongo conn_id.

PyMongo Wrapper to Interact With Mongo Database
Mongo Connection Documentation
https://docs.mongodb.com/manual/reference/connection-string/index.html
You can specify connection string options in extra field of your connection
https://docs.mongodb.com/manual/reference/connection-string/index.html#connection-string-options

If you want use DNS seedlist, set `srv` to True.

ex.
    {"srv": true, "replicaSet": "test", "ssl": true, "connectTimeoutMS": 30000}

**Arguments**:

- `mongo_conn_id`: The :ref:`Mongo connection id <howto/connection:mongo>` to use
when connecting to MongoDB.

<a id="hooks.mongo.MongoHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> MongoClient
```

Fetches PyMongo Client

<a id="hooks.mongo.MongoHook.close_conn"></a>

#### close\_conn

```python
def close_conn() -> None
```

Closes connection

<a id="hooks.mongo.MongoHook.get_collection"></a>

#### get\_collection

```python
def get_collection(
        mongo_collection: str,
        mongo_db: Optional[str] = None) -> pymongo.collection.Collection
```

Fetches a mongo collection object for querying.

Uses connection schema as DB unless specified.

<a id="hooks.mongo.MongoHook.aggregate"></a>

#### aggregate

```python
def aggregate(mongo_collection: str,
              aggregate_query: list,
              mongo_db: Optional[str] = None,
              **kwargs) -> pymongo.command_cursor.CommandCursor
```

Runs an aggregation pipeline and returns the results
https://pymongo.readthedocs.io/en/stable/api/pymongo/collection.html#pymongo.collection.Collection.aggregate
https://pymongo.readthedocs.io/en/stable/examples/aggregation.html

<a id="hooks.mongo.MongoHook.find"></a>

#### find

