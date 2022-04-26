---
title: "imap"
linkTitle: "imap"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     imap Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="sensors"></a>

# sensors

<a id="sensors.imap_attachment"></a>

# sensors.imap\_attachment

This module allows you to poke for attachments on a mail server.

<a id="sensors.imap_attachment.ImapAttachmentSensor"></a>

## ImapAttachmentSensor Objects

```python
class ImapAttachmentSensor(BaseSensorOperator)
```

Waits for a specific attachment on a mail server.

**Arguments**:

- `attachment_name`: The name of the attachment that will be checked.
- `check_regex`: If set to True the attachment's name will be parsed as regular expression.
Through this you can get a broader set of attachments
that it will look for than just only the equality of the attachment name.
- `mail_folder`: The mail folder in where to search for the attachment.
- `mail_filter`: If set other than 'All' only specific mails will be checked.
See :py:meth:`imaplib.IMAP4.search` for details.
- `imap_conn_id`: The :ref:`imap connection id <howto/connection:imap>` to run the sensor against.

<a id="sensors.imap_attachment.ImapAttachmentSensor.poke"></a>

#### poke

```python
def poke(context: 'Context') -> bool
```

Pokes for a mail attachment on the mail server.

**Arguments**:

- `context`: The context that is being provided when poking.

**Returns**:

`bool`: True if attachment with the given name is present and False if not.

<a id="hooks"></a>

# hooks

<a id="hooks.imap"></a>

# hooks.imap

This module provides everything to be able to search in mails for a specific attachment
and also to download it.
It uses the imaplib library that is already integrated in python 3.

<a id="hooks.imap.ImapHook"></a>

## ImapHook Objects

```python
class ImapHook(BaseHook)
```

This hook connects to a mail server by using the imap protocol.

.. note:: Please call this Hook as context manager via `with`
    to automatically open and close the connection to the mail server.

**Arguments**:

- `imap_conn_id`: The :ref:`imap connection id <howto/connection:imap>`
that contains the information used to authenticate the client.

<a id="hooks.imap.ImapHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> 'ImapHook'
```

Login to the mail server.

.. note:: Please call this Hook as context manager via `with`
    to automatically open and close the connection to the mail server.

**Returns**:

`ImapHook`: an authorized ImapHook object.

<a id="hooks.imap.ImapHook.has_mail_attachment"></a>

#### has\_mail\_attachment

```python
def has_mail_attachment(name: str,
                        *,
                        check_regex: bool = False,
                        mail_folder: str = 'INBOX',
                        mail_filter: str = 'All') -> bool
```

Checks the mail folder for mails containing attachments with the given name.

**Arguments**:

- `name`: The name of the attachment that will be searched for.
- `check_regex`: Checks the name for a regular expression.
- `mail_folder`: The mail folder where to look at.
- `mail_filter`: If set other than 'All' only specific mails will be checked.
See :py:meth:`imaplib.IMAP4.search` for details.

**Returns**:

`bool`: True if there is an attachment with the given name and False if not.

<a id="hooks.imap.ImapHook.retrieve_mail_attachments"></a>

#### retrieve\_mail\_attachments

```python
def retrieve_mail_attachments(name: str,
                              *,
                              check_regex: bool = False,
                              latest_only: bool = False,
                              mail_folder: str = 'INBOX',
                              mail_filter: str = 'All',
                              not_found_mode: str = 'raise') -> List[Tuple]
```

Retrieves mail's attachments in the mail folder by its name.

**Arguments**:

- `name`: The name of the attachment that will be downloaded.
- `check_regex`: Checks the name for a regular expression.
- `latest_only`: If set to True it will only retrieve the first matched attachment.
- `mail_folder`: The mail folder where to look at.
- `mail_filter`: If set other than 'All' only specific mails will be checked.
See :py:meth:`imaplib.IMAP4.search` for details.
- `not_found_mode`: Specify what should happen if no attachment has been found.
Supported values are 'raise', 'warn' and 'ignore'.
If it is set to 'raise' it will raise an exception,
if set to 'warn' it will only print a warning and
if set to 'ignore' it won't notify you at all.

**Returns**:

`a list of tuple`: a list of tuple each containing the attachment filename and its payload.

<a id="hooks.imap.ImapHook.download_mail_attachments"></a>

#### download\_mail\_attachments

```python
def download_mail_attachments(name: str,
                              local_output_directory: str,
                              *,
                              check_regex: bool = False,
                              latest_only: bool = False,
                              mail_folder: str = 'INBOX',
                              mail_filter: str = 'All',
                              not_found_mode: str = 'raise') -> None
```

Downloads mail's attachments in the mail folder by its name to the local directory.

**Arguments**:

- `name`: The name of the attachment that will be downloaded.
- `local_output_directory`: The output directory on the local machine
where the files will be downloaded to.
- `check_regex`: Checks the name for a regular expression.
- `latest_only`: If set to True it will only download the first matched attachment.
- `mail_folder`: The mail folder where to look at.
- `mail_filter`: If set other than 'All' only specific mails will be checked.
See :py:meth:`imaplib.IMAP4.search` for details.
- `not_found_mode`: Specify what should happen if no attachment has been found.
Supported values are 'raise', 'warn' and 'ignore'.
If it is set to 'raise' it will raise an exception,
if set to 'warn' it will only print a warning and
if set to 'ignore' it won't notify you at all.

<a id="hooks.imap.Mail"></a>

## Mail Objects

```python
class Mail(LoggingMixin)
```

This class simplifies working with mails returned by the imaplib client.

**Arguments**:

- `mail_body`: The mail body of a mail received from imaplib client.

<a id="hooks.imap.Mail.has_attachments"></a>

#### has\_attachments

```python
def has_attachments() -> bool
```

Checks the mail for a attachments.

**Returns**:

`bool`: True if it has attachments and False if not.

<a id="hooks.imap.Mail.get_attachments_by_name"></a>

#### get\_attachments\_by\_name

```python
def get_attachments_by_name(name: str,
                            check_regex: bool,
                            find_first: bool = False) -> List[Tuple[Any, Any]]
```

Gets all attachments by name for the mail.

**Arguments**:

- `name`: The name of the attachment to look for.
- `check_regex`: Checks the name for a regular expression.
- `find_first`: If set to True it will only find the first match and then quit.

**Returns**:

`list(tuple)`: a list of tuples each containing name and payload
where the attachments name matches the given name.

<a id="hooks.imap.MailPart"></a>

## MailPart Objects

```python
class MailPart()
```

This class is a wrapper for a Mail object's part and gives it more features.

**Arguments**:

- `part`: The mail part in a Mail object.

<a id="hooks.imap.MailPart.is_attachment"></a>

#### is\_attachment

```python
def is_attachment() -> bool
```

Checks if the part is a valid mail attachment.

**Returns**:

`bool`: True if it is an attachment and False if not.

<a id="hooks.imap.MailPart.has_matching_name"></a>

#### has\_matching\_name

```python
def has_matching_name(name: str) -> Optional[Tuple[Any, Any]]
```

Checks if the given name matches the part's name.

**Arguments**:

- `name`: The name to look for.

**Returns**:

`tuple`: True if it matches the name (including regular expression).

<a id="hooks.imap.MailPart.has_equal_name"></a>

#### has\_equal\_name

```python
def has_equal_name(name: str) -> bool
```

Checks if the given name is equal to the part's name.

**Arguments**:

- `name`: The name to look for.

**Returns**:

`bool`: True if it is equal to the given name.

<a id="hooks.imap.MailPart.get_file"></a>

#### get\_file

```python
def get_file() -> Tuple
```

Gets the file including name and payload.

**Returns**:

`tuple`: the part's name and payload.

