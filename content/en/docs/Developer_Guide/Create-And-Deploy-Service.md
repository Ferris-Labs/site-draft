---
title: "Create a Service"
linkTitle: "Create a Service"
weight: 203
description: >-
     Create a Service.
---
In this section we will create a simple service, add a manifest file to the service and deploy the service.

The following is an overview of the development steps involved in building a Ferris Service.

## Pull GIT Repository
As a first step clone/pull from the GIT Repository that was set up for the project in the previous steps. 

## Create a Service Directory
Create a directory with the name of the service (Snake Case Naming is preferred).

### Creating Scripts

The following is the most basic Service. Create a file with the following script and let us name it **app.py**

```python
print('Hello DX')
```

The above service script will print 'Hello DX' to the console. The output can be viewed within the DX Manager UI as tthe result of a run. 

As you will have noted the script does not include any specific references to the DX Platform.

Nonetheless by virtue of being run within the DX execution environment the script execution can be 

* run on a cron schedule
* run manually from the UI
* run through triggering by linking to an Event.

###  Add a Manifest File
Proceed to add a `manifest.json` file to your service to help describe and configure your service for deployment.