---
title: "Security"
linkTitle: "Security"
tags: [security, access rights] 
categories: [Security]
weight: -7
description: >-
  Introduction and "how-to" guide to the Ferris Security and Access Rights Management.

---

#### Concept

Ferris is taking a multi-layered and integrative approach to security and access rights management, protecting systems, networks, users and data alike.

While the security architecture of Ferris stands alone and operates well in isolation, it is built to integrate with enterprise security systems such as LDAP and Active Directory. 

It supports Single Sign On (SSO) through open protocols such as Auth0 and SAML.

This user guide focuses on the application internal - user controlled - aspects of the seurity functions.



#### Approach

Ferris applies the proven notion of #Users, #Roles and #Permissions and linking them to the application elements such as #Menues, Views and Pages.

This approach enables the breaking of the application into granular elements and organizing them into groups of like access control areas. The ultimate benefit is the implementation of user rights on a strict "need-to-know" basis.



#### Security Components

In the following sections you will learn how the security components work and how to set them up for your purpose.

> If you want to follow the instructions and examples, you first need to connect to your Ferris demo instance. The  [#Ferris Connect Quickstart]({{< ref "connect_quickstart.md" >}}) instructions will show you how.

##### Navigation

The Security menu is found on left hand navigation of Ferris. 

- Click on the Security menu to expand it and display all security relevant menu items.

![](/images/security_navigation.png)

*Ferris Security Navigation*

- [**List Users:**]({{< ref "users.md" >}}) Setup individual users and assign one or more roles to them. If Ferris is integrated with a company own Single Sign On, here is where all users can be viewed. Each user may be deactivated manually.
- [**List Roles:**]({{< ref "roles.md" >}}) Setup and maintain individual roles and assign them viewing, editing, executing and other rights pertinent to the character and scope of the role. Roles can be integrated and inheritet with the company Active Directory.
- **Users Statistics:** Useful grafical statistic displaying the login behavior of individual users, such as login count and failed logins. For *Security Admins* only.
- **User Registrations:** Listing pending registration requests. For *Security Admins* only.
- **Base Permissions:** Listing the base permissions. For *Security Admins* only.
- **Views/Menus:** Listing of all Menu and View (aka Pages, UI) items. For *Security Admins* only.
- **Permissions on Views/Menus:** Listing of the assigned permissions of each Menu and View element. For *Security Admins* only.

*NOTE that it is considered a good practice that security related tasks are provided to only a few dedicated Security Leads within the organization. For that purpose, setting up a dedicated **Security Lead** role is advised.*



#### Authentication and Authorization

Add text 



#### Data Level Security

Add text



#### Integrations

Add text



#### Audit Functions

Add viewing function (below)

Add logging and monitoring capabilities

