---

copyright:
  years: 2016,2018
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informationen zu {{site.data.keyword.composeForEtcd}}
{: #about-compose-for-etcd}

"etcd" ist ein Schlüssel/Wert-Speicher mit den immer korrekten Daten, die Sie zum Koordinieren und Verwalten Ihres Server-Clusters für die Konfigurationsverwaltung für verteilte Server benötigen. "etcd" verwendet den RAFT-Datenkonsistenzalgorithmus zur Sicherstellung der Konsistenz in Ihrem Cluster. Er erzwingt die Reihenfolge der Operationen an den Daten, sodass jeder Knoten im Cluster auf demselben Weg zum selben Ergebnis kommt. {{site.data.keyword.composeForEtcd_full}} fügt automatische Sicherungen Ihrer Konfigurationsdaten durch, die in "etcd" gespeichert sind. Über eine intuitive Verwaltungsschnittstelle können Sie Ihre Bereitstellung mit Leichtigkeit überwachen, skalieren und verwalten.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr {{site.data.keyword.cloud}}-Konto zugänglich und kann dort verwendet werden.

## {{site.data.keyword.composeForEtcd}}-Serviceinstanz erstellen

Sie können einen {{site.data.keyword.composeForEtcd}}-Service über die [{{site.data.keyword.composeForEtcd}}-Seite](https://console.{DomainName}/catalog/services/compose-for-etcd/) im {{site.data.keyword.cloud_notm}}-Katalog erstellen.

Wählen Sie einen Servicenamen und eine Region, eine Organisation und einen Bereich zur Bereitstellung des Service aus. Im Feld **Datenbankversion auswählen** können Sie eine der verfügbaren Datenbankversionen auswählen.

Bei der Bereitstellung Ihrer {{site.data.keyword.composeForEtcd}}-Instanz können Sie den Plan *Standard* oder *Enterprise* auswählen. Mit dem Plan *Enterprise* können Sie Ihre {{site.data.keyword.composeForEtcd}}-Instanz in einem {{site.data.keyword.composeEnterprise}}-Cluster bereitstellen. {{site.data.keyword.composeEnterprise}} stellt die für die Konformität mit Enterprise erforderliche Sicherheit und Isolation bereit und stellt mithilfe eines dedizierten Netzbetriebs die Leistung der bereitgestellten Datenbanken sicher. Weitere Details finden Sie in der [Dokumentation zu Compose Enterprise](../ComposeEnterprise/index.html).

## {{site.data.keyword.composeForEtcd}} verwalten

Sie können Ihren Service über das Service-Dashboard verwalten. Hier finden Sie Informationen zu Ihrer {{site.data.keyword.cloud_notm}} Compose-Datenbank und dazu, wie Sie eine Verbindung zu ihr herstellen. Außerdem können Sie:
- Ihre Sicherungen verwalten
- Ihrem Service mehr Ressourcen zuordnen
- Das Servicekennwort ändern
- Whitelists verwenden, um den Zugriff auf Ihre Datenbank zu beschränken. 
Weitere Informationen finden Sie im Abschnitt [Einstellungen](./dashboard-settings.html).

## Verbindung zu {{site.data.keyword.composeForEtcd}} herstellen

Sie können mit den Berechtigungsnachweisen, die zusammen mit Ihrem Service erstellt werden, oder mithilfe der Verbindungszeichenfolgen und der Befehlszeile, die auf der Registerkarte *Übersicht* Ihres Service-Dashboards bereitgestellt werden, eine Verbindung zu dem Service herstellen.

## Verbindung von einer {{site.data.keyword.cloud_notm}}-Anwendung zu {{site.data.keyword.composeForEtcd}} herstellen

Um eine {{site.data.keyword.cloud_notm}}-Anwendung mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Informationen zum Herstellen einer Verbindung von einer {{site.data.keyword.cloud_notm}}-Anwendung zu einem {{site.data.keyword.composeForEtcd}}-Service finden Sie im Abschnitt [{{site.data.keyword.cloud_notm}}-Anwendung verbinden](./connecting-bluemix-app.html).

## Verbindung zu {{site.data.keyword.composeForEtcd}} außerhalb von {{site.data.keyword.cloud_notm}} herstellen

Wenn Sie außerhalb von {{site.data.keyword.cloud_notm}} eine Verbindung zu {{site.data.keyword.composeForEtcd}} herstellen wollen, können Sie dazu die bereitgestellten Verbindungszeichenfolgen oder die Befehlszeile verwenden. Informationen dazu, wie sich eine Verbindung herstellen lässt, finden Sie im Abschnitt [Externe Anwendung verbinden](./connecting-external.html).
