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

# Architecture 
{: #architecture}

## Replication

An {{site.data.keyword.composeForEtcd_full}} service contains three etcd data members in a cluster. Their disk space is spread over the region's availability zones, and your data is replicated across all three data members.

In an etcd cluster, each member knows about every other member, and relies on a distributed consensus protocol to determine the leader. The leader broadcasts its leader status at a set interval. The followers all have their own interval after which they attempt to become a leader if nothing has been heard from the leader.

If one data member becomes unreachable, your cluster continues to operate normally.

## Disk Encryption

All {{site.data.keyword.composeForEtcd}} services have encryption at rest. Your data resides on servers that are enabled with volume-level encryption. 

Because {{site.data.keyword.composeForEtcd}} is a managed service, it's possible for {{site.data.keyword.cloud}} Compose operators to see data. If you're storing personal information in your database, encrypt it before you store it, or use extensions or features to enable encryption on the database itself. While these methods can impact usability or performance, it's good practice to ensure that personal information is protected with encryption.

## Auto-scaling

Resources are scaled automatically based on the total memory use of the etcd databases. Storage is based on a ratio of provisioned RAM at 4:1. These resources are bundled as units.

Auto-scaling is designed to respond to the short-to-medium term trends of your database. Every minute, your service is checked and if it is running short on RAM, then more units are allocated to the deployment. 

Auto-scaling does not scale down deployments where disk/memory usage has shrunk. The resources provisioned to your databases are retained for your future needs, or until you manually scale down your deployment.
{: tip}
