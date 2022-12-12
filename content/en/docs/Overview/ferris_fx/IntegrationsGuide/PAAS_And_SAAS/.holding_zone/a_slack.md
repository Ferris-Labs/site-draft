---
title: "slack"
linkTitle: "slack"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     slack Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.slack_webhook"></a>

# operators.slack\_webhook

<a id="operators.slack_webhook.SlackWebhookOperator"></a>

## SlackWebhookOperator Objects

```python
class SlackWebhookOperator(SimpleHttpOperator)
```

This operator allows you to post messages to Slack using incoming webhooks.

Takes both Slack webhook token directly and connection that has Slack webhook token.
If both supplied, http_conn_id will be used as base_url,
and webhook_token will be taken as endpoint, the relative path of the url.

Each Slack webhook token can be pre-configured to use a specific channel, username and
icon. You can override these defaults in this hook.

**Arguments**:

- `http_conn_id`: connection that has Slack webhook token in the extra field
- `webhook_token`: Slack webhook token
- `message`: The message you want to send on Slack
- `attachments`: The attachments to send on Slack. Should be a list of
dictionaries representing Slack attachments.
- `blocks`: The blocks to send on Slack. Should be a list of
dictionaries representing Slack blocks.
- `channel`: The channel the message should be posted to
- `username`: The username to post to slack with
- `icon_emoji`: The emoji to use as icon for the user posting to Slack
- `icon_url`: The icon image URL string to use in place of the default icon.
- `link_names`: Whether or not to find and link channel and usernames in your
message
- `proxy`: Proxy to use to make the Slack webhook call

<a id="operators.slack_webhook.SlackWebhookOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Call the SlackWebhookHook to post the provided Slack message

<a id="operators.slack"></a>

# operators.slack

<a id="operators.slack.SlackAPIOperator"></a>

## SlackAPIOperator Objects

```python
class SlackAPIOperator(BaseOperator)
```

Base Slack Operator

The SlackAPIPostOperator is derived from this operator.
In the future additional Slack API Operators will be derived from this class as well.
Only one of `slack_conn_id` and `token` is required.

**Arguments**:

- `slack_conn_id`: :ref:`Slack connection id <howto/connection:slack>`
which its password is Slack API token. Optional
- `token`: Slack API token (https://api.slack.com/web). Optional
- `method`: The Slack API Method to Call (https://api.slack.com/methods). Optional
- `api_params`: API Method call parameters (https://api.slack.com/methods). Optional
- `client_args`: Slack Hook parameters. Optional. Check airflow.providers.slack.hooks.SlackHook

<a id="operators.slack.SlackAPIOperator.construct_api_call_params"></a>

#### construct\_api\_call\_params

```python
def construct_api_call_params() -> Any
```

Used by the execute function. Allows templating on the source fields
of the api_call_params dict before construction

Override in child classes.
Each SlackAPIOperator child class is responsible for
having a construct_api_call_params function
which sets self.api_call_params with a dict of
API call parameters (https://api.slack.com/methods)

<a id="operators.slack.SlackAPIOperator.execute"></a>

#### execute

```python
def execute(**kwargs)
```

The SlackAPIOperator calls will not fail even if the call is not unsuccessful.
It should not prevent a DAG from completing in success

<a id="operators.slack.SlackAPIPostOperator"></a>

## SlackAPIPostOperator Objects

```python
class SlackAPIPostOperator(SlackAPIOperator)
```

Posts messages to a slack channel

Examples:

.. code-block:: python

    slack = SlackAPIPostOperator(
        task_id="post_hello",
        dag=dag,
        token="XXX",
        text="hello there!",
        channel="`random`",
    )

**Arguments**:

- `channel`: channel in which to post message on slack name (`general`) or
ID (C12318391). (templated)
- `username`: Username that airflow will be posting to Slack as. (templated)
- `text`: message to send to slack. (templated)
- `icon_url`: url to icon used for this message
- `attachments`: extra formatting details. (templated)
- see https://api.slack.com/docs/attachments.
- `blocks`: extra block layouts. (templated)
- see https://api.slack.com/reference/block-kit/blocks.

<a id="operators.slack.SlackAPIFileOperator"></a>

## SlackAPIFileOperator Objects

```python
class SlackAPIFileOperator(SlackAPIOperator)
```

Send a file to a slack channel

Examples:

.. code-block:: python

    # Send file with filename and filetype
    slack_operator_file = SlackAPIFileOperator(
        task_id="slack_file_upload_1",
        dag=dag,
        slack_conn_id="slack",
        channel="`general`",
        initial_comment="Hello World!",
        filename="/files/dags/test.txt",
        filetype="txt",
    )

    # Send file content
    slack_operator_file_content = SlackAPIFileOperator(
        task_id="slack_file_upload_2",
        dag=dag,
        slack_conn_id="slack",
        channel="`general`",
        initial_comment="Hello World!",
        content="file content in txt",
    )

**Arguments**:

- `channel`: channel in which to sent file on slack name (templated)
- `initial_comment`: message to send to slack. (templated)
- `filename`: name of the file (templated)
- `filetype`: slack filetype. (templated)
- see https://api.slack.com/types/file
- `content`: file content. (templated)

<a id="operators.slack.SlackAPIFileOperator.execute"></a>

#### execute

```python
def execute(**kwargs)
```

The SlackAPIOperator calls will not fail even if the call is not unsuccessful.
It should not prevent a DAG from completing in success

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_slack"></a>

# example\_dags.example\_slack

<a id="hooks"></a>

# hooks

<a id="hooks.slack_webhook"></a>

# hooks.slack\_webhook

<a id="hooks.slack_webhook.SlackWebhookHook"></a>

## SlackWebhookHook Objects

```python
class SlackWebhookHook(HttpHook)
```

This hook allows you to post messages to Slack using incoming webhooks.

Takes both Slack webhook token directly and connection that has Slack webhook token.
If both supplied, http_conn_id will be used as base_url,
and webhook_token will be taken as endpoint, the relative path of the url.

Each Slack webhook token can be pre-configured to use a specific channel, username and
icon. You can override these defaults in this hook.

**Arguments**:

- `http_conn_id`: connection that has Slack webhook token in the password field
- `webhook_token`: Slack webhook token
- `message`: The message you want to send on Slack
- `attachments`: The attachments to send on Slack. Should be a list of
dictionaries representing Slack attachments.
- `blocks`: The blocks to send on Slack. Should be a list of
dictionaries representing Slack blocks.
- `channel`: The channel the message should be posted to
- `username`: The username to post to slack with
- `icon_emoji`: The emoji to use as icon for the user posting to Slack
- `icon_url`: The icon image URL string to use in place of the default icon.
- `link_names`: Whether or not to find and link channel and usernames in your
message
- `proxy`: Proxy to use to make the Slack webhook call

<a id="hooks.slack_webhook.SlackWebhookHook.execute"></a>

#### execute

```python
def execute() -> None
```

Remote Popen (actually execute the slack webhook call)

<a id="hooks.slack"></a>

# hooks.slack

Hook for Slack

<a id="hooks.slack.SlackHook"></a>

## SlackHook Objects

```python
class SlackHook(BaseHook)
```

Creates a Slack connection to be used for calls.

Takes both Slack API token directly and connection that has Slack API token. If both are
supplied, Slack API token will be used. Also exposes the rest of slack.WebClient args.
Examples:
.. code-block:: python

    # Create hook
    slack_hook = SlackHook(token="xxx")  # or slack_hook = SlackHook(slack_conn_id="slack")

    # Call generic API with parameters (errors are handled by hook)
    #  For more details check https://api.slack.com/methods/chat.postMessage
    slack_hook.call("chat.postMessage", json={"channel": "`random`", "text": "Hello world!"})

    # Call method from Slack SDK (you have to handle errors yourself)
    #  For more details check https://slack.dev/python-slack-sdk/web/index.html#messaging
    slack_hook.client.chat_postMessage(channel="`random`", text="Hello world!")

**Arguments**:

- `token`: Slack API token
- `slack_conn_id`: :ref:`Slack connection id <howto/connection:slack>`
that has Slack API token in the password field.
- `use_session`: A boolean specifying if the client should take advantage of
connection pooling. Default is True.
- `base_url`: A string representing the Slack API base URL. Default is
``https://www.slack.com/api/``
- `timeout`: The maximum number of seconds the client will wait
to connect and receive a response from Slack. Default is 30 seconds.

<a id="hooks.slack.SlackHook.call"></a>

#### call

```python
def call(api_method: str, **kwargs) -> SlackResponse
```

Calls Slack WebClient `WebClient.api_call` with given arguments.

**Arguments**:

- `api_method`: The target Slack API method. e.g. 'chat.postMessage'. Required.
- `http_verb`: HTTP Verb. Optional (defaults to 'POST')
- `files`: Files to multipart upload. e.g. {imageORfile: file_objectORfile_path}
- `data`: The body to attach to the request. If a dictionary is provided,
form-encoding will take place. Optional.
- `params`: The URL parameters to append to the URL. Optional.
- `json`: JSON for the body to attach to the request. Optional.

**Returns**:

The server's response to an HTTP request. Data from the response can be
accessed like a dict.  If the response included 'next_cursor' it can be
iterated on to execute subsequent requests.

