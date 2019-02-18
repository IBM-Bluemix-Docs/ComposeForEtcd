---

copyright:
  years: 2016,2018
lastupdated: "2017-09-21"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an {{site.data.keyword.cloud_notm}} application
{: #ibmcloud-cf-app}

To connect an {{site.data.keyword.cloud}} application to your service, use the service credentials that are created when the service is provisioned. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForEtcd}} service using the provided credentials, and how to create a database and read from and write to the database.

## Using the 'Hello World' sample app

The [sample app](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForEtcd}} service using the provided credentials. The application creates, reads from, and writes to a database

Download the sample app and follow the instructions in the readme file. Then, in your application details page in {{site.data.keyword.cloud}}, click **View APP** to view the contents of the *examples* table.

## Available Credentials
{: #available-credentials}

To connect an app to your service, use the credentials that are created along with the service. The [sample app](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForEtcd}} service by using the credentials.

|Field Name|Description|
|----------|-----------|
|`ca_certificate_base64` `(optional)`|A base64 encoded, self-signed certificate that is used to confirm that an application is connecting to the appropriate server. The certificate is only present on services that have a self-signed instead of a Let's Encrypt certificate. You need to decode the key before you can use it, as shown in the sample application.|
|`deployment_id`|An internal identifier for the service as created within Compose.|
|`db_type`|The type of database that is offered by service; in this case `etcd`.|
|`name`|The database deployment name.|
|`uri`|The URI to be used when connecting to the service. The value includes the schema (`amqps:`), admin user name and password, the host name of the server, the port number to connect to, and `vhost` name.|
|`uri_direct_1`|A secondary URI that can be used when connecting to the service. Formatted as for `uri`.|
{: caption="Table 1. Compose for etcd credentials" caption-side="top"}

**Note:** Two `haproxy` portals provide access to the etcd service. Both `uri` and `uri_direct_1` can be used to connect. In your applications, switch between `uri` and `uri_direct_1` to manage responses to connection failures.
