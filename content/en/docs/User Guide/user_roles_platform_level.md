---
title: "Security"
linkTitle: "Security"
weight: -17
description: >-
  Overview and "How to" add Users and define User Roles on a Platform level.
---
#### Add Users and define User Roles

In this given Use Case, 3 different user roles are defined: (**Suggestions for the Platform User Role Rules**)

1. **Platform Admin has all permissions. The PA can see, add and delete services, events and users to some extend. Users should not be deletable due to security reasons such auditability and transparency but deactivated so it leaves a track record.**
2. **Platform Executor has similar permissions as the PA, with the exception that the ability to delete anything will be disabled. The PE can edit and add but not delete events and services. The PE has the ability to execute case managent/approval processes but has not the ability to see the Security tab to add or edit platform users.**
3. **Platform Public User (not functional yet BTW) can only see and verify the different events and services on the platform. The abilities are restricted, read only access for verification.**



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
