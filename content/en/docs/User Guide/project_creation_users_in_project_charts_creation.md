---
title: "Projects"
linkTitle: "Projects"
weight: -15
description: >
  How to create Projects, Users and Charts within a projects.
---

This subcategory explains the creation of new projects and users withtin these projects.

## Project 

1. Click on *Projects* in the menu on the left side to open dropdown and then on List Projects
2. Click on *"+Add"*

{{< blocks/screenshot color="white" image="/images/list_projects_add_roboto.png">}}



1. Name the new project
2. Save

{{< blocks/screenshot color="white" image="/images/create_project_roboto.png">}}


{{< blocks/screenshot color="white" image="/images/list_projects_created_roboto.png">}}



Project on the Ferris Platform form the overarching organizational bracket for different types of objects. All users, packages, scripts, parameters, secrets and other elements are organized into projects to ease enterprise data management. The default owner for new projects is the Platform Admin (PA).  

## User creation within the project

Since the Platform Administrator created the Project, he is automatically assigned as the Project Owner. All user roles on the project level are defined in detail as follows:

- **Project Owner** -  has all permissions on project and related entities (packages, users) including deletion of project(s) (and users) created by the PO. By default it is the user that created project
- **Project Admin** - has all permissions as Owner except deletion
- **Project User** - has only list / view permissions

**Please note that users without Platform Administrator role, do not see any projects and packages they are not assigned to. All project role rights are translated to package level also, eg. a user with Project User role will not be able to edit packages of that project, only to list/view them and run a (manual) execution**

1. Click on the magnifying glass to open Project details page


{{< blocks/screenshot color="white" image="/images/list_projects_loupe_roboto.png">}}


2. Click on *"+Add"* to add a new user to the project

{{< blocks/screenshot color="white" image="/images/click_add_new_user_roboto.png">}}



3. Choose a user from the drowdown 
4. Choose a user role from dropdown (Owner; Admin; User)
5. Click Save

{{< blocks/screenshot color="white" image="/images/add_new_project_user_roboto.png">}}


- Check the user has been created

{{< blocks/screenshot color="white" image="/images/check_all_users_new.png">}}



Since new users were created, no package(s) are yet assigned to the project. A project needs to be assigned to an existing package as follows:

1. Click on *Executions* to open dropdown and then *Packages* in the menu on the left
2. Click on edit

{{< blocks/screenshot color="white" image="/images/edit_package_to_add_project_roboto.png">}}

3. Choose a project from dropdown
4. Click Save

{{< blocks/screenshot color="white" image="/images/added_project_to_package_roboto.png">}}

Once that a project was assigned to a package, the users created within that project will be able to perform their chores.

##### Project Owner

1. Log in as *"Project Owner"*
2. Click on *Projects* to open dropdown and then List Projects

{{< blocks/screenshot color="white" image="/images/list_projects_as_projectowner_roboto.png">}}

As defined above, a Project Owner can add new projects, view, edit and delete the projects he belongs to.

3. Click on *Executions* to open dropdown and then on *Packages*

{{< blocks/screenshot color="white" image="/images/view_packages_as_project_owner.png">}}

As Project Owner, one can add new packages, view, edit, delete and trigger manual runs and delete the packages within the projects the user belongs to.

##### Project Admin

1. Log in as *"Project Admin"*
2. Click on *Projects* to open dropdown and then *List Projects*

{{< blocks/screenshot color="white" image="/images/list_projects_as_projectadmin_roboto.png">}}

As defined above, a Project Admin can add new projects, view and edit the projects he belongs to but can not delete anything.

3. Click on *Executions* to open dropdown and then on *Packages*

{{< blocks/screenshot color="white" image="/images/view_packages_as_projectadmin_roboto.png">}}

As Project Admin, one can add new packages, view, edit and trigger manually runs within the projects the user belongs to. The Project Admin can not delete the packages, runs or related elements.

**Project User**

1. Log in as "Project User"
2. Click on *Projects* to open dropdwon and then *List Projects*

{{< blocks/screenshot color="white" image="/images/list_projects_as_projectuser_roboto.png">}}

As defined above, a Project User can only view the projects he belongs to. He can neither edit, nore delete anything. 

3. Click on *Executions* to open dropdown and then on *Packages*.

{{< blocks/screenshot color="white" image="/images/view_packages_as_projectuser_roboto.png">}}

As Project User, one can view packages and trigger manually runs within the projects the user belongs to. The Project User can not delete or edit packages, runs or related elements.

## Chart creation within the project

Charts within the projects are the same charts as used by default on the Ferris Platform Dashboard. The sole difference is that users can more specifically adapt the charts on the project level to their needs.

Project Owners and Project Admins can create charts within a project. 

There are 3 different types of charts:

* Pie
* Line
* Table

The documentation on "how to format JSON data to render charts", can be found in the next subcategory: [Charts in Projects](/docs/user-guide/charts_in_projects/ "Charts in Projects").

**Note:** the API created by an user, returns the correctly formated JSON script.

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

{{< blocks/screenshot color="white" image="/images/list_charts_created_charts">}}
