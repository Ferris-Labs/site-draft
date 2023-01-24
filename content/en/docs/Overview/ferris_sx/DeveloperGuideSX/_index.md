---
title: "Developer Guide"
linkTitle: "Developer Guide"
weight: 2
description: >-
  Ferris SX Developer Guide (for Developers).
---

## Overview

**FerrisSX** is a container level solution for building highly scalable, cross-network  sync or async applications.

Using the Ferris SX platform to run and manage stream processing containers utilizing Ferris messaging infrastructure significantly reduces the cost of deploying enterprise application and offers standardized data streaming between workflow steps.  This will simplify the development and as result create a platform with agile data processing and ease of integration.

## Getting started with Stream Processors

Take a look at this library for creating Stream Processors on top of Kafka and running them inside Ferris platform:
[Ferris-SX](https://pypi.org/project/ferris-sx/) 

## Example of a Stream Processor

Below you can find an example application that is using ferris-sx python library functions to count the number of words in incoming messages and then sending the result to *twitter_feed_wc* Kafka topic.  
```python
import json
from ferris_sx.core import app
from ferris_sx.utils import sx_producer


def process(message):
    message_new = dict()
    message_new['text'] = message['text']
    message_new['word_count'] = len(message['text'].split(' '))
    message_new_json = json.dumps(message_new)
    print(message_new_json)
    sx_producer.send(topic="twitter_feed_wc", value=message_new_json.encode('utf-8'))


app.process = process

```

## Creating Docker Container

Below is an example of a dockerfile to create a Docker image for the Twitter Word Count application shown in the previous section. The user is free to use whatever base python image
and then add Ferris module and other libraries.

```
FROM python:3.9-alpine
#RUN pip install -i https://test.pypi.org/simple/ ferris-sx==0.0.8 --extra-index-url https://pypi.org/simple/ ferris-sx
RUN pip install ferris-sx
COPY twitter_word_count.py app.py
```

After the user have built an image and pushed it to some Docker image regitry, he can run it in Ferris SX UI.
