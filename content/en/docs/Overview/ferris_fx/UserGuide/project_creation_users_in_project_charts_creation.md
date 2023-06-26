---
title: "Projects"
linkTitle: "Projects"
weight: -15
description: >
  How to create Projects, Users and Charts within a projects.
---

This subcategory explains the creation of new projects and users within these projects.

## Project 

1. Click on *Projects* in the menu on the left side to open dropdown and then on List Projects
2. Click on *"+Add"*

{{< blocks/screenshot color="white" image="/images/list_projects_add_roboto.png">}}

1. Name the new project
2. Save

{{< blocks/screenshot color="white" image="/images/create_project_roboto.png">}}

{{< blocks/screenshot color="white" image="/images/list_projects_created_roboto.png">}}

Project on the Ferris Platform form the overarching organizational bracket for different types of objects. All users, services, scripts, parameters, secrets and other elements are organized into projects to ease enterprise data management. The default owner for new projects is the Platform Admin (PA).  

## Adding User(s) to the project

Once the project is created, the creator is automatically assigned as the Project Owner. All user roles on the project level are defined in detail as follows:

- **Project Owner** -  has all permissions on project and related entities (services, users) including deletion of project and users.
- **Project Admin** - has same permissions as the Owner, except deletion
- **Project User** - has only list / view permissions

**Below the Project User Matrix**

{{< blocks/screenshot color="white" image="/images/Ferris_Project_User_Matrix.png">}}

**Please note that users without Platform Administrator role, do not see any projects and services they are not assigned to. All project role rights are translated to service level also, eg. a user with Project User role will not be able to edit services of that project, only to list/view them and run a (manual) execution.**

1. Click on the magnifying glass to open Project details page


{{< blocks/screenshot color="white" image="/images/list_projects_loupe_roboto.png">}}


2. Click on *"+Add"* to add a new user to the project

{{< blocks/screenshot color="white" image="/images/click_add_new_user_roboto.png">}}



3. Choose a user from the drowdown 
4. Choose a user role from dropdown (Owner; Admin; User)
5. Click Save

{{< blocks/screenshot color="white" image="/images/add_new_project_user_roboto.png">}}


- Check the user has been added to the project

{{< blocks/screenshot color="white" image="/images/check_all_users_new.png">}}

Since new users were added, no service(s) are yet assigned to the project. A project needs to be assigned to an existing service. The details of "how to" can be found under [Executions/Services](/docs/user-guide/executions_services "Executions-Services").

Once a project was assigned to a service, the users created within that project will be able to perform their chores.

- Click on "List Services" to view the service the project belongs to

{{< blocks/screenshot color="white" image="/images/list_services_project.png">}}

##### Project Owner

1. Log in as *"Project Owner"*
2. Click on *Projects* to open dropdown and then List Projects

{{< blocks/screenshot color="white" image="/images/list_projects_as_projectowner_roboto.png">}}

As defined above, a Project Owner can  view and edit but not delete the projects he belongs to.

3. Click on the magnifying glass of the *Testing Demo Project*, the *List Services* tab should be redirected automatically. If not, click the *List Services* tab to view the services.

{{< blocks/screenshot color="white" image="/images/magnifying_glass_project_PO.png">}}

{{< blocks/screenshot color="white" image="/images/list_services_PO.png">}}

As Project Owner, one can add new services, view, edit and trigger manual runs but not delete the services within the projects the user belongs to.

##### Project Admin

1. Log in as *"Project Admin"*
2. Click on *Projects* to open dropdown and then *List Projects*

{{< blocks/screenshot color="white" image="/images/list_projects_as_projectadmin_roboto.png">}}

As defined above, a Project Admin can  view and edit the projects he belongs to but can not delete anything.

3. Click on the magnifying glass of the *Testing Demo Project*, the *List Services* tab should be redirected automatically. If not, click the *List Services* tab to view the services.

{{< blocks/screenshot color="white" image="/images/magnifying_glass_project_PA.png">}}

{{< blocks/screenshot color="white" image="/images/list_services_PA.png">}}

As Project Admin, one can add new services, view, edit and trigger manually runs within the projects the user belongs to.

**Project User**

1. Log in as "Project User"
2. Click on *Projects* to open dropdwon and then *List Projects*

{{< blocks/screenshot color="white" image="/images/list_projects_as_projectuser_roboto.png">}}

As defined above, a Project User can only view the projects he belongs to. He can neither edit, nor delete anything. 

3. Click on the magnifying glass of the *Testing Demo Project*, the *List Services* tab should be redirected automatically. If not, click the *List Services* tab to view the services.

{{< blocks/screenshot color="white" image="/images/view_services_as_projectuser_roboto.png">}}

{{< blocks/screenshot color="white" image="/images/list_services_PU.png">}}

As Project User, one can view services and trigger manually runs within the projects the user belongs to. The Project User can not delete or edit services and runs.

## Chart adding within the project

By default projects view page includes standard dashboard chart, but in project scope. Beside that, user can add additional charts that will be sourced by custom data.

Project Owners and Project Admins can create charts within a project. 

There are 3 different types of charts:

* Pie
* Line
* Table

The documentation on "how to format JSON data to render charts", can be found in the next subcategory: [Charts in Projects](/docs/user-guide/charts_in_projects/ "Charts in Projects").

**Note:** the API created by a user, returns the correctly formated JSON script.

Navigate to a previously created project.

1. Click on the "List Charts" tab 
2. Click on "+Add" to load the "Create Chart" page

{{< blocks/screenshot color="white" image="/images/list_charts.png">}}

1. Name the chart
2. Input the API url of the chart
3. Select the chart type in the dropdown menu:
   1. Pie
   2. Line
   3. Table
4. Select "Active" to activate the chart 
5. Click on "Preview" to verify if the JSON script returned by the API is structured as shown in the documentation
6. Click "Save" to create the chart on the project page

{{< blocks/screenshot color="white" image="/images/create_chart_pie.png">}}

The new chart will be displayed on the Project's "Details" page.

{{< blocks/screenshot color="white" image="/images/preview_chart_details_page.png">}}

The created chart can also be viewed under the "List Charts" tab.

{{< blocks/screenshot color="white" image="/images/list_charts_created_charts.png">}}
