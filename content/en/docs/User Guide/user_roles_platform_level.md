---
title: "Security"
linkTitle: "Security"
weight: -17
description: >-
  How to add Users and define User Roles on a Platform level.
---
## Add Users and define User Roles

In this exemplary Use Case, three different user roles are defined: (**Suggestions for the Platform User Role Rules**)

1. **Platform Admin (PA)** has all permissions. The PA can see, add and delete services, events and users. In a production setting users should not be deletable due to  auditability and transparency reasons but rather deactivated to ensure a complete audit trail.
2. **Platform Executor (PE)** has similar permissions as the PA but lacks the ability to delete anything. The PE can edit and add events and services but not delete them. In addition the PE has the ability to execute case managent/approval processes. In this example setup the PE but may not see the Security tab to add or edit platform users.
3. **Public User** (not functional yet) can only see and verify existing events and services on the platform. All change abilities are restricted except for read only access to support verification and monitoring tasks.



**Note: The following process example only defines Plattform wide roles & users.**

1. Click on Security to open dropdown
2. Click on List Users to open the user details page
3. Click on "+" to add a new user

![](/images/security_list_users_roboto.png)

The following steps define how to create a new user:

1. First Name
2. Last Name
3. User Name (valid for authentication on DB or LDAP, unused OID auth)
4. Click checkbox to activate the user (can be deactivated if removed from project/company)
5. Email
6. Select the User Role
7. Save

![](/images/add_platform_user_roboto.png)

Click on Security -> List Users to check the created user

![](/images/list_users_new_blurred.png)

**Note: that the User Roles on project and application level still need to be defined.**
