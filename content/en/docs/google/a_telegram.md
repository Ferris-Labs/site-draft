---
title: "telegram"
linkTitle: "telegram"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     telegram Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="operators"></a>

# operators

<a id="operators.telegram"></a>

# operators.telegram

Operator for Telegram

<a id="operators.telegram.TelegramOperator"></a>

## TelegramOperator Objects

```python
class TelegramOperator(BaseOperator)
```

This operator allows you to post messages to Telegram using Telegram Bot API.

Takes both Telegram Bot API token directly or connection that has Telegram token in password field.
If both supplied, token parameter will be given precedence.

.. seealso::
    For more information on how to use this operator, take a look at the guide:
    :ref:`howto/operator:TelegramOperator`

**Arguments**:

- `telegram_conn_id`: Telegram connection ID which its password is Telegram API token
- `token`: Telegram API Token
- `chat_id`: Telegram chat ID for a chat/channel/group
- `text`: Message to be sent on telegram
- `telegram_kwargs`: Extra args to be passed to telegram client

<a id="operators.telegram.TelegramOperator.execute"></a>

#### execute

```python
def execute(context: 'Context') -> None
```

Calls the TelegramHook to post the provided Telegram message

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_telegram"></a>

# example\_dags.example\_telegram

Example use of Telegram operator.

<a id="hooks"></a>

# hooks

<a id="hooks.telegram"></a>

# hooks.telegram

Hook for Telegram

<a id="hooks.telegram.TelegramHook"></a>

## TelegramHook Objects

```python
class TelegramHook(BaseHook)
```

This hook allows you to post messages to Telegram using the telegram python-telegram-bot library.

The library can be found here: https://github.com/python-telegram-bot/python-telegram-bot
It accepts both telegram bot API token directly or connection that has telegram bot API token.
If both supplied, token parameter will be given precedence, otherwise 'password' field in the connection
from telegram_conn_id will be used.
chat_id can also be provided in the connection using 'host' field in connection.
Following is the details of a telegram_connection:
name: 'telegram-connection-name'
conn_type: 'http'
password: 'TELEGRAM_TOKEN'
host: 'chat_id' (optional)
Examples:
.. code-block:: python

    # Create hook
    telegram_hook = TelegramHook(telegram_conn_id="telegram_default")
    # or telegram_hook = TelegramHook(telegram_conn_id='telegram_default', chat_id='-1xxx')
    # or telegram_hook = TelegramHook(token='xxx:xxx', chat_id='-1xxx')

    # Call method from telegram bot client
    telegram_hook.send_message(None, {"text": "message", "chat_id": "-1xxx"})
    # or telegram_hook.send_message(None', {"text": "message"})

**Arguments**:

- `telegram_conn_id`: connection that optionally has Telegram API token in the password field
- `token`: optional telegram API token
- `chat_id`: optional chat_id of the telegram chat/channel/group

<a id="hooks.telegram.TelegramHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> telegram.bot.Bot
```

Returns the telegram bot client

**Returns**:

`telegram.bot.Bot`: telegram bot client

<a id="hooks.telegram.TelegramHook.send_message"></a>

#### send\_message

```python
@tenacity.retry(
    retry=tenacity.retry_if_exception_type(telegram.error.TelegramError),
    stop=tenacity.stop_after_attempt(5),
    wait=tenacity.wait_fixed(1),
)
def send_message(api_params: dict) -> None
```

Sends the message to a telegram channel or chat.

**Arguments**:

- `api_params`: params for telegram_instance.send_message. It can also be used to override chat_id

