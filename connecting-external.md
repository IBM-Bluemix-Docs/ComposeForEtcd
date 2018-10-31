---

copyright:
  years: 2017,2018
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an external application
{: #connecting-external-app}

You can find the information that you need to connect to {{site.data.keyword.composeForEtcd_full}} on the *Overview* page of your deployment, in the _Connection Strings_ section. {{site.data.keyword.composeForEtcd}} deployments accept TLS/SSL secured connections that are backed with a Let's Encrypt certificate.

## Connecting with etcdctl

`etcdctl` is the command-line client for etcd and can be used to manage your etcd. It is installed with a local installation of the etcd package.

The _Connection Strings_ panel has a _Command Line_ tab with a formatted `etcdctl` command to connect to your deployment. 

```shell
ETCDCTL_API=3 etcdctl --endpoints=https://portal-ssl8-39.bmix-dal-yp-29efe85a-ebc4-45c9-96b0-2f7dc246478d.1556490063.composedb.com:62697,https://portal-ssl4-40.bmix-dal-yp-29efe85a-ebc4-45c9-96b0-2f7dc246478d.1556490063.composedb.com:62697 --user=root:<password> member list -w table
```
You have to specify the version of the API to use by setting the environment with `ETCDCTL_API=3`. The `--endpoints` parameter accepts the addresses of the two HAProxy portals, and the `--user` parameter is the root user and its password. The `member list -w table` is the command to display all the data members of your etcd cluster in a table format.

An `etcdctl` command reference is available on the [GitHub page](https://github.com/etcd-io/etcd/tree/master/etcdctl).

## Connecting with a language's driver

etcd drivers are often able to make a connection to your deployment when given the URI-formatted connection string found in the _HTTPS_ tab of the _Connection Stings_ panel. For example, 
```
https://root:<password>@portal-ssl8-39.bmix-dal-yp-29efe85a-ebc4-45c9-96b0-2f7dc246478d.1556490063.composedb.com:62697
```

The table covers a few of the etcd drivers in various languages.

Language|Driver|Documentation
----------|-----------
Node|`etcd3`|[Link](https://mixer.github.io/etcd3/classes/index_.etcd3.html)
Java|`jetcd`|[Link](https://github.com/etcd-io/jetcd)
Java|`etcd-java`|[Link](https://github.com/IBM/etcd-java)
Go|`etcd/client`|[Link](https://github.com/etcd-io/etcd/tree/master/client)
{: caption="Table 2. Common etcd drivers" caption-side="top"}

