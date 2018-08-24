---
copyright:
  years: 2016,2018
lastupdated: "2018-06-11"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuração da Conexão
{: #connection-configuration}

As conexões com o banco de dados do {{site.data.keyword.composeForEtcd_full}} são gerenciadas por 2 portais HAProxy. Cada portal tem 64 MB de memória.

Os dois portais permitirão que os aplicativos mantenham a conectividade no caso de um deles se tornar inacessível. Failover no lado do cliente é responsabilidade do designer de aplicativo. Alguns drivers etcd manipulam automaticamente múltiplas sequências de conexões e failovers normais. A menos que esteja trabalhando com um driver que manipule completamente erros de failover, será necessário executar as etapas a seguir para manipular erros:

* Trabalhar com um driver que aceite múltiplos terminais em sua configuração de conexão.
* Assegure-se de que as chamadas de seu aplicativo para ler ou gravar no banco de dados reajam aos erros apropriadamente. É possível configurar seu aplicativo para reagir a erros de diferentes maneiras, incluindo o seguinte:
  - Registre o erro e reconecte-se.
  - Reconecte e tente novamente a operação que causou o erro.
  - Enfileire a operação com falha e planeje uma reconexão.

## Criptografia em Trânsito

Todos os portais HAProxy do {{site.data.keyword.composeForEtcd}} têm o TLS/SSL ativado e suportam o TLS versão 1.2. Os certificados para o serviço são certificados Let's Encrypt.

## Limites de Conexão

As conexões com o banco de dados têm um limite de 2000 conexões por portal. Exceder o limite de conexão tornará seu serviço não responsivo. É possível gerenciar conexões de seu aplicativo por meio do recurso de definição do conjunto de conexões do driver.

## Tempos limite de proxy

Os portais HAProxy gerenciam o ciclo de vida de conexões entre o servidor e o cliente. Nós as detalhamos aqui como uma referência para gravadores de driver e outros que têm interesse na atividade de baixo nível de conexões com o banco de dados do {{site.data.keyword.composeForEtcd}}.

Configurando | Value | Aplica
----------|-----------|-----------
cliente | 1 dia | Quando se espera que o cliente reconheça ou envie dados.
conectar | 1m | Quando uma conexão está sendo feita entre o proxy e o servidor.
server | 1 dia | Quando se espera que o servidor reconheça ou envie dados.
check | 1m | Como uma verificação de tempo limite secundário quando uma conexão está sendo feita entre o proxy e o servidor.
{: caption="Tabela 1. Tempos limite de HAProxy etcd" caption-side="top"}
