---

Copyright:
  Years: 2017
lastupdated: "2017-10-23"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visão geral do serviço

A página _Visão geral_ mostra informações sobre seu banco de dados do {{site.data.keyword.cloud}} Compose. A visão geral inclui informações essenciais de identificação e o uso do recurso atual. Você também localizará uma seção para sequências de conexões que podem ser usadas com ferramentas ou fazer uso de ferramentas para se conectar a seu banco de dados.

## Detalhes da implementação

O painel _Detalhes da implementação_ mostra detalhes de seu serviço.

![Deployment Details](./images/etcd-deployment-details.png "A view of the Deployment Details panel")

### Tipo

O tipo de banco de dados que é oferecido pelo serviço e a versão do banco de dados que seu serviço usa.

### Nome

Um identificador interno para o serviço.

### Uso

O tamanho de seu banco de dados e a quantia de armazenamento fornecido por seu plano de serviço.


## Sequências de conexões

As Sequências de conexões podem ser usadas por algumas bibliotecas do cliente e contêm todas as informações necessárias para outras bibliotecas se conectarem. É possível descobrir como usar uma Sequência de conexões para se conectar ao {{site.data.keyword.composeForEtcd_full}} em [Conectando um aplicativo externo](./connecting-external.html).

Você localizará cada Sequência de conexões para seu serviço em uma guia diferente no painel _Sequências de conexões_.

### HTTPS

A sequência de conexões **HTTPS** pode ser usada por algumas bibliotecas do cliente e contém todas as informações necessárias para outras bibliotecas se conectarem. É possível descobrir como usar a sequência de conexões para se conectar em [Conectando um aplicativo externo](./connecting-external.html).

### Linha de comandos

A **Linha de comandos** é um comando pré-formatado que chamará `etcd` com os parâmetros corretos. Para usá-la, você precisará ter as ferramentas do cliente etcd instaladas no sistema local. É possível descobrir mais sobre como fazer isso em [Conectando um aplicativo externo](./connecting-external.html).

### Certificado SSL

Seu serviço Compose {{site.data.keyword.cloud}} fornece um certificado SSL que é possível usar para conectar-se a seu banco de dados.
