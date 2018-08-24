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

# Sicherungen
{: #backups}

Sie können Sicherungen erstellen und über die Registerkarte _Sicherungen_ der Seite _Verwalten_ Ihres Service-Dashboards herunterladen. Dabei sind tägliche, wöchentliche und monatliche Sicherungen sowie Sicherungen nach Bedarf verfügbar. Die Aufbewahrungszeit richtet sich nach folgendem Zeitplan:

Sicherungstyp|Aufbewahrungszeitplan
----------|-----------
Täglich|Tägliche Sicherungen werden 7 Tage aufbewahrt
Wöchentlich|Wöchentliche Sicherungen werden 4 Wochen aufbewahrt
Monatlich|Monatliche Sicherungen werden 3 Monate aufbewahrt
Bei Bedarf|Es wird eine bei Bedarf erstellte Sicherung aufbewahrt. Dabei ist die aufbewahrte Sicherung immer die letzte bei Bedarf erstellte Sicherung.
{: caption="Tabelle 1. Aufbewahrungszeitplan für Sicherungen" caption-side="top"}

Sicherungszeitpläne und Aufbewahrungsrichtlinien sind festgelegt. Falls Sie mehr Sicherungen benötigen als die, die im Aufbewahrungszeitplan vorgesehen sind, laden Sie Sicherungen herunter und bewahren Sie Sicherungsarchive gemäß Ihren Geschäftsanforderungen auf.

## Vorhandene Sicherungen anzeigen

Tägliche Sicherungen Ihrer Datenbank werden automatisch geplant. Gehen Sie wie folgt vor, um Ihre vorhandenen Sicherungen anzuzeigen:

1. Navigieren Sie zu der Seite _Verwalten_ Ihres Service-Dashboards.
2. Klicken Sie auf die Registerkarte **Sicherungen**, um die Seite _Sicherungen_ zu öffnen. Es wird eine Liste der verfügbaren Sicherungen angezeigt:

  ![Verfügbare Sicherungen](./images/etcd-backups-show.png "Liste der verfügbaren Sicherungen.")

Klicken Sie auf eine Zeile, um die Optionen für die entsprechende verfügbare Sicherung zu erweitern.

  ![Sicherungsoptionen](./images/etcd-backups-options.png "Optionen für eine Sicherung.") 

### API verwenden, um vorhandene Backups anzuzeigen

Eine Liste der Backups steht am Endpunkt `GET /2016-07/deployments/:id/backups` zur Verfügung. Die Basisendpunkte mit der Serviceinstanz-ID und der Bereitstellungs-ID werden beide in der _Übersicht_ des Service angezeigt.

``` 
https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
```  

## Manuelle Sicherung erstellen

Neben geplanten Sicherungen können Sie manuelle Sicherungen erstellen. Führen Sie zum Erstellen einer manuellen Sicherung die Schritte zum Anzeigen der vorhandenen Sicherungen aus. Klicken Sie dann über der Liste der vorhandenen Sicherungen auf **Jetzt sichern**. Es wird eine Nachricht darüber angezeigt, dass eine Sicherung eingeleitet wurde, und zur Liste der verfügbaren Sicherungen wird eine 'anstehende' Sicherung hinzugefügt.

### API verwenden, um eine Sicherung zu erstellen

Senden Sie eine POST-Anforderung an den Endpunkt der Sicherung, um eine manuelle Sicherung zu initialisieren: `POST /2016-07/deployments/:id/backups`. Daraufhin wird sofort die Anleitungs-ID mit Informationen zur aktiven Sicherung zurückgegeben. Sie müssen den Endpunkt der Sicherung überprüfen, um festzustellen, ob die Sicherung fertiggestellt wurde und um die zugehörige Sicherungs-ID (backup_id) zu suchen, bevor Sie sie verwenden können. Verwenden Sie `GET /2016-07/deployments/:id/backups/`.

## Sicherung herunterladen

Führen Sie zum Herunterladen einer Sicherung die Schritte zum Anzeigen der vorhandenen Sicherungen aus. Klicken Sie dann auf die entsprechende Zeile, um die Optionen für die Sicherung zu erweitern, die Sie herunterladen wollen, und klicken Sie auf **Herunterladen**. Die komprimierte Datei enthält einen binären Snapshot Ihrer Daten zur lokalen Verwendung.

### API verwenden, um eine Sicherung herunterzuladen

Suchen Sie auf der Seite _Sicherungen_ für Ihren Service die Sicherung aus, die Sie wiederherstellen wollen, und kopieren Sie die Angabe für `backup_id` oder verwenden Sie `GET /2016-07/deployments/:id/backups`, um eine Sicherung und die zugehörige Sicherungs-ID über die Compose-API zu suchen. Verwenden Sie dann den Wert für `backup_id`, um Informationen zu einer bestimmten Sicherung zu erhalten sowie einen entsprechenden Download-Link zu finden: `GET /2016-07/deployments/:id/backups/:backup_id`.

## Sicherung wiederherstellen

Führen Sie zum Wiederherstellen einer Sicherung auf einer neuen Serviceinstanz die Schritte zum Anzeigen der vorhandenen Sicherungen aus. Klicken Sie dann auf die entsprechende Zeile, um die Optionen für die Sicherung zu erweitern, die Sie herunterladen wollen, und klicken Sie auf **Wiederherstellen**. Es wird eine Nachricht darüber angezeigt, dass eine Wiederherstellung eingeleitet wurde. Die neu erstellte Serviceinstanz erhält automatisch den Namen "etcd-restore-[timestamp]" und wird beim Start der Bereitstellung in Ihrem Dashboard angezeigt.

### Wiederherstellung über die {{site.data.keyword.cloud_notm}}-CLI

Führen Sie die folgenden Schritte aus, um eine Sicherung aus einem aktiven etcd-Service mithilfe der {{site.data.keyword.cloud_notm}}-CLI in einem neuen etcd-Service wiederherzustellen. 

1. Bei Bedarf können Sie die [CLI herunterladen und installieren](https://console.{DomainName}/docs/cli/index.html#overview). 

2. Suchen Sie auf der Seite _Sicherungen_ in Ihrem Service die Sicherung aus, die für die Wiederherstellung verwendet werden soll, und kopieren Sie die Sicherungs-ID.

  **ODER**  
  Verwenden Sie `GET /2016-07/deployments/:id/backups`, um eine Sicherung und die zugehörige ID über die Compose-API zu suchen. Der Basisendpunkt und die Serviceinstanz-ID werden beide in der _Übersicht_ des Service angezeigt. Beispiel: 
  ``` 
  https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
  ```  
  Die Antwort beinhaltet eine Liste aller verfügbaren Sicherungen für diese Serviceinstanz. Wählen Sie die Sicherung aus, die für die Wiederherstellung verwendet werden soll, und kopieren Sie die zugehörige ID.

3. Melden Sie sich mit dem entsprechenden Konto und den zugehörigen Berechtigungsnachweisen an. Verwenden Sie hierfür den Befehl `ibmcloud login` (oder `ibmcloud login -help`, damit alle Anmeldeoptionen angezeigt werden).

4. Wechseln Sie mit `ibmcloud target -o "$YOUR_ORG" -s "YOUR_SPACE"` zu Ihrer Organisation und Ihrem Bereich.

5. Verwenden Sie den Befehl `service create`, um einen neuen Bereich bereitzustellen. Geben Sie in einem JSON-Objekt den Quellenservice und die spezifische Sicherung an, die Sie wiederherstellen. Beispiel:

  ``` 
  ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": "$BACKUP_ID" }'
  ```

  - Geben Sie für _SERVICE_ die Angabe `compose-for-etcd` ein.
  - Geben Sie für _PLAN_ abhängig von Ihrer Umgebung entweder 'Standard' oder 'Enterprise' an.
  - _SERVICE\_INSTANCE\_NAME_ ist der Name Ihres neuen Service.
  - Geben Sie für _source\_service\_instance\_id_ die Serviceinstanz-ID der Quelle der Sicherung ein. Diese können Sie durch Ausführen von `ibmcloud cf service DISPLAY_NAME --guid` abrufen, wobei _DISPLAY\_NAME_ der Name des etcd-Service ist, von dem die Sicherung stammt. 
  
  Enterprise-Benutzer müssen ferner mit dem Parameter `"cluster_id": "$CLUSTER_ID"` im JSON-Objekt angeben, auf welchem Cluster die Bereitstellung erfolgen soll.
  
### Migration auf eine neue Version

Einige Upgrades der übergeordneten Version sind in der aktuell ausgeführten Bereitstellung nicht verfügbar. Sie müssen einen neuen Service bereitstellen, auf dem die per Upgrade aktualisierte Version ausgeführt wird, und anschließend Ihre Daten mithilfe einer Sicherung in diesen neuen Service migrieren. Dieser Prozess entspricht der Wiederherstellung einer Sicherung, jedoch mit dem Unterschied, dass Sie die Version angeben, auf die Sie das Upgrade durchführen möchten.

``` 
ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": ""$BACKUP_ID", "db_version":"$VERSION_NUMBER" }'
```

Verwenden Sie zum Wiederherstellen einer älteren Version eines {{site.data.keyword.composeForEtcd}}-Service auf einem neuen Service, auf dem etcd 3.2.13 ausgeführt wird, den folgenden Befehl:

```
ibmcloud service create compose-for-etcd Standard migrated_etcd -c '{ "source_service_instance_id": "0269e284-dcac-4618-89a7-f79e3f1cea6a", "backup_id":"5a96d8a7e16c090018884566", "db_version":"3.2.13"  }'
```

