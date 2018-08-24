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

# Configurazione della connessione
{: #connection-configuration}

Le connessioni al database {{site.data.keyword.composeForEtcd_full}} sono gestite da 2 portali HAProxy. Ciascun portale ha 64 MB di memoria.

I due portali consentono alle applicazioni di mantenere la connettività nel caso in cui uno dei portali diventi irraggiungibile. Il failover al lato client è responsabilità del progettista dell'applicazione. Alcuni driver etcd gestiscono più stringhe di connessione e il failover normale in modo automatico. A meno che tu non stia lavorando con un driver che gestisce completamente gli errori di failover, devi attenerti alla seguente procedura per gestire gli errori:

* Lavorare con un driver che accetta più endpoint nella sua configurazione della connessione.
* Assicurarti che le chiamate della tua applicazione per leggere o scrivere nel database reagiscano in modo appropriato agli errori. Puoi configurare la tua applicazione in modo che reagisca agli errori in modi diversi, inclusi i seguenti:
  - Registra l'errore e ristabilisci la connessione.
  - Ristabilisci la connessione e ritenta l'operazione che ha causato l'errore.
  - Accoda l'operazione non riuscita e pianifica una riconnessione.

## Crittografia in transito

Tutti i portali HAProxy {{site.data.keyword.composeForEtcd}} hanno TLS/SSL abilitati e supportano TLS versione 1.2. I certificati per il servizio sono certificati di Let's Encrypt.

## Limiti di connessioni

Le connessioni al database hanno un limite di connessioni di 2000 connessioni per portale. Se si supera il limite di connessioni, il tuo servizio smetterà di rispondere. Puoi gestire le connessioni dalla tua applicazione tramite la funzione di pooling di connessioni del tuo driver.

## Timeout proxy

I portali HAProxy gestiscono il ciclo di vita delle connessioni tra il server e il client. Li descriviamo qui in dettaglio come guida di riferimento per gli scrittori di driver e per gli altri che hanno un interesse nell'attività di basso livello delle connessioni al database {{site.data.keyword.composeForEtcd}}.

Impostazione | Valore | Si applica
----------|-----------|-----------
client | 1 giorno | Quando si prevede che il client riconosca o invii i dati.
connect | 1m | Quando si sta stabilendo una connessione tra il proxy e il server.
server | 1 giorno | Quando si prevede che il server riconosca o invii i dati.
check | 1m | Come un controllo di timeout secondario quando si sta stabilendo una connessione tra il proxy e il server.
{: caption="Tabella 1. Timeout HAProxy etcd" caption-side="top"}
