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

# Panoramica sul servizio

La pagina _Overview_ ti mostra le informazioni sul tuo database {{site.data.keyword.cloud}} Compose. La panoramica include le informazioni di identificazione essenziali e l'utilizzo della risorsa corrente. Troverai inoltre una sezione per le stringhe di connessione che puoi utilizzare con gli strumenti o utilizzare gli strumenti per il collegamento al tuo database.

## Dettagli della distribuzione

Il pannello _Deployment Details_ mostra i dettagli del tuo servizio.

![Dettagli della distribuzione](./images/etcd-deployment-details.png "Una vista del pannello dei dettagli della distribuzione")

### Tipo

Il tipo di database offerto dal servizio e la versione che il servizio utilizza.

### Nome

Un identificativo interno per il servizio.

### Utilizzo

La dimensione del tuo database e la quantità di memoria fornita dal tuo piano di servizio.


## Stringhe di connessione

Le stringhe di connessione possono essere utilizzate da alcune librerie client e contenere tutte le informazioni necessarie al collegamento di altre librerie. Puoi trovare come utilizzare una stringa di connessione a {{site.data.keyword.composeForEtcd_full}} in [Connessione a un'applicazione esterna](./connecting-external.html).

Troverai ogni stringa di connessione per il tuo servizio in una scheda differente nel pannello _Connection Strings_.

### HTTPS

La stringa di connessione **HTTPS** può essere utilizzata da alcune librerie client e contiene tutte le informazioni necessarie al collegamento di altre librerie. Puoi trovare come utilizzare la stringa di connessione per il collegamento in [Connessione a un'applicazione esterna](./connecting-external.html). 

### Riga di comando

La **Riga di comando** è un comando pre-formattato che richiamerà `etcd` con i parametri corretti. Per utilizzarla, dovrai aver installato gli strumenti client etcd nel sistema locale. Puoi trovare ulteriori informazioni su come farlo in [Connessione a un'applicazione esterna](./connecting-external.html).

### Certificato SSL

Il tuo servizio Compose {{site.data.keyword.cloud}} ti fornisce un certificato SSL che puoi utilizzare per collegarti al tuo database.
