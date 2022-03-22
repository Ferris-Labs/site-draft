---
title: "discord"
linkTitle: "discord"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     discord Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.discord_webhook"></a>

# operators.discord\_webhook

<a id="operators.discord_webhook.DiscordWebhookOperator"></a>

## DiscordWebhookOperator Objects

```python
class DiscordWebhookOperator(SimpleHttpOperator)
```

This operator allows you to post messages to Discord using incoming webhooks.

Takes a Discord connection ID with a default relative webhook endpoint. The
default endpoint can be overridden using the webhook_endpoint parameter
(https://discordapp.com/developers/docs/resources/webhook).

Each Discord webhook can be pre-configured to use a specific username and
avatar_url. You can override these defaults in this operator.

**Arguments**:

- `http_conn_id`: Http connection ID with host as "https://discord.com/api/" and
default webhook endpoint in the extra field in the form of
{"webhook_endpoint": "webhooks/{webhook.id}/{webhook.token}"}
- `webhook_endpoint`: Discord webhook endpoint in the form of
"webhooks/{webhook.id}/{webhook.token}"
- `message`: The message you want to send to your Discord channel
(max 2000 characters). (templated)
- `username`: Override the default username of the webhook. (templated)
- `avatar_url`: Override the default avatar of the webhook
- `tts`: Is a text-to-speech message
- `proxy`: Proxy to use to make the Discord webhook call

<a id="operators.discord_webhook.DiscordWebhookOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Call the DiscordWebhookHook to post message

<a id="hooks"></a>

# hooks

<a id="hooks.discord_webhook"></a>

# hooks.discord\_webhook

<a id="hooks.discord_webhook.DiscordWebhookHook"></a>

## DiscordWebhookHook Objects

```python
class DiscordWebhookHook(HttpHook)
```

This hook allows you to post messages to Discord using incoming webhooks.

Takes a Discord connection ID with a default relative webhook endpoint. The
default endpoint can be overridden using the webhook_endpoint parameter
(https://discordapp.com/developers/docs/resources/webhook).

Each Discord webhook can be pre-configured to use a specific username and
avatar_url. You can override these defaults in this hook.

**Arguments**:

- `http_conn_id`: Http connection ID with host as "https://discord.com/api/" and
default webhook endpoint in the extra field in the form of
{"webhook_endpoint": "webhooks/{webhook.id}/{webhook.token}"}
- `webhook_endpoint`: Discord webhook endpoint in the form of
"webhooks/{webhook.id}/{webhook.token}"
- `message`: The message you want to send to your Discord channel
(max 2000 characters)
- `username`: Override the default username of the webhook
- `avatar_url`: Override the default avatar of the webhook
- `tts`: Is a text-to-speech message
- `proxy`: Proxy to use to make the Discord webhook call

<a id="hooks.discord_webhook.DiscordWebhookHook.execute"></a>

#### execute

```python
def execute() -> None
```

Execute the Discord webhook call

