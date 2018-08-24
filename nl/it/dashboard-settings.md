---

Copyright:
  years: 2017,2018
lastupdated: "2017-10-23"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Impostazioni

Queste funzioni ti consentono di adattare il tuo servizio {{site.data.keyword.composeForEtcd_full}} per soddisfare in modo migliore i tuoi bisogni e requisiti.

## Aggiorna versione

 Se il tuo servizio è già all'ultima versione disponibile, il pannello visualizza le informazioni sulla versione corrente. Se è disponibile una nuova versione del database, viene visualizzato un menu a discesa che ti consente di selezionare una versione a cui eseguire l'upgrade.

![Il pannello della versione](./images/etcd-version-show.png "Il pannello della versione")


## Ridimensionamento delle risorse

Se il tuo servizio necessita ulteriore memoria o desideri ridurre la quantità di memoria assegnata al tuo servizio, puoi eseguire queste operazioni per ridimensionare le risorse.

1. Passa alla pagina della panoramica del dashboard del tuo servizio.
2. Nel pannello _Deployment Details_, fai clic su **Scale Resources**. Viene aperta la pagina di ridimensionamento delle risorse.
    ![La pagina di ridimensionamento delle risorse](./images/etcd-scale-show.png "La pagina di ridimensionamento delle risorse")
3. Modifica lo slider per aumentare o diminuire la memoria assegnata al servizio {{site.data.keyword.composeForEtcd}}. Sposta lo slider a sinistra per ridurre la quantità di memoria o a destra per incrementarla.
4. Fai clic su **Scale Deployment** per attivare il ridimensionamento e ritorna alla panoramica del dashboard. 

Quando il ridimensionamento è completo il pannello _Deployment Details_ si aggiorna per visualizzare l'utilizzo corrente e il nuovo valore per la memoria disponibile.


## Modifica la password

Potresti dover modificare la password del tuo servizio. Puoi eseguire tale operazione dal pannello _Change Password_. 

Puoi utilizzare la password generata casualmente che viene creata per tuo conto oppure puoi immettere una tua password nel campo. Per rigenerare una nuova password casuale, fai clic sul dado a destra del campo. 
  
![Aggiornamento della password etcd](./images/etcd-update-password.png "Generatore della password automatico")

Fai clic su **Update Password**. Ti sarà richiesto di confermare la modifica. Fai clic su **Update Password** nella finestra di dialogo per confermare la nuova password o per annullare la modifica. Il pannello _Deployment Details_ visualizza il progresso del lavoro in esecuzione.

**Nota:** modificando la password modifichi le credenziali che tu e i tuoi servizi utilizzate per il collegamento e annulla la validità della stringa di connessione del tuo servizio. Può anche causare un tempo di inattività.

### Aggiornamento delle applicazioni connesse
La modifica della password rende non valida la stringa di connessione esistente e ne genera una nuova. Questo può causare un'interruzione del servizio finché le applicazioni connesse non vengono aggiornate con la nuova stringa di connessione.

Per ulteriori informazioni sulla connessione delle tue applicazioni, vedi [Connessione di un'applicazione {{site.data.keyword.cloud}}](./connecting-bluemix-app.html).
e [Connessione di un'applicazione esterna](./connecting-external.html).


## Utilizzo delle whitelist

Se desideri limitare l'accesso ai tuoi database, puoi inserirei in una whitelist indirizzi IP specifici o intervalli di indirizzi IP del tuo servizio. Quando non sono presenti indirizzi IP nella whitelist, essa è disabilitata e la distribuzione accetterà le connessioni da tutti i sistemi in internet.

![IP della whitelist](./images/etcd-whitelist-show.png "I campi della whitelist.")

### Indirizzi IP
Il campo *IP* può avere solo un indirizzo IPv4 o IPv6 con o senza una netmask. Senza una netmask, le connessioni in entrata devono provenire esattamente da tale indirizzo IP. 

**Nota:** anche se la voce IP consente IPv6, nessuna distribuzione Compose è al momento disponibile per la rete IPv6, per cui non è possibile applicare filtri su questi indirizzi.

### Netmask
Per consentire una connessione da un intervallo specificato di indirizzi IP, utilizza una netmask. L'indirizzo IP deve essere completamente specificato quando utilizzi una netmask. Questo significa che devi immettere, ad esempio, `192.168.1.0/24` invece di `192.168.1/24`.

### Descrizione
*Description* può essere un qualsiasi testo per identificare la voce della whitelist - ad esempio, un nome del cliente, un identificativo del progetto o un numero del dipendente. Il campo della descrizione è obbligatorio.

### Servizi Compose
Le voci della whitelist vengono automaticamente aggiunte ai server di Compose per consentire loro di collegarsi.

### Rimozione degli indirizzi IP inseriti nella whitelist
Per rimuovere un indirizzo IP o una netmask dalla whitelist, fai clic su *Remove IP* nella riga corrispondente.
Quando tutte le voci nella whitelist sono state rimosse, sarà disabilitata e tutti gli indirizzi IP saranno accettati dai portali di accesso TCP.
