---
title: "UI Generator"
linkTitle: "UI Generator"
description: >-
  How to generate UIs in a simplified and automated approach.
---

The UI Generator has the ability to facilitate and automate manual parameter based processes to define step by step flows or pipelines. Based on definition of models, views and interfaces within the code, the generator will create UIs automatically considering the configuration of modules as well.

Another script which has the ability to generate  UIs will be added to the service already created previously "Test Service". This process will work as follows:

## Edit existing service

1. Click on *Executions -> Services* to open the list of services
2. Click on the edit icon to open the service/execution details

{{< blocks/screenshot color="white" image="/images/edit_service_roboto.png">}}

3. Click on "*+Add More Scripts"* 

4. Click on *"Choose file"* to add the *"parameters.json"* file

5. Click on *"Save"*

{{< blocks/screenshot color="white" image="/images/add_parameters_json_script_roboto.png">}}

**Note that the "parameters.json" file describes which parameters a user can input while executing the service. These parameters can be adapted to any use case and script and can for example replace command line parameters if the script in question supports such parameters.**

##### parameters.json script

The *parameters.json* file contains a JSON definition of fields that will be rendered and presented to user upon manually triggering a service execution in order to gather the parameter values for running the service. This way, same service can be easily adapted and reused by different scenarios or environments simply by sending different parameter values to the same service.

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

**The "Run" button changed by displaying the service has a typeform that needs to be filled out by the user before starting the actual execution.**

## Create/Build the UI by clicking Run

- Click on *"Run"* to display the created/built UI

{{< blocks/screenshot color="white" image="/images/run_UI_service_roboto.png">}}

The parameters from the "parameters.json" test script will be rendered and displayed.

1. Fill in some text "Server1-test" since it is a required field
2. Fill in some text
3. Add some file
4. Click on Run to send the filled parameters to the service for execution

**Note that these are test parameters with dummy text**

{{< blocks/screenshot color="white" image="/images/run_parameters_UI_roboto.png">}}

- Click on the "magnifying glass" icon to check the details of the execution/run


{{< blocks/screenshot color="white" image="/images/click_loupe_parameters_run.png">}}

On the next screenshot it is clearly displayed that the run has been completed.

{{< blocks/screenshot color="white" image="/images/parameters_run_completed.png">}}

**The importance of saved runs:**

Note: If the user is a DevOp that wants to trigger a script which will verify the server down- or up-time, instead of creating 10 services and changing the details in the typeform (parameters) every time the service gets executed, the user will be able to simply edit and save the service before running it. This saves tremendous time by replacing the creation of new services and filling or changing data in the generated typeform. 