---
title: "Case Management - Workflow"
linkTitle: "Workflow"
weight: -10
description: >-
  Overview and "How to" generate a Workflow to facilitate the verification of the administration process
---

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

#### Case Management / Approval Process

1. Click on Case Management in the left menu to open dropdown and then on Approvals

2. Click on "Info" to verify the data/file type, name and the bucket. Close "Info"

   ![](/images/case_management_workflow.png)

   ![](/images/cm_workflow_info.png)

3. **In this given use case, the administrator should download the file "view file" to verify the content to decide of its outcome. "Approve; Decline; Cancel"** 

4. Click on Approve

5. Add commentar to describe the reason why it has been approved

![](/images/workflow_approve.png)

![](/images/approval_comment.png)

6. Click on "Approved i" to check the reason it has been approved (declined; cancelled)

![](/images/approvedi_comment_check.png)

#### Execution Triggered 

Once the workflow was approved, an execution was triggered. Below the details and steps are verified:

1. Click on Workflows to open dropdwon and then on List Workflows
2. Click on the loupe to open details page

![](/images/list_workflows.png)

![](/images/workflow_details.png)

3. Click on "Steps" to check the execution steps of the approved workflow

![](/images/steps_workflow_execution.png)

The next step is to verify if the execution/package has been triggered.

1. Click on Executions -> Packages
2. Click on the loupe to open the details page of your execution/package
3. Click on "List Package Executions" to verify if it was triggered and completed

![](/images/triggered_execution_wf.png)

![](/images/execution_triggered_verified_wf.png)

**Note that any component of the FerrisFX app is a module on its own. Through the workflow we make it possible that any event can combine the different modules.**