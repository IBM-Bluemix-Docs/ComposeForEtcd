---
copyright:
  years: 2016,2018
lastupdated: "2018-06-11"

keywords: etcd, compose

subcollection: compose-for-etcd

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Connection Architecture
{: #connection-architecture}

{{site.data.keyword.composeForEtcd_full}} database connections are managed by 2 HAProxy portals. Each portal has 64 MB of memory.

The two portals allow for applications to maintain connectivity if one of the portals becomes unreachable. Failover at the client side is the responsibility of the application designer. Some etcd drivers automatically handle multiple connection strings and graceful failover. Unless you are working with a driver that completely handles failover errors, take the following steps to handle errors.

* Work with a driver that accepts multiple endpoints in its connection configuration.
* Ensure your application's calls to read from or write to the database react to errors appropriately. You can configure your application to react to errors in different ways.
  - Log the error and reconnect.
  - Reconnect and retry the operation that caused the error.
  - Queue the failed operation and schedule a reconnection.

## Encryption in Transit

All {{site.data.keyword.composeForEtcd}} HAProxy portals have TLS/SSL enabled and support TLS version 1.2. The certificates for the service are Let's Encrypt certificates.

## Connection Limits

Database connections have a connection limit of 2000 connections per portal. Exceeding the connection limit will make your service unresponsive. You can manage connections from your application through your driver's connection pooling feature.

## Proxy Timeouts

The HAProxy portals manage the lifecycle of connections between the server and client. We detail them here as a reference for driver writers and others who have an interest in the low-level activity of {{site.data.keyword.composeForEtcd}} database connections.

Setting | Value | Applies
----------|-----------|-----------
`client` | 1 day | When the client is expected to acknowledge or send data.
`connect` | 1 m | When a connection is being made between the proxy and the server.
`server` | 1 day | When the server is expected to acknowledge or send data.
`check` | 1 m | As a secondary timeout check when a connection is being made between the proxy and the server.
{: caption="Table 1. etcd HAProxy timeouts" caption-side="top"}
