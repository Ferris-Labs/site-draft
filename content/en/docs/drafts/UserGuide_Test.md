---
title: "Ferris User Guide"
linkTitle: "User Guide"
weight: 1
description: >
  User Guide:
---



# Executor

The Executor is a custom framework allowing the organization and automatization of script processing which can be triggered:

- at a scheduled time (intervals)
- as a reaction to an event



### Getting Started

* Login to [home.ferris.ai](http://home.ferris.ai/)
* Login Credentials: 
  - Username (email)
  - Password

In this given Use Case the identity and access management process is secured through KeyCloak.



### Dashboard / Landing Page

The dashboard can show various statistics and analytics such as:

- User activities
- Page views
- Income (daily, weekly, total)
- Active projects

![](/images/ferris_home.png)

### Executor (Executions) 

Primar entities on "Executions" are packages which are composed by scripts that are executed in a defined order.

#### Executions -> Packages

In this given Use Case it is defined how to create and run a package.

1. Click on Executions on the left side of the dashboard menu to open drop-down
2. Click on Packages
3. Click on +Add to create a package

![](/images/Executions GB.png)



#### Create Package

1. Name package
2. Describe package
3. Select the Project to which the package will be bound
4. Add Tags manually or select from predefined tags
5. Schedule cron job -> "Cron like schedule definition. NOTE: day of week start on Monday (0 - Monday, 6 - Sunday)" example: "20****" -> meaning every 20 minutes of every hour, every day, every month and year.
6. Trigger Event Types - Select Value -> select event type to trigger the exectution of the package
7. Check the checkbox to Allow Manual Triggering -> click to allow manual triggering of the package
8. Check the checkbox to Activate your package -> click to set the package to active
9. Click on Choose file (optional) to Upload a Script -> upload a JSON "config.json" script to configure the package
10. Click on +Add More Scripts... to add more scripts -> upload a python "test_scr.py" script to pull the configuratio from config file and print all items
11. Click on Save to save package

![](/images/create_package_with_configs.png)



#### Check Created Package

The created package should be triggered every 20 minutes of every hour but can also be run manually.

- Click on the loupe icon to open the package's details page

![](/images/click_loupe_packages.png)

1. Check details page
2. Click on "Show Trigger Event"

![](/images/package_details_show_trigger_event.png)

1. Check the triggered event details
2. Close

![](/images/triggered_event_details.png)



#### Package Executions / Runs

- Click on the "Run" button down the page to run the package manually

![](/images/run_button_manual_package.png)

It will automatically transfer you to the "List Package Executions" tab

1. Check runs/package executions to see if you manually triggered execution was processed
2. Click on the loupe icon of your latest manually triggered run to open details page of the exectuion

![](/images/run_check_loupe_details.png)

1. Check the details "Show Package Execution" of the run/exection
2. Click on "List Steps" tab to see the steps of the execution

![](/images/exection_run_details.png)

1. Check the steps of the run and status (completed; pending; failed)
2. Click on "Show Results" to verify the script for failed executions

![](/images/run_list_steps.png)

![](/images/script_run_execution.png)

- Close window



## Taxonomies (Tagging) 

The following User Guide will explain and describe how to understand and use the Taxonomy/Tagging module.

**Tagging/Taxonomy** makes it easier to group and find similar functions, rules and data elements.



### Getting Started

* Login to [home.ferris.ai](http://home.ferris.ai/)
* Login Credentials: 
  - Username (email)
  - Password



### Taxonomy / Tagging 

It was developed as a module and can easily be added to any model by the developers/users.

Two different ways of adding tags are available:

- Executions -> Packages
- [Taxonomies -> Tags -> Please refer to section further down] (href="Taxonomies / Tags") [Taxonomies/Tags] (#Taxonomies/Tags)



#### Taxonomies / Tags

1. Click on Taxonomies in the left menu and then on Tags
2. Click Add to create a tag

![](/images/Taxonomies Tags Add.png)

1. Name Tag
2. Save

![](/images/Create Tag.png)

- Check created Tag(s)

1. Details 
2. Click on any tag to open details page  
3. Click on List Packages to see in which packages the same tags are used
4. Click on List Workflows to see in which workflows the same tags are used
5. Click on the Edit icon to edit a tag

![](/images/List packages 1 click tag.png)

![](/images/Details package.png)

![](/images/list packages 2.png)

![](/images/list workflows 3.png)

![](/images/Check Tag Details Edit.png)



#### Search Tag

1. Search Tag
2. Click Add Filter to choose a filter

![](/images/Search Tag.png)

1. Choose from the dropdown list
2. Insert Name
3. Hit the Search button

![](/images/Search with Filter.png)

1. Check search results

![](/images/search results.png)

