---
title: "CronJob"
linkTitle: "CronJob"
weight: -15
description: >-
  How to use CronJob to schedule regularly recurring actions.
---

CronJobs are used to schedule regularly recurring actions such as backups, report generation and similar items. Each of those tasks should be configured to recur for an indefinite period into the future on a regular frequency (for example: once a day / week / month). The user also can define the point in time within that interval when the job should start.

## Example:

This example CronJob manifest would execute and trigger an event every minute:

```json
schedule: "*/1 * * * *"
```

## Cron Schedule Syntax

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

To generate CronJob schedule expressions, you can also use web tools like [crontab.guru](https://crontab.guru/).

