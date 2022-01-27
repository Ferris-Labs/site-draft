---
title: "CronJob"
linkTitle: "CronJob"
tags: [executor] 
categories: []
weight: -15
description: >-
  Overview and "How to" use CronJob for performing regular scheduled actions.
---

CronJobs are meant for performing regularly scheduled actions such as backups, report generation, and so on. Each of those tasks should be configured to recur indefinitely (for example: once a day / week / month). The point in time when the job is to be started can be freely defined.

#### Example:

This example Cron Job manifest triggers an event every minute:

```json
schedule: "*/1 * * * *"
```



#### Cron Schedule Syntax

```json
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                   7 is also Sunday on some systems)
# │ │ │ │ │
# │ │ │ │ │
# * * * * *
```



| Entry                  | Description                                                | Equivalent to |
| ---------------------- | ---------------------------------------------------------- | ------------- |
| @yearly (or @annually) | Run once a year at midnight of 1 January                   | 0 0 1 1 *     |
| @monthly               | Run once a month at midnight of the first day of the month | 0 0 1 * *     |
| @weekly                | Run once a week at midnight on Sunday morning              | 0 0 * * 0     |
| @daily (or @midnight)  | Run once a day at midnight                                 | 0 0 * * *     |
| @hourly                | Run once an hour at the beginning of the hour              | 0 * * * *     |

For example, the line below states that the task must be started every Friday at midnight, as well as on the 13th of each month at midnight:

```
0 0 13 * 5
```

To generate Cron Job schedule expressions, you can also use web tools like [crontab.guru](https://crontab.guru/).

