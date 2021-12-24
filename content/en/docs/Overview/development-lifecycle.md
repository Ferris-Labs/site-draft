---
title: "Development Lifecycle of an FX Service"
linkTitle: "Development Lifecycle"
weight: 100
description: >-
     Development Lifecycle of an FX Service.
---

The following is an overview of the development steps involved in building a Ferris Service.

## Creating A Service

A service is a collection of scripts, modules and assets such as additional configuration files.

### Creating Scripts

The following is the most basic Service. Create a file with the following script and let us name it **app.py**

```python
import sys
import json

payload = json.loads(sys.arg[1])
print(payload)
```

The above service script will load and print the JSON payload.

### Load the Script to the Platform

Log in to the UI and skip to the packages sub-menu and create a New service. Let us call the service "hello_world".

In the add file section upload the file you have just created.

### Run the Service, view Results & Errors

The service is now ready to be run. Once you save it you will see the Run Button. On clicking it you will be taken to the list of runs of the specific service. 

By clicking on steps you can check the individual steps. 

On Clicking result you will see the output of the script.

If the script has errors you will see the errors displayed in the same pop-up.

### Trigger an Event and Another Service from your Service

First let us create another service "**hello_world_2**" with a copy of the **app.py** of the previous service.

So the code for "**hello_world_2**" is as below.

```python
import sys
import json

payload = json.loads(sys.arg[1])
print(payload)
```

Create the new service and upload the script to the service.

Now we edit our earlier service **hello_world/app.py** to send out a custom event type.

```python
import sys
import json
from ferris_cli import ApplicationConfigurator
from ferris_cli import EventSender

payload = json.loads(sys.arg[1])
print(payload)
my_config = ApplicationConfigurator().get("ferris.services.hello_world.config")['my_config']
print(my_config)

event_type = "my_custom_event_type"
data = {"some_parameter":"Hello from Hello World"}

EventSender().send(event_type,data)
```

Update the '**hello_world**' service and trigger a run.

Now browse to 'Runs' menu of the UI and on refreshing the page you will see that the second service is either pending or being processed. The print out of the app.py script should now show you the additional parameters sent.

### Run your Service on a Scheduled CRON

Open the edit Package UI of the service '**hello_world**'.

Add the following CRON expression in the schedule. 

Save the package.

Switch to the Execute.

You should now see the hello_world package executes every 5 minutes (and also triggers the hello_world_2 Service in turn).

Now that you have seen how it works it is probably best to delete the CRON expression and save the service.

For a more detailed understanding of the CRON expression please check this page "CronJob" in the User Guide.

In the above sections you have seen how basic services can be created and triggered in 3 ways.

### Run Multiple Scripts in a Service

Create a copy of app.py and call it step_2.py. The code should look as below.

```python
import sys
import json

payload = json.loads(sys.arg[1])
print(payload)
print("I am step 2")
```

Upload the new script to the Service. Once you upload the script you will have 2 scripts and you can change the order in which they are run by clicking and dragging. When you run the service you will also note that boh scripts have access to the properties of the incoming event.

### Add and Retrieve Service Specific Configurations

Service specific configurations are often a requirement. In order to set up specific configurations for your service please create a file named **config.json** and upload it to the service.

```json
{
"my_config": "this is easy"
}
```

The configs that you uploaded will be placed by the platform within Consul. Since the application is called hello_world the key of the config in Consul will be "ferris.services.hello_world.config". If you have called your service something else you can always retrieve the path from the UI as shown below.

You can now adjust your code to retrieve and print the configs at run time.

```python
import sys
import json
from ferris_cli import ApplicationConfigurator

payload = json.loads(sys.arg[1])
print(payload)
my_config = ApplicationConfigurator().get("ferris.services.hello_world.config")['my_config']
print(my_config)
```

Update the service by uploading the new version of the code, trigger it and check the results.

For a full discussion on configuration best practices please review this page - Configurations in FerrisFX.

### Retrieve Platform Specific Configurations

Platform specifc configurations are stored in Consul in the ferris.env key. These are primarily used for platform wide configurations and environment ( DEV, UAT, PRD) specific URLs etc. You can retrieve them like so.

```python
import sys
import json
from ferris_cli import ApplicationConfigurator

platform_config = ApplicationConfigurator().get("ferris.env")
print(platform_config)
```

### Modularising Your Service

Within each package you can create classes in order to keep your code clean. Let us create a simple class and use it.

**my_class.py** 

```python
import json

class MyClass{
  def print_payload(payload):
    print(payload)
}
```

Update the app.py

```python
import sys
import json
from my_class import MyClass

payload = json.loads(sys.arg[1])
MyClass().print_payload(payload)
```

Edit the hello_world package and delete the 2 files present before re-uploading the app.py and my_class.py files. Once uploaded and saved you can run the service and check results.

### Provide a UI to Service for Manual Runs by End Users

UI metadata json guide.

### Load Asset Files and Templates

Show how to load asset files and get path on OS.

### Extend the Executor with New Libraries

Show how images are built.

