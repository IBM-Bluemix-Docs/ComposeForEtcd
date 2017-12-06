---

copyright:
  years: 2016,2017
lastupdated: "2017-09-21"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 连接 {{site.data.keyword.cloud_notm}} 应用程序

要将 {{site.data.keyword.cloud}} 应用程序连接到服务，请使用供应服务时所创建的服务凭证。样本应用程序演示如何使用 Node.js，通过提供的凭证连接到 {{site.data.keyword.composeForEtcd}} 服务，以及如何创建数据库以及如何对数据库进行读取和写入操作。

## 使用“Hello World”样本应用程序进行连接

[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) 样本应用程序演示如何使用 Node.js，通过提供的凭证连接到 {{site.data.keyword.composeForEtcd}} 服务。应用程序创建、读取和写入数据库

下载样本应用程序，并遵循自述文件中的指示信息。然后，在 {{site.data.keyword.cloud}} 中的应用程序详细信息页面中，单击**查看应用程序**，以查看*示例*表的内容。

## 可用凭证
{: #available-credentials}

要将应用程序连接到服务，请使用随服务一起创建的凭证。[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) 样本应用程序会示范如何使用 Node.js 连接到使用凭证的 {{site.data.keyword.composeForEtcd}} 服务。

|字段名称|描述|
|----------|-----------|
|`ca_certificate_base64`|自签名证书，用于确认应用程序连接到相应的服务器。证书是 Base64 编码。您必须先解码密钥，才能对其进行使用，如样本应用程序中所示。|
|`deployment_id`|在 Compose 内创建的服务的内部标识。|
|`db_type`|服务所提供的数据库类型；在本例中为 `etcd`。|
|`name`|数据库部署名称。|
|`uri`|连接到服务时要使用的 URI。`uri` 包括模式 (`amqps:)、管理用户名和密码、服务器的主机名、要连接到的端口号和 `vhost` 名称。|
{: caption="表 1. Compose for etcd 凭证" caption-side="top"}
