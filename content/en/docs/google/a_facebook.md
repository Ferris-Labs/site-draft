---
title: "facebook"
linkTitle: "facebook"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     facebook Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="ads"></a>

# ads

<a id="ads.hooks.ads"></a>

# ads.hooks.ads

This module contains Facebook Ads Reporting hooks

<a id="ads.hooks.ads.JobStatus"></a>

## JobStatus Objects

```python
class JobStatus(Enum)
```

Available options for facebook async task status

<a id="ads.hooks.ads.FacebookAdsReportingHook"></a>

## FacebookAdsReportingHook Objects

```python
class FacebookAdsReportingHook(BaseHook)
```

Hook for the Facebook Ads API

.. seealso::
    For more information on the Facebook Ads API, take a look at the API docs:
    https://developers.facebook.com/docs/marketing-apis/

**Arguments**:

- `facebook_conn_id`: Airflow Facebook Ads connection ID
- `api_version`: The version of Facebook API. Default to None. If it is None,
it will use the Facebook business SDK default version.

<a id="ads.hooks.ads.FacebookAdsReportingHook.multiple_accounts"></a>

#### multiple\_accounts

```python
@cached_property
def multiple_accounts() -> bool
```

Checks whether provided account_id in the Facebook Ads Connection is provided as a list

<a id="ads.hooks.ads.FacebookAdsReportingHook.facebook_ads_config"></a>

#### facebook\_ads\_config

```python
@cached_property
def facebook_ads_config() -> Dict
```

Gets Facebook ads connection from meta db and sets
facebook_ads_config attribute with returned config file

<a id="ads.hooks.ads.FacebookAdsReportingHook.bulk_facebook_report"></a>

#### bulk\_facebook\_report

```python
def bulk_facebook_report(
    params: Optional[Dict[str, Any]],
    fields: List[str],
    sleep_time: int = 5
) -> Union[List[AdsInsights], Dict[str, List[AdsInsights]]]
```

Pulls data from the Facebook Ads API regarding Account ID with matching return type.

The return type and value depends on the ``account_id`` configuration. If the
configuration is a str representing a single Account ID, the return value is the
list of reports for that ID. If the configuration is a list of str representing
multiple Account IDs, the return value is a dict of Account IDs and their
respective list of reports.

**Arguments**:

- `fields`: List of fields that is obtained from Facebook. Found in AdsInsights.Field class.
https://developers.facebook.com/docs/marketing-api/insights/parameters/v6.0
- `params`: Parameters that determine the query for Facebook
https://developers.facebook.com/docs/marketing-api/insights/parameters/v6.0
- `sleep_time`: Time to sleep when async call is happening

**Returns**:

`List[AdsInsights] or Dict[str, List[AdsInsights]]`: Facebook Ads API response,
converted to Facebook Ads Row objects regarding given Account ID type

<a id="ads.hooks"></a>

# ads.hooks

