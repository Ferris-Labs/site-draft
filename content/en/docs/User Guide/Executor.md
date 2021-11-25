---
title: "Executor"
linkTitle: "Executor / Executions"
weight: -10
description: >-  
  Overview and "How to" use the Executor Framework for script automation and package (execution) triggering
---

The Executor is a custom framework allowing the organization and automatization of script processing which can be triggered:

- at a scheduled time (intervals)
- as a reaction to an event

It allows users to use their locally tested scripts without changes or need to learn complex DL (description language). Together with a Git integration it gives the possibility to easily deploy and test new versions of code in an agile way with changes being applied immediately. Packages can be configurable and parametrised which makes them reusable for similar jobs. Events package triggering allows users to run multiple packages in parallel as a reaction to the same event.

### Executor (Executions) 

Primar entities on "Executions" are packages which are composed by scripts that are executed in a defined order.

#### Executions -> Packages

In this given Use Case it is defined how to create and run a package.

1. Click on Executions on the left side of the dashboard menu to open drop-down
2. Click on Packages
3. Click on +Add to create a package

![](/images/executions_packages_add.png)



#### Create Package

1. Name package
2. Describe package
3. Select the Project to which the package will be bound
4. Add Tags manually or select from predefined tags
5. Schedule cron job -> "Cron like schedule definition. NOTE: day of week start on Monday (0 - Monday, 6 - Sunday)" example: "20****" **-> The whole definition of "Cron Jobs" can be found in a separate sub-category of this UserGuide **
6. Trigger Event Types - Select Value -> select event type to trigger the exectution of the package
7. Check the checkbox to Allow Manual Triggering -> click to allow manual triggering of the package
8. Check the checkbox to Activate your package -> click to set the package to active
9. Click on Choose file (optional) to Upload a Script -> upload a JSON "config.json" script to configure the package
10. Click on +Add More Scripts... to add more scripts -> upload a python "test_scr.py" script to pull the configuratio from config file and print all items
11. Click on Save to save package

![](/images/create_package_with_configs.png)



#### Check Created Package

The created package should be triggered every 20 minutes of every hour but can also be run manually.

- Click on the loupe icon to open the package's details page

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

It will automatically transfer you to the "List Package Executions" tab

1. Check runs/package executions to see if you manually triggered execution was processed
2. Click on the loupe icon of your latest manually triggered run to open details page of the exectuion

![](/images/run_check_loupe_details.png)

1. Check the details "Show Package Execution" of the run/exection
2. Click on "List Steps" tab to see the steps of the execution

![](/images/exection_run_details.png)

1. Check the steps of the run and status (completed; pending; unprocessed; failed)
2. Click on "Show Results" to verify the script for failed executions

![](/images/run_list_steps.png)

![](/images/script_run_execution.png)

- Close window

**Note that currently only python and sql handlers are available, files of different type will be unprocessed.**

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

**In the next section "UI Generator", the importance of the saved run will be showcased**.