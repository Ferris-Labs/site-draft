---
title: "Case Management - Workflow"
linkTitle: "Workflow"
weight: -13
description: >-
  How to generate a Workflow to facilitate the verification of the administration process.
---

A workflow is an administrative process that consists in verifying, in this example the incomming data, before enabling a predefined mechanism and setting its status from "to be verified" to "done", "inactive" to "active" or "pending" to "approved". 

In this use case example, the workflow created works as follows:

1. A file gets uploaded to the File Storage (S3)
2. The file needs to be verified and approved by an "admin" role
3. The package/execution gets triggered by the approval

#### Getting Started

1. On the left side menu, click on *Workflows* to open dropdown
2. Click on *List Workflows*
3. Click on *"+Add"* to create a new workflow

![](/images/list_workflows.png)

**Note that before starting to input the values for the workflow, the JSON file needs to be edited:**

**1. "package_id" in the JSON file which is the "Uuid (unique user ID)" in the predefined package/execution**

**2. package_name" in the JSON file which is also called "Package Name" in the predefined package/execution**

![](/images/uuid_packagename_edit_json.png)

Change the template / example values to the values from the package and safe JSON file.

1. Name the workflow
2. Add a description
3. Add Tags 
4. Copy and paste the script from the JSON file
5. Copy from the script the "source" and paste it to the "Entrypoint source"
6. Copy from the script the "event_type" and paste it to the "Entrypoint event"
7. Click the checkbox to set the workflow as active
8. Click "Save"

![](/images/create_workflow.png)

##### workflow_script.json

The workflow module gives user possibility to define a list of actions that should be executed in a certain order as reaction to some event. Each workflow is defined with it’s entrypoint (event that will trigger the workflow execution) and a list of steps (actions).

```json
{
  'workflow': {
    'entrypoint': {
      'type': 'event',
      'source': 'ferris.apps.web',
      'event_type': 'ferris.apps.modules.minio.file_uploaded'
    },
    'steps': [
      {
        'event_type': 'ferris.apps.modules.minio.file_uploaded',
        'actions': [
          {
            'event_type': 'ferris.apps.modules.approvals.approve_step',
            'action_name': 'File Content Verification',
            'additional_data': {
              'approval_type': 'file_content_verification',
              'approval_role': 'Admin'
            }
          }]
      },
      {
        'event_type': 'ferris.apps.modules.approvals.step_approval_completed',
        'actions': [
          {
            'event_type': 'ferris_executor.run_execution.scheduled_run',
            'action_name': 'Trigger Execution',
            'additional_data': {
              'package_id': '0b2d6295-d0a9-40b5-84df-c95d5d407a9c',
              'package_name': 'ferris.executor.packages.test_package_with_scripts'
            },
            'condition': {
              'approval_status': 'Approved'
            }
          },
          {
            'event_type': 'ferris.apps.modules.workflow.execution_canceled',
            'action_name': 'Workflow Canceled',
            'additional_data': {
            },
            'condition': {
              'approval_status': 'Canceled'
            }
          }]
      },
      {
        'event_type': 'ferris_executor.run_execution.execution_finished',
        'actions': [
        ]
      }]
  }
}
```

#### 

**Upload a file to the bucket to test the approval process**

1. Click on *File Storage* in the left menu to open dropdown
2. Click on *List Files*
3. Click on *"+Add"*

![](/images/upload_file_test_workflow.png)

1. Choose File to insert
2. Select File/Data Type in dropdown (CSV Table; Plain Text; JSON)
3. Select Bucket Name (scripts; test; testbucket)
4. Save 

![](/images/select_file_test_workflow.png)

#### Case Management / Approval Process

1. Click on *Case Management* in the left menu to open dropdown and then on *Approvals*

2. Click on *"Info"* to verify the data/file type, name and the bucket. Close "Info"

   ![](/images/case_management_workflow.png)

   ![](/images/cm_workflow_info.png)

3. In this example use case, the administrator should download the file "view file" to verify the content to decide of the outcome of the approval and then decide to "Approve", "Decline" or "Cancel" 

4. Click on *Approve*

5. Add a comment to describe the reason for the approval / dismissal

![](/images/workflow_approve.png)

![](/images/approval_comment.png)

6. Click on *"Approved i"* to check the reason it has been approved (declined; cancelled)

![](/images/approvedi_comment_check.png)

#### Execution Triggered 

Once the workflow was approved, an execution was triggered. 
Below the details and steps executed are verified:

1. Click on *Workflows* to open dropdown and then on *List Workflows*
2. Click on the magnifying glass to open details page

![](/images/list_workflows.png)

![](/images/workflow_details.png)

3. Click on *"Steps"* to check the execution steps of the approved workflow

![](/images/steps_workflow_execution.png)

The next step is to verify if the execution/package has been triggered.

1. Click on Executions -> Packages
2. Click on the magnifying glass to open the details page of your execution/package
3. Click on "List Package Executions" to verify if it was triggered and completed

![](/images/triggered_execution_wf.png)

![](/images/execution_triggered_verified_wf.png)

**Note that any component of the FerrisFX app is a module on its own. Through the workflow we make it possible that any event can be combined across different modules. Hence it also is possible to model an event cascade that involves different approval and manual parameter entry UI steps as required by any given enterprise use case.**