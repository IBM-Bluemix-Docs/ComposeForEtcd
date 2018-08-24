---

copyright:
  years: 2016,2018
lastupdated: "2018-01-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Pricing
{: #pricing}

## Base Configuration

An {{site.data.keyword.composeForEtcd_full}} service starts with three etcd data members in a cluster; each member has 256 MB memory and 256 MB storage, which is equal to one unit of resources. The service _includes_ replication and high-availablity, so each unit and the price per unit _includes_ the cost of the resources across all three data members.

Two HAProxy portals - each with 64 MB memory - are also included for managing connections and high-availability.

The base service configuration has a set price. Consult the catalog tiles on {{site.data.keyword.cloud_notm}} for base pricing in your local currency. For example, the base price in US dollars is $19.50/month.

## Increasing resources

If you need extra storage or memory for your service, you can increase the resources that are allocated in a 1:1 ratio of disk storage to memory unit. Increasing the disk allocated to the deployment also increases the RAM allocated. A {{site.data.keyword.composeForEtcd}} unit consists of 256 MB of storage and 256 MB of memory, and each unit and the price per unit _includes_ the cost to increase the resources on all three data members in the cluster. 

## Calculating the cost of your deployment
{: #tiered-pricing}

Each additional unit (256 MB storage/256 MB memory) has a per-unit price, which is listed in your local currency on the {{site.data.keyword.cloud_notm}} catalog tile for the service. In US dollars, each additional unit costs $19.50. As the _total_ size of all your {{site.data.keyword.composeForEtcd}} services increases, the per unit price decreases, as shown in the tiered pricing table.

Number of Units|Price per Unit
----------|-----------
1 - 9 units|Base per unit price - $19.50 USD/Unit
10 - 24 units|10% reduction - $17.55 USD/Unit
25 - 49 units|20% reduction - $15.60 USD/Unit
50 - 99 units|30% reduction - $13.65 USD/Unit
100 - 499 units|40% reduction - $11.70 USD/Unit
500 - 999 units|50% reduction - $9.75 USD/Unit
1,000 - 4,999|60% reduction - $7.80 USD/Unit
5,000+ units|70% reduction - $5.85 USD/Unit
{: caption="Table 1. {{site.data.keyword.composeForEtcd}} tiered pricing" caption-side="top"}
