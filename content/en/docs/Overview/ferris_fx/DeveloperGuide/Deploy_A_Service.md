---
title: "Deploy a Service"
linkTitle: "Deploy a Service"
weight: 204
description: >-
    Deploy a Service.
---

### Push to the GIT Repository

Push the code to the Project linked GIT Repository

### Sync and Run the Service

Proceed to the Ferris UI. Select the project that you created and click on the `Git Repositories Tab`. Click on
the `Sync Now` button. Your code is now deployed to the platform.

### Run the Service, View Results & Errors

* Once the service has been synced with the repository you can trigger the execution from the UI by clicking the `run`
  button.

* On clicking it you will be taken to the list of runs of the specific service.

* By clicking on steps you can check the individual steps.

* On clicking result you will see the output of the script.

* If the script has errors you will see the errors displayed in the same pop-up.
* If any of the scripts in a sequence has errors then the execution will be shown as having failed.

## Set Up Trigger Conditions

The script can be triggered by

* Clicking the `Run` button displayed for each service on the Ferris UI.
* Adding a cron expression in the UI. For how to set up a cron please view the
  section `Run your Service on a Scheduled CRON`
* Linking it to an event emitted by another service within the platform.

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

event_type = "my_custom_event_type"
data = {"some_parameter": "Hello from Hello World"}

EventSender().send(event_type, data)
```

Update the '**hello_world**' service and trigger a run.

Now browse to 'Runs' menu of the UI and on refreshing the page you will see that the second service is either pending or
being processed. The print out of the app.py script should now show you the additional parameters sent.

### Run your Service on a Scheduled CRON

Open the edit Package UI of the service '**hello_world**'.

Add the following CRON expression in the schedule.

Save the package.

Switch to the Execute.

You should now see the hello_world package executes every 5 minutes (and also triggers the hello_world_2 Service in
turn).

Now that you have seen how it works it is probably best to delete the CRON expression and save the service.

For a more detailed understanding of the CRON expression please check this
page [CronJob](/docs/overview/ferris_fx/userguide/"CronJob") in the *User Guide*.

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

Upload the new script to the Service. Once you upload the script you will have 2 scripts and you can change the order in
which they are run by clicking and dragging. When you run the service you will also note that both scripts have access
to
the properties of the incoming event.

### Add Service Specific Configurations and Secrets

Service specific configurations are often a requirement. In order to set up specific configurations for your service
please create a file named **config.json** and upload it to the service.

```json
{
    "my_config": "this is easy"
}
```

The configs that you uploaded will be placed by the platform within Consul.

Secrets are variables that you require in executor packages which you do not wish to be exposed on UI or in Consul, but
use in your scripts.

In order to create Service specific secrets upload a secrets.json file to your package.

The following is a sample secrets json.

```json
{
    "DB_NAME": "my_database_username",
    "DB_PASS": "my_database_password"
}
```

## Retrieve Service Specific Configurations, Secrets and Parameters

Ferris makes all configurations, secrets and parameters available to each script being run in the service through
the `context` object.

The following sample demonstrates the retrieval of the attribuets from the context object.

```python
from ferris_ef import context

print("------- Get Service Config -------")
print(context.config)

print("------- Get Execution Params -------")
print(context.params)

print("------- Get Service Info -------")
print(context.package.name)
print(context.package.id)

print("------- Get Service State -------")
print(context.state.get())

print("------- Update Service State -------")
context.state.put("some_key", "some_value")
context.state.put("other_key", {"attr_1": "val_1"})

print("------- Get Secret -------")
print(context.secrets.get("test_secret_1"))

print("------- Set Secret -------")
print(context.secrets.set("test_secret_4", {"somekey": "plsomeval"}, "platform"))
print(context.secrets.set("test_secret_4", {"somekey": "plsomeval"}, "project"))
```

Update the service by uploading the new version of the code, trigger it and check the results.

**Please note that Secrets are not displayed in the configuration manager to avoid inadvertent manual editing or secrets
leakage.**

For a full discussion on configuration best practices please review the page [Parameters and Configurations](/docs/overview/ferris_fx/developerguide/"CronJob")

## Retrieve Platform Specific Configurations

Platform specifc configurations are stored in Consul in the ferris.env key. These are primarily used for platform wide
configurations and environment ( DEV, UAT, PRD) specific URLs etc. You can retrieve them like so.

```python
import sys
import json
from ferris_cli import ApplicationConfigurator

platform_config = ApplicationConfigurator().get("ferris.env")
print(platform_config)
```

## Add and Retrieve Service Specific Secrets

Secrets are variables that you require in executor packages which you do not wish to be exposed on UI or in Consul, but
use in your scripts. Secrets are package specific.

In order to use secrets there are 2 steps:

1. Upload a secrets.json file to your package.
2. Use the provided library to access the Secrets

The following is a sample `secrets.json`.

```json
{
    "DB_NAME": "my_database_username",
    "DB_PASS": "my_database_password"
}
```

The following is a sample retreival of secrets.

```python
from ferris_ef import get_secret

print(f"DB NAME: {get_secret('DB_NAME')}")
print(f"DB PASS: {get_secret('DB_PASS')}")
```

**Please note that secrets are not exposed in the UI nor stored in plain text in the system. So once set they can only
be updated or queried through the executor.**

## Modularising Your Service

Within each package you can create classes in order to keep your code clean. Let us create a simple class and use it.

`my_class.py

```python
class MyClass:

    def print_payload(payload):
    print(payload)
```

Update the `app.py`

```python
import sys
import json
from my_class import MyClass

payload = json.loads(sys.arg[1])
MyClass().print_payload(payload)
```

Edit the hello_world package and delete the 2 files present before re-uploading the app.py and my_class.py files. Once
uploaded and saved you can run the service and check results.

## Retrieve Trigger Event Payload

The data section of trigger events are provided to all scripts executed within a package. This is how to retreive them.

```python
import json
import sys
from ferris_ef import get_param

fa = json.loads(sys.argv[1])
for k, v in fa.items():
    print(k, v)

# Alternatively you can use the provided helper function.
my_parameter = get_param('MY_PARAMETER')

```

## Load Asset Files and Templates

You can load additional helper files such as file with .json, .txt, .jinja extensions for use by your scripts. The
following is a sample on how to load the files in your application code.

```python
import os

script_dir = os.path.dirname(__file__)
rel_path = "es_last_30_days_curated_by_schema.txt"
abs_file_path = os.path.join(script_dir, rel_path)

with open(abs_file_path, 'r') as f:
    for line in f:
        print(line)
```

## Provide a UI to Service for Manual Runs by End Users

Sometimes you may be required to allow end users to trigger ad hoc runs with run specific parameters. In order to
support this usage scenario you can use the auto-generated UI feature. In order to define the UI you must provide a file
metadata.json. The UI is generated based on the metadata.json and the parameter values are passed to the execution when
run.

- Once you have created a metadata.json file you can upload it along with the other scripts.
- The run icon for the executor will change to a form icon. On clicking run the user will be displayed the form for
  entry of the parameter values.

The following is a self-explantory template showing the different types of form fields that can be generated and the
constraints thereof.

```json
{
    "fields": [
        {
            "type": "text",
            "label": "Some Text",
            "name": "some_text",
            "required": true,
            "description": "This field is required"
        },
        {
            "type": "textarea",
            "label": "Some Textarea",
            "name": "some_textarea"
        },
        {
            "type": "file",
            "label": "Some File",
            "name": "some_file",
            "data": {
                "bucket": "testbucket",
                "async": true
            }
        },
        {
            "type": "int",
            "label": "Some Number",
            "name": "some_number",
            "default": 1,
            "min": 0,
            "max": 10
        },
        {
            "type": "float",
            "label": "Some Float",
            "name": "some_float",
            "placeholder": "0.01",
            "step": 0.01,
            "min": 0,
            "max": 10
        },
        {
            "type": "select",
            "label": "Some Select",
            "name": "some_select",
            "default": "value 2",
            "choices": [
                {
                    "title": "Choice 1",
                    "value": "value 1"
                },
                {
                    "title": "Choice 2",
                    "value": "value 2"
                },
                {
                    "title": "Choice 3",
                    "value": "value 3"
                }
            ]
        },
        {
            "type": "multiselect",
            "label": "Some MultiSelect",
            "name": "some_multiselect",
            "default": [
                "value 2",
                "value 3"
            ],
            "choices": [
                {
                    "title": "Choice 1",
                    "value": "value 1"
                },
                {
                    "title": "Choice 2",
                    "value": "value 2"
                },
                {
                    "title": "Choice 3",
                    "value": "value 3"
                }
            ]
        },
        {
            "type": "radio",
            "label": "Some Radio",
            "name": "some_radio",
            "choices": [
                {
                    "title": "Choice 1",
                    "value": "value 1"
                },
                {
                    "title": "Choice 2",
                    "value": "value 2"
                },
                {
                    "title": "Choice 3",
                    "value": "value 3"
                }
            ]
        }
    ]
}
```

## Create an HPSM Message

HPSM messages can be created by sending an appropriately formatted JSON to the ferris.hpsm Kafka topic.

The following is sample method to create an HPSM message.

```python
from kafka import KafkaProducer


def create_hpsm_message(owner_group, assignment_group, title, description):
    log_time = datetime.now().strftime("%Y-%m-%dT%H:%M:%SZ")
    hpsm_message = {"log_time": log_time,
                    "jbIncident": {
                        "IncidentType": "DEFAULT",
                        "AffectedService": "SERVICE_NAME",
                        "Category": "incident",
                        "Subcategory": "failure",
                        "Area": "error message",
                        "ImpactedUserScope": "single",
                        "ImpactedUserType": "employee",
                        "OwnerGroup": owner_group,
                        "AssignmentGroup": assignment_group,
                        "Title": title,
                        "Description": [description]
                    }
                    }
    return hpsm_message


def send_hpsm(hpsm_message):
    platform_environment = self.get_platform_env()
    producer = KafkaProducer(
        bootstrap_servers=f"{platform_environment['KAFKA_BOOTSTRAP_SERVER']}:{platform_environment['KAFKA_PORT']}",
        value_serializer=lambda v: json.dumps(v).encode('utf-8'))
    producer.send('ferris.hpsm', hpsm_message)


owner_group = 'owner_group',
assignment_group = 'assignment_group'
title = 'title'
description = 'description'

hpsm_message = create_hpsm_message(owner_group, assignment_group, title, description)
send_hpsm(hpsm_message)

```
