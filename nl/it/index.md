---

copyright:
  years: 2016,2018
lastupdated: "2018-03-26"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni su {{site.data.keyword.composeForEtcd}}
{: #about-compose-for-etcd}

etcd è un archivio di valore-chiave che ospita i dati sempre corretti di cui hai bisogno per coordinare e gestire il tuo cluster server per la gestione della configurazione del server distribuito. etcd utilizza l'algoritmo coseno RAFT per assicurare la consistenza dei dati nel tuo cluster. Forza l'ordine in cui vengono eseguite le operazioni sui dati in modo che ogni nodo nel cluster arrivi allo stesso risultato con la stessa modalità. {{site.data.keyword.composeForEtcd_full}} aggiunge backup automatici dei tuoi dati di configurazione archiviati in etcd. Un'interfaccia di amministrazione intuitiva che ti permette di monitorare, ridimensionare e gestire la tua distribuzione con facilità.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account {{site.data.keyword.cloud}}.

## Creazione di una istanza del servizio {{site.data.keyword.composeForEtcd}}

Puoi creare un servizio {{site.data.keyword.composeForEtcd}} dalla pagina [{{site.data.keyword.composeForEtcd}}](https://console.{DomainName}/catalog/services/compose-for-etcd/) nel catalogo {{site.data.keyword.cloud_notm}}.

Scegli un nome del servizio, una regione, un'organizzazione e uno spazio in cui eseguire il provisioning del servizio. Puoi utilizzare il campo **Select a database version** per scegliere tra le versioni del database disponibili.

Quando esegui il provisioning della tua istanza {{site.data.keyword.composeForEtcd}} puoi scegliere i piani *Standard* o *Enterprise*. Con il piano *Enterprise*, puoi eseguire il provisioning della tua istanza {{site.data.keyword.composeForEtcd}} in un cluster {{site.data.keyword.composeEnterprise}} disponibile. {{site.data.keyword.composeEnterprise}} fornisce la sicurezza e l'isolamento necessari per la conformità aziendale e utilizza la rete dedicata per garantire le prestazioni dei database distribuiti. Per ulteriori dettagli, consulta la [Documentazione aziendale Compose](../ComposeEnterprise/index.html).

## Gestione di {{site.data.keyword.composeForEtcd}}

Puoi gestire il tuo servizio dal dashboard del servizio. Qui puoi trovare le informazioni sul tuo database {{site.data.keyword.cloud_notm}} Compose e su come collegarti ad esso. Puoi anche:
- gestire i tuoi backup
- assegnare ulteriori risorse al tuo servizio
- modificare la password del servizio
- utilizzare le whitelist per limitare l'accesso ai tuoi database 

Per ulteriori informazioni, consulta [Impostazioni](./dashboard-settings.html).

{{site.data.keyword.composeForEtcd}} si basa sui ruoli Cloud Foundry per gestire l'accesso al servizio. Solo gli utenti con il ruolo di sviluppatore possono visualizzare o utilizzare il dashboard del servizio. Per ulteriori informazioni sui ruoli Cloud Foundry, consulta le pagine [Cloud Foundry access](https://console.bluemix.net/docs/iam/cfaccess.html#cfaccess) e [Managing Cloud Foundry access](https://console.bluemix.net/docs/iam/mngcf.html#mngcf).
{: .tip}

## Connessione a {{site.data.keyword.composeForEtcd}}

Puoi collegarti al tuo servizio utilizzando le credenziali create insieme al servizio o con le stringhe di connessione e la riga di comando forniti nella scheda *Overview* nel tuo dashboard del servizio.

## Connessione di un'applicazione {{site.data.keyword.cloud_notm}} a {{site.data.keyword.composeForEtcd}}

Per collegare un'applicazione {{site.data.keyword.cloud_notm}} al tuo servizio, utilizza le credenziali create insieme al servizio. Puoi trovare le informazioni su come collegare un'applicazione {{site.data.keyword.cloud_notm}} a un servizio {{site.data.keyword.composeForEtcd}} in [Connessione a un'applicazione {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Connessione a {{site.data.keyword.composeForEtcd}} dall'esterno di {{site.data.keyword.cloud_notm}}

Se desideri collegarti a {{site.data.keyword.composeForEtcd}} dall'esterno di {{site.data.keyword.cloud_notm}}, puoi utilizzare la riga di comando o le stringhe di connessione fornite. Puoi trovare le informazioni su come collegarti in [Connessione a un'applicazione esterna](./connecting-external.html).
