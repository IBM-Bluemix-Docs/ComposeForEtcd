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

# Versões
{: #versions}

Versões Implementáveis | Versão Preferencial
----------|-----------
3.2.18. 3.3.3 | 3.2.18, 3.3.3
{: caption="Tabela 1. Versões do {{site.data.keyword.composeForEtcd}}" caption-side="top"}

## Versão Preferencial

A versão preferencial é geralmente a mais recente do banco de dados etcd que está disponível para o {{site.data.keyword.composeForEtcd}}. É a versão que é o padrão no seletor de versão suspensa na página do catálogo. Também é a versão que será provisionada automaticamente pela API se nenhuma versão for especificada na chamada.

### Novo Protocolo de Versão Preferencial

Quando uma nova versão é disponibilizada, sua liberação é anunciada e ela é disponibilizada para implementação. Após a liberação, há uma janela de aproximadamente 7 dias na qual a versão mais recente fica disponível, mas não é listada como a versão preferencial. Essa janela permite que os usuários implementem e testem a nova versão, enquanto ainda têm a versão atual disponível para eles. Também permite que os engenheiros do Compose localizem e corrijam quaisquer problemas que surjam na nova versão. No final da janela de 7 dias, a nova versão é configurada como a versão preferencial ou uma nova data para essa mudança é anunciada.

A lista de versões disponíveis para provisões está na [página de catálogo](https://console.{DomainName}/catalog/services/compose-for-etcd) do {{site.data.keyword.composeForEtcd}}.

Para obter uma lista atual de versões disponíveis para o serviço {{site.data.keyword.composeForEtcd}}, é possível usar o terminal [GET /2016-07/deployments/:id/versions](https://apidocs.compose.com/v1.0/reference#2016-07-get-deployments-versions).
