---
title: "Executions - Parallelisation"
linkTitle: "Executions - Parallelisation"
weight: -12
description: >-  
  Overview of service and executions prioritisation and priority based execution lanes.
---

## Executions prioritisation

Executions prioritisation is used to ensure that all service executions, especially ones with high priority, are executed in an expected time frame. Each service can be prioritised using the 1-10 priority scale:

- 1-3 - high priority
- 4-7 - medium priority
- 8-10 - low priority

The default priority is 5.

### Priority based execution lanes

There are 3 execution lanes based on priority and one lane reserved for scheduled executions:

| Lane      | Service priority                  |
| --------- | --------------------------------- |
| priority  | 1-3                               |
| default   | 4-7                               |
| slow      | 8-10                              |
| scheduled | reserved for scheduled executions |

Lanes are working in parallel. In case that one lane is under a heavy load, executions can be distributed to different (IDLE) lanes without changing the service priority.

### Auto re-prioritisation

If the last execution of a service took more than EXECUTOR_SLOW_THRESHOLD (configurable, default 300 seconds) it will be marked with prio 10 and it will be executed in the slow lane. This is not applicable to services that are marked with priority 1-3, those will execute in the priority lane and will not be subject of auto re-prioritisation regardless of its execution time. If a service is auto re-prioritisated as slow and it reduces execution time, its priority will not be automatically reverted to previous level, but it can be done manually via UI.

Scheduled executions will be executed through the scheduled lane regardless of service priority.

