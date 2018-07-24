---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Architecture 
{: #architecture}

## Replication

An {{site.data.keyword.composeForEtcd_full}} service contains three etcd data members in a cluster, with their disk space spread over the region's availability zones, and your data replicated across all three. In an etcd cluster each member knows about every other member and relies on a distributed consensus protocol to determine the leader. The leader broadcasts its leader status at a set interval. The followers, if nothing has been heard from the leader, all have their own interval after which they will attempt to become a leader. Should one data member become unreachable, your cluster continues to operate normally.

## Disk Encryption

All {{site.data.keyword.composeForEtcd}} services have encryption at rest. Your data resides on servers that have volume-level encryption enabled. 

Because {{site.data.keyword.composeForEtcd}} is a managed service, it is possible for {{site.data.keyword.cloud}} Compose operators to see data. In addition to the disk encryption, you should encrypt personal information before storing it in the database or use extensions or features to enable encryption on the database itself. While these methods might impact usability or performance, it is good practice to ensure that personal information is protected with encryption.

## Auto-scaling

Resources are scaled automatically based on the total memory use of the etcd databases. Storage is based on a ratio of provisioned RAM at 4:1. These resources are bundled as units.

Auto-scaling is designed to respond to the short-to-medium term trends of your database. Every minute, your service is checked and if it is running short on RAM, then more units are allocated to the deployment. 

Auto-scaling does not scale down deployments where disk/memory usage has shrunk. The resources provisioned to your databases are retained for your future needs, or until you manually scale down your deployment.
{: .tip}
