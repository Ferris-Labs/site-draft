---
title: "Ferris User Guide"
linkTitle: "User Guide"
weight: 1
description: >
  User Guide:
---



### Getting Started

* Login to [home.ferris.ai](http://home.ferris.ai/)
* Login Credentials: 
  - Username (email)
  - Password

In this given Use Case the identity and access management process is secured through KeyCloak.



### Dashboard / Landing Page

The dashboard can show various statistics and analytics such as:

- User activities
- Page views
- Income (daily, weekly, total)
- Active projects

![](/images/ferris_home.png)



#### Add Users and define User Roles

In this given Use Case, 3 different user roles are defined: 

1. Admin
2. Public
3. Executor

**Note that the User Roles on platform level still need to be defined.**

1. Click on Security to open dropdown
2. Click on List Users to open the user details page
3. Click on "+" to add a new user

![](/images/security_list_users.png)

The following steps define how to create a new user:

1. First Name
2. Last Name
3. User Name (valid for authentication on DB or LDAP, unused OID auth)
4. Click checkbox to activate the user (can be deactivated if removed from project/company)
5. Email
6. Select the User Role
7. Save

![](/images/add_user_platform.png)

- Click on Security -> List Users to check the created user

![](/images/list_users.png)

**Note that the User Roles on platform level still need to be defined.**



# Executor

The Executor is a custom framework allowing the organization and automatization of script processing which can be triggered:

- at a scheduled time (intervals)
- as a reaction to an event

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
5. Schedule cron job -> "Cron like schedule definition. NOTE: day of week start on Monday (0 - Monday, 6 - Sunday)" example: "20****" -> meaning every 20 minutes of every hour, every day, every month and year.
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

**In the next section "Typeform like UI Generator", the importance of the saved run will be showcased**.



#### Typeform like UI Generator

Another script which will be able to generate typeform like UIs will be added to the package created above "Test Package with Scripts".

1. Click on Executions -> Packages to open the list of packages

2. Click on the edit icon to open the package/execution details

   ![](/images/edit_package.png)

3. Click on "+Add More Scripts" 
4. Click on "Choose file" to add the "parameters.json" file
5. Click on "Save"

![](/images/add_parametersjson_script.png)

**Note that the "parameters.json" file describes which parameters a user can input while executing the package. These parameters can be adapted to any use case.**

The "Run" button changed by displaying the package has a typeform that needs to be filled out by the user before finalizing the execution.

- Click on "Run" to display the created/built typeform

![](/images/run_typeform_package.png)

The parameters from the "parameters.json" test script will be rendered and displayed.

1. Fill in some text "Server 1 - test" since it is a required field
2. Fill in some text
3. Click on Run to send the filled parameters to the package for execution

**Note that these are test parameters with dummy text**

![](/images/run_parameters_typeform.png)

- Click on the "loupe" icon to check the details of the execution/run

  ![](/images/click_loupe_parameters_run.png)

On the next screenshot it is clearly displayed that the run has been completed.

![](/images/parameters_run_completed.png)

**The importance of saved runs:**

If the user is a DevOp for example and wants to trigger a script which will verify the server down or up time, instead of creating 10 packages and changing the details in the typeform (parameters) every time he executed the package, the user will be able to simply edit and save the package before running it. By doing so it avoids loosing tremendous time by creating new packages and filling or changing data in the generated typeform. 



### Workflow

A workflow is an administrative process that consists in verifying, in this case the incomming data, before enabling a predefined mechanism and setting it from undone to done, inactive to active or pending to approved. 

In this given use case, a workflow will be created that works as follows:

1. A file gets uploaded to the File Storage (MinIO)
2. Once the file verified and approved by "admin"
3. The package/execution gets triggered

#### Getting Started

1. On the left side menu, click on Workflows to open dropdown
2. Click on List Workflows
3. Click on "+Add" to create a workflow

![](/images/list_workflows.png)

**Note that before starting to input the values for the workflow, the JSON file needs to be edited:**

**1. "package_id" in the JSON file which is the "Uuid (unique user ID)" in the predefined package/execution**

**2. package_name" in the JSON file which is also called "Package Name" in the predefined package/execution**

![](/images/uuid_packagename_edit_json.png)

Change those values with the values from the package and safe JSON file.

1. Name the workflow
2. Add a description
3. Add Tags 
4. Copy and paste the script from the JSON file
5. Copy from the script the "source" and paste it to the "Entrypoint source"
6. Copy from the script the "event_type" and paste it to the "Entrypoint event"
7. Click the checkbox to set the workflow as active
8. Click "Save"

![](/images/create_workflow.png)

**Upload a file to the bucket to test the approval process**

1. Click on File Storage in the left side menu to open dropdown
2. Click on List Files
3. Click on "+Add"

![](/images/upload_file_test_workflow.png)

1. Choose File to insert
2. Select File/Data Type in dropdown (CSV Table; Plain Text; JSON)
3. Select Bucket Name (scripts; test; testbucket)
4. Save 

![](/images/select_file_test_workflow.png)



### Taxonomies / Tagging

The following User Guide will explain and describe how to understand and use the Taxonomy/Tagging module.

**Tagging/Taxonomy** makes it easier to group and find similar functions, rules and data elements.



### Getting Started

* Login to [home.ferris.ai](http://home.ferris.ai/)
* Login Credentials: 
  - Username (email)
  - Password



### Taxonomy / Tagging 

It was developed as a module and can easily be added to any model by the developers/users.

Two different ways of adding tags are available and will be showcased below.

#### Taxonomies / Tags

1. Click on Taxonomies in the left menu and then on Tags
2. Click Add to create a tag

![](/images/Taxonomies Tags Add.png)

1. Name Tag
2. Save

![](/images/Create Tag.png)

- Check created Tag(s)

1. Details 
2. Click on any tag to open details page  
3. Click on List Packages to see in which packages the same tags are used
4. Click on List Workflows to see in which workflows the same tags are used
5. Click on the Edit icon to edit a tag

![](/images/List packages 1 click tag.png)

![](/images/Details package.png)

![](/images/list packages 2.png)

![](/images/list workflows 3.png)

![](/images/Check Tag Details Edit.png)



#### Search Tag

1. Search Tag
2. Click Add Filter to choose a filter

![](/images/Search Tag.png)

1. Choose from the dropdown list
2. Insert Name
3. Hit the Search button

![](/images/Search with Filter.png)

1. Check search results

![](/images/search results.png)

