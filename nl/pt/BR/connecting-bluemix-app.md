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

# Conectando um aplicativo {{site.data.keyword.cloud_notm}}

Para conectar um aplicativo {{site.data.keyword.cloud}} a seu serviço, use as credenciais de serviço que são criadas quando o serviço é provisionado. O aplicativo de amostra demostra como usar o Node.js para se conectar a um serviço {{site.data.keyword.composeForEtcd}} usando as credenciais fornecidas e como criar um banco de dados e ler e gravar no banco de dados.

## Conectando usando o aplicativo de amostra 'Hello World'

O aplicativo de amostra [compose-etcd-helloworld-nodejs](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) demonstra como usar o Node.js para se conectar a um serviço {{site.data.keyword.composeForEtcd}} usando as credenciais fornecidas. O aplicativo cria, lê e grava em um banco de dados

Faça download do aplicativo de amostra e siga as instruções no arquivo leia-me. Em seguida, em sua página de detalhes do aplicativo no {{site.data.keyword.cloud}}, clique em **Visualizar app** para visualizar os conteúdos da tabela *exemplos*.

## Credenciais Disponíveis
{: #available-credentials}

Para conectar um app ao seu serviço, use as credenciais que são criadas com o serviço. O aplicativo de amostra [compose-etcd-helloworld-nodejs](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) demonstra como usar o Node.js para se conectar a um serviço {{site.data.keyword.composeForEtcd}} usando as credenciais.

|Campo de nome|Descrição|
|----------|-----------|
|` ca_certificate_base64 `  ` (opcional) `|Um certificado autoassinado codificado em base64 usado para confirmar se um aplicativo está se conectando ao servidor apropriado. O certificado está presente apenas em serviços que possuem um certificado autoassinado em vez de um certificado Let's Encrypt. É necessário decodificar a chave antes de poder usá-la, conforme mostrado no aplicativo de amostra.|
|`deployment_id`|Um identificador interno para o serviço conforme criado no Compose.|
|`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `etcd`.|
|`name`|O nome da implementação do banco de dados.|
|`uri`|O URI a ser usado na conexão com o serviço. `uri` inclui o esquema (`amqps:), o nome do usuário administrativo e a senha, o nome do host do servidor, o número da porta à qual se conectar e o `nome do vhost.|
|`uri_direct_1`|Um URI secundário que pode ser usado ao se conectar ao serviço. Formatado como para `uri`.|
{: caption="Tabela 1. Credenciais do Compose for etcd" caption-side="top"}

**Nota:** dois portais `haproxy` fornecem acesso ao serviço etcd. Tanto `uri` quanto `uri_direct_1` podem ser usados para a conexão. Em seus aplicativos, alterne entre `uri` e `uri_direct_1` para gerenciar respostas às falhas de conexão.
