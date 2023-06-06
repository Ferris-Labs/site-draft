---
title: "Release 2.0.5"
tags: ["releases"] 
categories: ["Release Notes"]
linkTitle:
weight: -108
description: >-
     New features, improvements and fixes provided to you in the 1st and 2nd Quarter of 2023.
---

![ferris_banner](/images/ferris_banner.png)


## New <img src="/images/added_blue.png" alt="added_blue" style="zoom:25%;" />

- Introduced the **Correlation ID** giving you the ability to track executions related to a single flow across multiple services.

- Introduced **programmatic retry function**, programatically execute retry of an execution giving the developer control over retries if a specific execution fails.

- Introduced a dedicated **listing of failed events**. For easier tracking and analysis of failed executions.

- Added a dedicated button for an **executive overview** of logs, triggers and parameters.

- Added a new UI for **combined logs** and **all scripts**. View aggregated logs of all steps of an execution from the 'list executions' view.

- Added a UI for **correlations based flow tracking**. UI for tracking executions which share a correlation ID.

- Added generic **extensions** and dashboard **improvements**.

---


## Changed <img src="/images/changed_yellow.png" alt="changed_yellow" style="zoom:25%;" /> 

- Switched to **Bootstrap 5**

---


## Improved <img src="/images/improved_green.png" alt="improved_green" style="zoom:25%;" />

- Added **caching of old executions** to improve the speed of rendering.

- Extension to **ferris_ef** library:

    - supporting new correlation id
    - support for logging. Logs of services which use the ferri_ef logging are aggregated to Kafka.
    - scheduling
    - programmatic retry

---


## Fixed <img src="/images/fixed_red.png" alt="fixed_red" style="zoom:25%;" />

- no fixes to report

---

