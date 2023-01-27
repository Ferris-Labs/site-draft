---
title: "Containers + Purpose"
linkTitle: "Containers & Purpose"
weight: 5
description: >
  Ferris SX Containers + Purpose.
---

## Creating a Docker Container

Below is an example of a dockerfile to create a Docker image for some Ferris SX application. The user is free to choose what base python image
to use and then add Ferris module and other libraries.

```
FROM python:3.9-alpine
#RUN pip install -i https://test.pypi.org/simple/ ferris-sx==0.0.8 --extra-index-url https://pypi.org/simple/ ferris-sx
RUN pip install ferris-sx
COPY app.py utils.py
```

After the user have built an image and pushed it to some Docker image regitry, he can run it in Ferris SX UI.
