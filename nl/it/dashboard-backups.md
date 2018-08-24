---

copyright:
  years: 2017,2018
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Backup
{: #backups}

Puoi creare e scaricare i backup dalla scheda _Backups_ della pagina _Manage_ del tuo dashboard del servizio. Sono disponibili backup giornalieri, settimanali, mensili e su richiesta. Vengono conservati in base alla seguente pianificazione:

Tipo di backup|Pianificazione conservazione
----------|-----------
Giornaliero|I backup giornalieri sono conservati per 7 giorni
Settimanale|I backup settimanali sono conservati per 4 settimane
Mensile|I backup mensili sono conservati per 3 mesi
Su richiesta|Il backup su richiesta viene conservato. Il backup conservato è sempre il più recente backup su richiesta.
{: caption="Tabella 1. Pianificazione conservazione backup" caption-side="top"}

Le politiche di conservazione e di pianificazione del backup sono fissate. Se hai bisogno di conservare più backup rispetto a quelli consentiti dalla pianificazione di conservazione, scarica i backup e conserva gli archivi in base ai tuoi requisiti di business.

## Visualizzazione dei backup esistenti

I backup giornalieri del tuo database vengono automaticamente pianificati. Per visualizzare i tuoi backup esistenti:

1. Passa alla pagina _Manage_ del tuo dashboard del servizio.
2. Fai clic su **Backups** nelle schede per aprire la pagina _Backups_. Viene visualizzato un elenco di backup disponibili:

  ![Backup disponibili](./images/etcd-backups-show.png "Un elenco di backup disponibili.")

Fai clic sulla riga corrispondente per espandere le opzioni per ogni backup disponibile.

  ![Opzioni backup](./images/etcd-backups-options.png "Opzioni per il backup.") 

### Utilizzo dell'API per visualizzare i backup esistenti

Un elenco dei backup è disponibile nell'endpoint `GET /2016-07/deployments/:id/backups`. L'endpoint fondazione con l'ID istanza di servizio e l'ID distribuzione sono entrambi visualizzati nella _Panoramica_ del servizio.

``` 
https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
```  

## Creazione di un backup manuale

Come per i backup pianificati puoi creare un backup manualmente. Per creare un backup manuale, segui le istruzioni per visualizzare i backup esistenti, quindi fai clic su **Back up now** sopra l'elenco dei backup disponibili. Viene visualizzato un messaggio per farti sapere che è stato avviato un backup ed è stato aggiunto un backup 'in sospeso' all'elenco dei backup disponibili.

### Utilizzo dell'API per creare un backup

Invia una richiesta POST all'endpoint di backup per avviare un backup manuale: `POST /2016-07/deployments/:id/backups`. Restituisce immediatamente l'ID ricetta e le informazioni sul backup mentre è in esecuzione. Dovrai controllare l'endpoint dei backup per vedere se il backup è terminato e trovare il relativo backup_id prima di utilizzarlo. Utilizza `GET /2016-07/deployments/:id/backups/`.

## Scaricamento di un backup

Per scaricare un backup, segui le istruzioni per visualizzare i backup esistenti, quindi fai clic sulla riga corrispondente per espandere le opzioni del backup che desideri scaricare e fai clic su **Download**. Il file compresso contiene un'istantanea binaria dei tuoi dati da utilizzare localmente.

### Utilizzo dell'API per scaricare un backup

Trova il backup da cui vuoi eseguire il ripristino nella pagina _Backups_ del tuo servizio e copia il backup_id oppure utilizza il `GET /2016-07/deployments/:id/backups` per trovare un backup e il relativo `backup_id` tramite l'API Compose. Utilizza quindi il `backup_id` per trovare le informazioni e un link di download per uno specifico backup: `GET /2016-07/deployments/:id/backups/:backup_id`.

## Ripristino di un backup

Per ripristinare un backup in una nuova istanza del servizio, segui le istruzioni per visualizzare i backup esistenti, quindi fai clic sulla riga corrispondente per espandere le opzioni del backup che desideri scaricare e fai clic su **Restore**. Viene visualizzato un messaggio per farti sapere che è stato avviato un ripristino. La nuova istanza del servizio che viene creata è automaticamente denominata 'etcd-restore-[timestamp]' e visualizzata nel tuo dashboard quando viene avviato il provisioning.

### Ripristino tramite la CLI {{site.data.keyword.cloud_notm}}

Utilizza la seguente procedura per ripristinare un backup da un servizio etcd in esecuzione a un nuovo servizio etcd utilizzando la CLI {{site.data.keyword.cloud_notm}}. 

1. Se ne hai bisogno, [scarica e installa la CLI](https://console.{DomainName}/docs/cli/index.html#overview). 

2. Trova il backup da cui vuoi eseguire il ripristino nella pagina _Backups_ del tuo servizio e copia l'ID backup.

  **In alternativa**  
  Usa `GET /2016-07/deployments/:id/backups` per trovare un backup e il suo ID tramite la API Compose. L'endpoint fondazione e l'ID istanza di servizio sono entrambi visualizzati nella _Panoramica_ del servizio. Ad esempio: 
  ``` 
  https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
  ```  
  La risposta contiene un elenco di tutti i backup disponibili per tale istanza del servizio. Scegli il backup da cui vuoi eseguire il ripristino e copiane l'ID.

3. Esegui l'accesso con l'account e le credenziali appropriati. `ibmcloud login` (oppure `ibmcloud login -help` per visualizzare tutte le opzioni di accesso).

4. Passa alla tua organizzazione e al tuo spazio: `ibmcloud target -o "$YOUR_ORG" -s "YOUR_SPACE"`

5. Usa il comando `service create` per eseguire il provisioning di un nuovo servizio. Fornisci il servizio di origine e il backup specifico che stai ripristinando in un oggetto JSON. Ad esempio:

  ``` 
  ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": "$BACKUP_ID" }'
  ```

  - Per _SERVICE_, immetti `compose-for-etcd`
  - _PLAN_ può essere Standard o Enterprise, a seconda del tuo ambiente.
  - _SERVICE\_INSTANCE\_NAME_ è il nome del tuo nuovo servizio.
  - Per _source\_service\_instance\_id_, immetti l'ID istanza del servizio dell'origine del backup; puoi ottenere questo valore eseguendo `ibmcloud cf service DISPLAY_NAME --guid` dove _DISPLAY\_NAME_ è il nome del servizio etcd da cui proviene il backup. 
  
  Gli utenti Enterprise devono anche utilizzare il parametro `"cluster_id": "$CLUSTER_ID"` nell'oggetto JSON per specificare in quale cluster eseguire la distribuzione.
  
### Migrazione a una nuova versione

Alcuni upgrade di versione principale non sono disponibili nella distribuzione in esecuzione attuale. Devi eseguire il provisioning di un nuovo servizio che sta eseguendo la versione di cui è stato eseguito l'upgrade e migrare quindi in essa i tuoi dati utilizzando un backup. Questo processo è lo stesso di un ripristino di un backup, con la differenza che specifichi la versione alla quale desideri eseguire l'upgrade.

``` 
ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": ""$BACKUP_ID", "db_version":"$VERSION_NUMBER" }'
```

Ad esempio, per ripristinare una versione meno recente di un servizio {{site.data.keyword.composeForEtcd}} a un nuovo servizio che esegue etcd 3.2.13, utilizza questo comando:

```
ibmcloud service create compose-for-etcd Standard migrated_etcd -c '{ "source_service_instance_id": "0269e284-dcac-4618-89a7-f79e3f1cea6a", "backup_id":"5a96d8a7e16c090018884566", "db_version":"3.2.13"  }'
```

