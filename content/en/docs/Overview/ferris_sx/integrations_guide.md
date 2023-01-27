---
title: "Integrations Guide"
linkTitle: "Integrations Guide"
weight: 2
description: >
  Ferris SX Integrations Guide (for Engineers).
---

## How does it Work?

There are two main approaches to implementing the external notifications support.

* Implementation within a Ferris SX container
* Implementation in an Exit Gateway

The 2nd option is used in platforms which are behind a firewall and therefore require the gateway to be outside the firewall for accessing external services. In these cases the adapter runs as a separate container. 

Irrespective of the infrastructure implementation the service internal API (as illustrated above) does not change.
