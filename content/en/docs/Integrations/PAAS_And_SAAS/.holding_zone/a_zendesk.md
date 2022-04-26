---
title: "zendesk"
linkTitle: "zendesk"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     zendesk Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="example_dags"></a>

# example\_dags

<a id="example_dags.example_zendesk_custom_get"></a>

# example\_dags.example\_zendesk\_custom\_get

<a id="hooks"></a>

# hooks

<a id="hooks.zendesk"></a>

# hooks.zendesk

<a id="hooks.zendesk.ZendeskHook"></a>

## ZendeskHook Objects

```python
class ZendeskHook(BaseHook)
```

Interact with Zendesk. This hook uses the Zendesk conn_id.

**Arguments**:

- `zendesk_conn_id`: The Airflow connection used for Zendesk credentials.

<a id="hooks.zendesk.ZendeskHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> Zenpy
```

Get the underlying Zenpy client.

**Returns**:

zenpy.Zenpy client.

<a id="hooks.zendesk.ZendeskHook.get_ticket"></a>

#### get\_ticket

```python
def get_ticket(ticket_id: int) -> Ticket
```

Retrieve ticket.

**Returns**:

Ticket object retrieved.

<a id="hooks.zendesk.ZendeskHook.search_tickets"></a>

#### search\_tickets

```python
def search_tickets(**kwargs) -> SearchResultGenerator
```

Search tickets.

**Arguments**:

- `kwargs`: (optional) Search fields given to the zenpy search method.

**Returns**:

SearchResultGenerator of Ticket objects.

<a id="hooks.zendesk.ZendeskHook.create_tickets"></a>

#### create\_tickets

```python
def create_tickets(tickets: Union[Ticket, List[Ticket]],
                   **kwargs) -> Union[TicketAudit, JobStatus]
```

Create tickets.

**Arguments**:

- `tickets`: Ticket or List of Ticket to create.
- `kwargs`: (optional) Additional fields given to the zenpy create method.

**Returns**:

A TicketAudit object containing information about the Ticket created.
When sending bulk request, returns a JobStatus object.

<a id="hooks.zendesk.ZendeskHook.update_tickets"></a>

#### update\_tickets

```python
def update_tickets(tickets: Union[Ticket, List[Ticket]],
                   **kwargs) -> Union[TicketAudit, JobStatus]
```

Update tickets.

**Arguments**:

- `tickets`: Updated Ticket or List of Ticket object to update.
- `kwargs`: (optional) Additional fields given to the zenpy update method.

**Returns**:

A TicketAudit object containing information about the Ticket updated.
When sending bulk request, returns a JobStatus object.

<a id="hooks.zendesk.ZendeskHook.delete_tickets"></a>

#### delete\_tickets

```python
def delete_tickets(tickets: Union[Ticket, List[Ticket]], **kwargs) -> None
```

Delete tickets, returns nothing on success and raises APIException on failure.

**Arguments**:

- `tickets`: Ticket or List of Ticket to delete.
- `kwargs`: (optional) Additional fields given to the zenpy delete method.

