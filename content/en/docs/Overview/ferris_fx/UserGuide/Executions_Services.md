---
title: "Executions - Services"
linkTitle: "Executions - Services"
weight: -13
description: >-
    How to use the Executions/Services Framework for script automation and service (execution) triggering.
---

The Executions/Services is an event oriented framework that allows enterprise organizations the automation of script
processing which can be triggered by:

- Manually: By clicking the ‘Run’ button on the FerrisFX Management Server.
- On Schedule: As a cron job whereas the Cron expression is added on the UI.
- On Event: Where a service is configured to be triggered by the FX Router when a specific type of event is observed on
  the platform.

It allows users to deploy their locally tested scripts without DevOps specific changes or the need to learn complex
DSL (description and configuration language). In tandem with Git integrated source code management FX allows distributed
and fragmented tech teams to easily deploy and test new versions of code in an agile way with changes being applied
immediately.

Continuous Change Integration / Change Deployment becomes a component based and building block driven approach, where
services can be configured and parametrised. All scripts and their parameters, such as secrets and environment
variables, form services which makes them reusable for similar jobs or event chains. Event based service triggering
allows users to run multiple services in parallel as a reaction to the same event.

Primary entities for "Executions" are Services which are composed by scripts that are executed in a predefined order.

## Navigation: Services

This Use Case defines how to create and run a new service.

1. Click on *Executions* on the left side of the dashboard menu to open drop-down
2. Click on *Services*
3. Click on *+Add* to create a Service

{{< blocks/screenshot color="white" image="/images/executions_services_add_roboto.png">}}

## Create service

| **Field name**                | **Steps & Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|:------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1. Name                       | 1. Name the service                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| 2. Description                | 2. Describe the Service                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 3. Project                    | 3. Select the project to which the service will be bound                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 4. Tags                       | 4. Add Tags of choice manually or select from predefined tags                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 5. Schedule                   | 5. Schedule cron job -> "Cron like schedule definition. NOTE: day of week start on Monday (0 - Monday, 6 - Sunday) example: "20****" -> **The whole definition of [Cron Jobs](/docs/user-guide/cronjob/ "CronJob") can be found in the next sub-category of this UserGuide**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 6. Trigger Event Type         | 6. Select Value -> select event type to trigger the exectution of the service -> please visit the sub-category [Events](/docs/user-guide/events/ "Events") to get a better understanding of how to set event triggers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| 7. Allow Manual Triggering    | 7. Checkbox -> click to allow manual triggering of the service                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 8. Active                     | 8. Checkbox -> click to set the service to active                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 9. Priority                   | 9. Select from 1-10 the priority level of the service (*High 1-3; Regular 4-7; Low: 8-10*)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 10. File Upload (choose file) | 10. Click on Choose file (Optional) to upload a script -> upload a JSON "config.json" script to configure the service                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 11. File Upload (choose file) | 11. Click on Choose file (Optional) to upload a script -> upload a python "test_scr.py" script to pull the configuratio from config file and print all items                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 12.                           | 12. Click Save to save services                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| *Supported File upload Types* | 4 different file types are supported: <br />**1. ".py file"** -> A PY file is a program file or script written in Python, an interpreted object-oriented programming language. <br />**2. ".json file"** -> A JSON file is a file that stores simple data structures and objects in JavaScript Object Notation (JSON) format, which is a standard data interchange format. <br />**3. ".sql file"** -> A (SQL) file with .sql extension is a Structured Query Language (SQL) file that contains code to work with relational databases. <br />**4. ".csv file"** -> A CSV (comma-separated values) file is a text file that has a specific format which allows data to be saved in a table structured format.<br />**5. ".jinja"** -> A Jinja file is *a fast, expressive, extensible templating engine*. Special placeholders in the template allow writing code similar to Python syntax. Jinja is **a Python template engine used to create HTML, XML or other markup formats that are returned to the user via an HTTP response**.<br /> **6. ".jinja2"** -> A Jinja2 file is a commonly-used **templating engine for web frameworks such as Flask, Bottle, Morepath and, as of its 1.8 update, optionally Django as well**. Jinja2 is also used as a template language by configuration management tool Ansible and the static site generator Pelican, among many other similar tools.<br /> |

{{< blocks/screenshot color="white" image="/images/create_service_with_configs_roboto.png">}}

##### config.json script

The `config.json` file contains key/value configuration pairs that can be accessed in scripts at execution time.

```json
{
    "somekey": "some value 2"
}
```

##### test_scr.py script

This is an example script that shows how configuration from `config.json` file can be accessed from a
script. `service_name` will be passed to the script as argument and then can be used for fetching configuration
using `ApplicationConfigurator` from `
li` python service.

```python
import sys, json
from ferris_cli.v2 import ApplicationConfigurator

fa = json.loads(sys.argv[1])

service_name = fa['service_name']
config = ApplicationConfigurator.get(service_name)

for k, v in config.items():
    print(f"{k} -> {v}")
    print(v)
```

## Check Created Service

The created service should be triggered every 20 minutes of every hour but can also be run manually.

- Click on the magnifying glass icon to open the service's details page

{{< blocks/screenshot color="white" image="/images/click_loupe_service_roboto.png">}}

1. Check details page
2. Click on "Show Trigger Event"

{{< blocks/screenshot color="white" image="/images/service_details_show_trigger_event_roboto.png">}}

1. Check the triggered event details
2. Close

{{< blocks/screenshot color="white" image="/images/triggered_event_details_roboto.png">}}

## Service Executions / Runs

- Click on the "Run" button down the page to run the service manually

{{< blocks/screenshot color="white" image="/images/run_button_manual_service.png">}}

It will automatically transfer you to the "List Service Executions" tab

1. Check runs/service executions to see if your manually triggered execution was processed
2. Click on the magnifying glass icon of your latest manually triggered run to open details page of the exectuion

{{< blocks/screenshot color="white" image="/images/manual_run_check_loupe_details_roboto.png">}}

1. Check the details "Show Service Execution" of the run/exection
2. Click on "List Steps" tab to see the steps of the execution

{{< blocks/screenshot color="white" image="/images/exection_manual_run_details_roboto.png">}}

1. Check the steps of the run and status (completed; pending; unprocessed; failed)
2. Click on "Show Results" to verify the script for failed executions

{{< blocks/screenshot color="white" image="/images/manual_run_list_steps_roboto.png">}}

{{< blocks/screenshot color="white" image="/images/script_manual_run_execution.png">}}

- Close window

## Save a Run/Execution

1. Go back to the "List Service Executions" tab
2. Click on the edit icon to open make the run/execution editable

{{< blocks/screenshot color="white" image="/images/list_service_executions_edit_manual_run_roboto.png">}}

1. Name the execution/run
2. Describe the execution/run
3. Click "Saved" check box
4. Save

{{< blocks/screenshot color="white" image="/images/save_execution_run_roboto.png">}}

1. Click on Executions to open dropdown
2. Click on Saved Executions to check the saved run

{{< blocks/screenshot color="white" image="/images/check_saved_run_roboto.png">}}

**In the section [UI Generator](/docs/developer_guide/ui_generator/ "UI Generator"), the importance of the
saved run will be showcased**.

