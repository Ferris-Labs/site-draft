---
title: "UI Generator"
linkTitle: "UI Generator"
weight: -10
description: >-
  Overview and "How to" generate UIs in a simplified and automated approach
---

The UI Generator has the ability to facilitate and automate manual processes in order to define step by step what has to be done. Based on definition of models, views and interfaces within the code, the generator will create UI automatically considering the configuration of modules as well.

Another script which has the ability to generate  UIs will be added to the package already created previously "Test Package with Scripts". This process will work as follows:

1. Click on Executions -> Packages to open the list of packages

2. Click on the edit icon to open the package/execution details

   ![](/images/edit_package.png)

3. Click on "+Add More Scripts" 

4. Click on "Choose file" to add the "parameters.json" file

5. Click on "Save"

![](/images/add_parametersjson_script.png)

**Note that the "parameters.json" file describes which parameters a user can input while executing the package. These parameters can be adapted to any use case.**

The "Run" button changed by displaying the package has a typeform that needs to be filled out by the user before finalizing the execution.

#### Create/Build the Typeform by clicking Run

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