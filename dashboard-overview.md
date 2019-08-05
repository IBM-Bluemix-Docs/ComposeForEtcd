---

Copyright:
  years: 2017,2018
lastupdated: "2018-05-07"

keywords: etcd, compose

subcollection: compose-for-etcd

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Service Overview
{: #dashboard-overview}

The _Overview_ page shows you information about your {{site.data.keyword.cloud}} Compose database, including essential identifying information and current resource usage. It also includes connection strings that you can use with tools to connect to your database.

## Deployment Details

The _Deployment Details_ panel shows details of your service.

![Deployment Details](./images/etcd-deployment-details.png "A view of the Deployment Details panel")

### Type

The type of database that is offered by the service, and the database version that your service uses. If a more recent database version is available, a notification is displayed, and a link to the [Upgrade version](/docs/services/ComposeForEtcd?topic=compose-for-etcd-dashboard-settings#upgrade-version) section of your service dashboard.

### ID

An internal identifier for the service.

### Usage

The size of your database and the amount of storage that is provided by your service plan.

## Recent Tasks

Making administrative changes to your service (such as scaling, or taking a manual backup) starts a task. While the task is running, the _Recent Tasks_ panel shows the task name and a progress bar.

## Connection Strings

Connection Strings can be used by some client libraries and contain all the information that is needed for other libraries to connect. You can find out how to use a Connection String to connect to {{site.data.keyword.composeForEtcd_full}} in [Connecting an external application](/docs/services/ComposeForEtcd?topic=compose-for-etcd-external-app).

You can find each Connection String for your service in a different tab in the _Connection Strings_ panel.
{: tip}

### HTTPS

The **HTTPS** connection string can be used by some client libraries and contains all the information that is needed for other libraries to connect. For more information, [Connecting an external application](/docs/services/ComposeForEtcd?topic=compose-for-etcd-external-app).

### Command Line

The **Command Line** is a preformatted command that invokes `etcd` with the correct parameters. To use it, you need to have the etcd client tools installed on the local system. For more information, see [Connecting an external application](/docs/services/ComposeForEtcd?topic=compose-for-etcd-external-app).

### SSL Certificate

Your Compose {{site.data.keyword.cloud}} service provides you with an SSL certificate that you can use to connect to your database.

## Instance Administration API

You can manage your {{site.data.keyword.composeForEtcd}} service through the {{site.data.keyword.cloud_notm}} Compose API.

### Foundation Endpoint

The foundation endpoint is composed of the region the service resides in and the service instance ID. It is found at the start of every endpoint.

### Deployment ID

The deployment ID is necessary for most calls, and identifies the specific deployment instance.

### Reference

For more documentation and reference for using the {{site.data.keyword.cloud_notm}} Compose API, across all {{site.data.keyword.cloud_notm}} Compose services, read [The {{site.data.keyword.cloud_notm}} Compose API](https://www.compose.com/articles/the-ibm-cloud-compose-api/).
