---
title: "Project Creation & Users within the Project"
linkTitle: "Project Creation & Users within the Project"
weight: -12
description: >
  Overview and "How to" create Projects and Users within the Project.
---

In this subcategory the creation of new projects and users withtin the project will be elaborated.

#### Project

1. Click on Projects in the menu on the left side to open dropdown and then on List Projects
2. Click on "+Add"

![](/images/list_projects_add.png)

1. Name the new project
2. Save

![](/images/create_project.png)

![](/images/list_projects_created.png)

In this given use case, the Project was created by the Platform Administrator which has insights in all projects on the Ferris Platform. 

#### User creation within the project

Since the Platform Administrator created the Project, he is automatically assigned as the Project Owner. All user roles on the project level are defined in debt as follows:

- **Project Owner -  has all permissions on project and related entities (packages, users) including deletion of project(s) (and users) created by the PO. By default it is the user that created project**
- **Project Admin - has all permissions as Owner except deletion**
- **Project User - has only list / view permissions**

**Please note that users without Platform Administrator role, won't see any projects and packages they are not belonging to. All project role rights are translated to package level also, eg. a user with Project User role will not be able to edit packages of that project, only to list/view them and run (manually) an execution**

1. Click on the magnifying glass to open Project details page

![](/images/list_projects_details.png)

2. Click on "+Add" to add a new user to the project

![](/images/click_add_new_user.png)

3. Choose a user from the drowdown 
4. Choose a user role from dropdown (Owner; Admin; User)
5. Click Save

![](/images/add_new_project_user.png)

- Check created users

![](/images/check_all_users.png)

Since new users were created, no package(s) are yet assigned to the project. A project needs to be assigned to an existing package as follows:

1. Click on Executions to open dropdown and then Packages in the menu on the left
2. Click on edit

![](/images/edit_package_to_add_project.png)

3. Choose a project from dropdown
4. Click Save

![](/images/added_project_to_package.png)

Once that a project was assigned to a package, the users created within the project will be able to perform their cores.

##### Project Owner

1. Log in as "Project Owner"
2. Click on Projects to open dropdown and then List Projects

![](/images/list_projects_as_projectowner.png)

As defined above, a Project Owner can add new projects, view, edit and delete the projects he belongs to.

3. Click on Executions to open dropdown and then on Packages

![](/images/view_packages_as_project_owner.png)

As Project Owner, one can add new packages, view, edit, delete and trigger manually runs and delete the packages within the projects the user belongs to.

##### Project Admin

1. Log in as "Project Admin"
2. Click on Projects to open dropdown and then List Projects

![](/images/list_projects_as_projectadmin.png)

As defined above, a Project Admin can add new projects, view and edit the projects he belongs to but can not delete anything.

3. Click on Executions to open dropdown and then on Packages

![](/images/view_packages_as_projectadmin.png)

As Project Admin, one can add new packages, view, edit and trigger manually runs within the projects the user belongs to. The Project Admin can not delete the packages, runs, whatsoever.

**Project User**

1. Log in as "Project User"
2. Click on Projects to open dropdwon and then List Projects

![](/images/list_projects_as_projectuser.png)

As defined above, a Project User can only view the projects he belongs to. He can neither edit, nore delete anything. 

3. Click on Executions to open dropdown and then on Packages.

![](/images/view_packages_as_projectuser.png)

As Project User, one can view packages and trigger manuallz runs within the projects the user belongs to. The Project User can not delete or edit packages, runs, whatsoever.

