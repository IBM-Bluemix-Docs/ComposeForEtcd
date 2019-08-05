---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"

keywords: etcd, compose

subcollection: compose-for-etcd

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Versions
{: #versions}

Deployable Versions | Preferred Version
----------|-----------
3.2.18, 3.3.3 | 3.2.18, 3.3.3
{: caption="Table 1. {{site.data.keyword.composeForEtcd}} versions" caption-side="top"}

You can find the list of available versions on the {{site.data.keyword.composeForEtcd}} [catalog page](https://{DomainName}/catalog/services/compose-for-etcd).

## Preferred Version

The preferred version is typically the newest version of the etcd database that is available for {{site.data.keyword.composeForEtcd}}. It is the version that is the default in the drop-down version selector on the catalog page. It is also the version that is automatically provisioned by API if no version is specified in the call.

### New Preferred Version Protocol

When a new version is made available, its release is announced and the version is made available for deployment. After release there is an approximately 7-day window where the newest version is available, but it is not listed as the preferred version. This window allows users to deploy and test the new version, while still having the current version available to them. At the end of the 7-day window the new version is set as the preferred version, or a new date for this change is announced.

The list of versions available for provisions is on the {{site.data.keyword.composeForEtcd}} [catalog page](https://{DomainName}/catalog/services/compose-for-etcd).

To get a current list of available versions for your {{site.data.keyword.composeForEtcd}} service, you can use the 
`GET /2016-07/deployments/:id/versions` endpoint. For more information, see the [API documentation](https://apidocs.compose.com/v1.0/reference#2016-07-get-deployments-versions)

