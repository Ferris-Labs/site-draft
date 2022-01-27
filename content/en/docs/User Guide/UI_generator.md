---
title: "UI Generator"
linkTitle: "UI Generator"
tags: [ui, executor, packages] 
categories: []
weight: -14
description: >-
  Overview and "How to" generate UIs in a simplified and automated approach.
---

The UI Generator has the ability to facilitate and automate manual processes in order to define step by step what has to be done. Based on the definition of models, views and interfaces within the code, the generator creates pages automatically considering the configuration of modules as wel.

Following the example setup from the Executor / Executions section, another script which has the ability to generate UIs will be added to the package already created previously "Test Package with Scripts". This process works as follows:

1. Navigate to Executions -> Packages to open the list of packages

2. Click on the edit icon to open the package/execution details

   ![](/images/edit_package.png)

3. Click on "+Add More Scripts" 

4. Click on "Choose file" to add the "parameters.json" file

5. Click on "Save"

![](/images/add_parametersjson_script.png)

*Note that the "parameters.json" file describes which parameters a user can input while executing the package. These parameters can be adapted to any use case.*

##### parameters.json script

The parameters.json file contains a JSON definition of fields that will be rendered and presented to the user on a manual run of the Package Execution in order to gather parameters needed for running package execution. This way, the same package can be  reused by sending different parameter values to the same package.

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
      "default": ["value 2", "value 3"],
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

*Note that the "Run" button changed by displaying the package has a typeform that needs to be filled out by the user before finalizing the execution.*

#### Create/Build the UI by clicking Run

- Click on "Run" to display the automatically genUI

![](/images/run_UI_package.png)

The parameters from the "parameters.json" test script a rendered and displayed.

1. Fill in some text "Server 1 - test" since it is a required field
2. Fill in some text
3. Click on Run to send the c parameters to the package for execution

*Note that these are test parameters with dummy text*

![](/images/run_parameters_UI.png)

- Click on the "magnifying glass" icon to check the details of the execution/run

  ![](/images/click_loupe_parameters_run.png)

The next page shows that the run has been completed.

![](/images/parameters_run_completed.png)

#### The importance of saved runs

A user, such as Dev Ops, may simply edit and save a package before running it. By doing so it avoids repetitively generating and running packages.