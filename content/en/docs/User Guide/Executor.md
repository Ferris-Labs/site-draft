---
title: "Executor"
linkTitle: "Executor / Executions"
tags: [executor, pacakges] 
categories: [""]
weight: -16
description: >-  
  Overview and "How to" use the Executor Framework for script automation and package (execution) triggering.
---

The Executor is a framework allowing the organization and automation of script processing which can be triggered:

- at a scheduled time (intervals)
- as a reaction to an event
- manual triggering

It allows users to use their locally tested scripts without changes or need to learn complex DSL (description language). Together with a Git integration it gives the possibility to easily deploy and test new versions of code in an agile way with changes being applied immediately. Packages can be configurable and parametrised which makes them reusable for similar jobs. Events package triggering allows users to run multiple packages in parallel as a reaction to the same event.

### Executor (Executions) 

Primary entities on "Executions" are packages which are composed by scripts that are executed in a defined order.

#### Executions -> Packages

In this given Example you learn how to create and run a package.

1. Click on Executions on the left hand navigation to expand the menu
2. Click on Packages
3. Click on +Add to create a package

![](/images/executions_packages_add.png)



#### Create Package

1. Name package

2. Describe package

3. Select the [#Project]({{< ref "project_creation_and_users_within_project.md" >}}) to which the package will be bound

4. Add [#Tags]({{< ref "taxonomy_tagging.md" >}}) manually or select from predefined tags

5. Schedule [#Cron Job]({{< ref "CronJob" >}}) to define regularly scheduled jobs

   *NOTE: day of week start on Monday (0 - Monday, 6 - Sunday)"*

6. Trigger Event Types: Select from previously defined event types to trigger the exectution of the package

7. Check to allow Manual Triggering of this package

8. Check to activate the Package

9. Upload Execution Script of any supported language

   *Example: JSON "config.json" script to configure the package*

10. Upload any number of additional Executions Scripts

    *Example: Python "test_scr.py" script to pull the configuratio from config file and print all items*

11. Save package

![](/images/create_package_with_configs.png)

##### config.json script

The config.json file contains key/value configuration pairs that can be accessed in scripts at execution time.

```json
{"somekey":"some value 2"}
```

##### test_scr.py script

This is an example script that shows how the configuration from `config.json` file can be accessed from a script. `package_name` will be passed to the script as argument and then can be used for fetching configuration using `ApplicationConfigurator` from `ferris_cli` python package.

```python
import sys, json
from ferris_cli.v2 import ApplicationConfigurator

fa = json.loads(sys.argv[1])

package_name = fa['package_name']
config = ApplicationConfigurator.get(package_name)

for k, v in config.items():
    print(f"{k} -> {v}")
    print(v)
```

#### Check Created Package

The created package should be triggered every 20 minutes of every hour but can also be run manually.

- Click on the magnifying glass icon to open the package's details page

![](/images/click_loupe_packages.png)

1. Check details page
2. Click on "Show Trigger Event"

![](/images/package_details_show_trigger_event.png)

1. Check the triggered event details
2. Close

![](/images/triggered_event_details.png)



#### Package Executions / Runs

- Click on the "Run" button down the page to run the package manually

![](/images/run_button_manual_package.png)

This will open the "List Package Executions" tab

1. Check runs/package executions to see if the manually triggered execution was processed
2. Click on the magnifying glass icon of the latest manually triggered run to open the details page of the execution

![](/images/run_check_loupe_details.png)

1. Check the details "Show Package Execution" of the run/exection
2. Click on "List Steps" tab to see the steps of the execution

![](/images/exection_run_details.png)

1. Check the steps of the run and their respective status (completed, pending, unprocessed, failed)
2. Click on "Show Results" to verify the script for failed executions

![](/images/run_list_steps.png)

![](/images/script_run_execution.png)

- Close window

#### Save a Run/Execution

1. Go back to the "List Package Executions" tab 
2. Click on the edit icon to open make the run/execution editable

![](/images/list_package_executions_edit_run.png)

1. Name the execution/run
2. Describe the execution/run
3. Click "Saved" check box
4. Save

![](/images/save_execution_run.png)

1. Click on Executions to open dropdown
2. Click on Saved Executions to check the saved run

![](/images/check_saved_run.png)



#### Note

- *Currently only python and sql handlers are available, files of different type will be unprocessed.*

- *In the next section "UI Generator", the importance of the saved run will be showcased.*