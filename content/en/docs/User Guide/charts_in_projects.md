---
title: "Charts in Projects"
linkTitle: "Charts in Projects"
weight: -14
description: >-
  How to format JSON data to render proper charts. There are 3 types of charts:
    - Pie
    - Line
    - Table

---

## Pie Chart

Key/Value Pairs:

`data` - root element of charts data

`data.title` - Title of the chart that will be displayed on top

`data.type` - type of the chart (in this case - pie)

`data.labels` - array of labels for each slice of pie chart

`data.datasets` - actual data for the chart

`data.datasets.data` - array of values for each slice

`data.datasets.backgroundColor` - array of colors for each slice

*NOTE: Slice data will be labeled and colored with the values of element with same index across `labels`, `data`, `backgroundColor` arrays.*

Example of a valid Pie chart data - `data.json`:

```json
{
  "data": {
    "datasets": [
      {
        "backgroundColor": [
          "#008675",
          "#971b2f",
          "#448086",
          "#007FA3"
        ],
        "data": [
          608,
          224,
          0,
          0
        ],
      }
    ],
    "labels": [
      "completed",
      "failed",
      "pending",
      "in progress"
    ]
  },
  "title": "Executions by Status (Last 7 days)",
  "type": "pie"
}
```

## Line Chart 

Key/Value Pairs:

`data` - root element of charts data

`data.title` - Title of the chart that will be displayed on top

`data.type` - type of the chart (in this case - `pie`)

`data.labels` - array of labels for each point on X axis

`data.datasets` - array of objects that represents each line in the chart

`data.datasets[].data` - array of values for each point on X axis (defined by `data.labels`)

`data.datasets[].borderColor` - color of the line

`data.datasets[].backgroundColor` - color of the line - should be same value as `borderColor`, will be disabled

`data.datasets[].fill` - wether line should be filled - true is recomended, will be disabled

`data.datasets[].label` - label for the line (will be shown in legend)

Example of valid a Line chart data - `data.json`:

```json
{
  "data": {
    "datasets": [
      {
        "backgroundColor": "#008675",
        "borderColor": "#008675",
        "data": [
          0,
          0,
          0,
          0,
          0,
          0,
          0
        ],
        "fill": true,
        "label": "triggered"
      },
      {
        "backgroundColor": "#971b2f",
        "borderColor": "#971b2f",
        "data": [
          47,
          96,
          95,
          98,
          61,
          88,
          1
        ],
        "fill": true,
        "label": "scheduled"
      },
      {
        "backgroundColor": "#007FA3",
        "borderColor": "#007FA3",
        "data": [
          0,
          0,
          0,
          0,
          0,
          0,
          0
        ],
        "fill": true,
        "label": "manual"
      }
    ],
    "labels": [
      "04-06-22",
      "05-06-22",
      "06-06-22",
      "07-06-22",
      "08-06-22",
      "09-06-22",
      "05-02-23"
    ]
  },
  "title": "Executions Trigger Type per Day (Last 5 days)",
  "type": "line"
}
```

## Table Chart

Key/Value Pairs:

`title` - Title of the chart that will be displayed on top

`type` - type of the chart (in this case - `pie`)

`columns` - array of objects representing each column of the table

`columns[].field` - name of the field that is represented by column

`columns[].title` - column name that will be displayed

`data` - array of objects representing table rows. Each row object is consisted of `key:value` pairs which holds field name and value for it.

Example of a valid Table chart data - `data.json`:

```json
{
  "columns": [
    {
      "field": "package_name",
      "title": "Service Name"
    },
    {
      "field": "avg_time",
      "title": "Average Exec. Time"
    },
    {
      "field": "exec_count",
      "title": "Number of Exec."
    }
  ],
  "data": [
    {
      "avg_time": 341135.94,
      "exec_count": 154,
      "package_name": "test_context"
    },
    {
      "avg_time": 2950.1,
      "exec_count": 153,
      "package_name": "Test secret script"
    },
    {
      "avg_time": 2264.09,
      "exec_count": 154,
      "package_name": "test_import"
    },
    {
      "avg_time": 1507.73,
      "exec_count": 154,
      "package_name": "super test sql 124"
    },
    {
      "avg_time": 916.37,
      "exec_count": 3,
      "package_name": "test_manifest"
    },
    {
      "avg_time": 770.68,
      "exec_count": 3,
      "package_name": "dfasdfasfda"
    }
  ],
  "title": "Average Execution Time per Service in last 7 days",
  "type": "table"
}
```

