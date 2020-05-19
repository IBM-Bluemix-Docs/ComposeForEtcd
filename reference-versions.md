---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"

keywords: etcd, compose

subcollection: ComposeForEtcd

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Versions
{: #versions}

You can find the list of available versions on the {{site.data.keyword.composeForEtcd}} [catalog page](https://{DomainName}/catalog/compose-for-etcd) or from the [`GET /2016-07/deployments/:id/versions`](https://apidocs.compose.com/reference#2016-07-get-deployments-versions) API endpoint. 

## Preferred Version

The preferred version is typically the newest version of the etcd database that is available for {{site.data.keyword.composeForEtcd}}. It is the version that is the default in the drop-down version selector on the catalog page. It is also the version that is automatically provisioned by API if no version is specified in the call.

### New Preferred Version Protocol

When a new version is made available, its release is announced and the version is made available for deployment. After release there is an approximately 7-day window where the newest version is available, but it is not listed as the preferred version. This window allows users to deploy and test the new version, while still having the current version available to them. At the end of the 7-day window the new version is set as the preferred version, or a new date for this change is announced.

