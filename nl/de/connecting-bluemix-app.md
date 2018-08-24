---

copyright:
  years: 2016,2018
lastupdated: "2017-09-21"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.cloud_notm}}-Anwendung verbinden

Verbinden Sie eine {{site.data.keyword.cloud}}-Anwendung mit Ihrem Service mithilfe der Berechtigungsnachweise dieses Service, die bei dessen Bereitstellung erstellt werden. Die Beispielapp veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung zu einem {{site.data.keyword.composeForEtcd}}-Service mithilfe der bereitgestellten Berechtigungsnachweise und die Vorgehensweise zur Erstellung einer Datenbank sowie Lese- und Schreibvorgänge in dieser Datenbank.

## Verbindung mithilfe der Beispielapp 'Hello World' herstellen

Die Beispielapp [compose-etcd-helloworld-nodejs](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung zu einem {{site.data.keyword.composeForEtcd}}-Service mithilfe der bereitgestellten Berechtigungsnachweise. Die Anwendung erstellt eine Datenbank, liest daraus und schreibt darin.

Laden Sie die Beispielapp herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in {{site.data.keyword.cloud}} auf **App anzeigen**, um den Inhalt der Tabelle *examples* anzuzeigen.

## Verfügbare Berechtigungsnachweise
{: #available-credentials}

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispielapp [compose-etcd-helloworld-nodejs](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit einem {{site.data.keyword.composeForEtcd}}-Service mithilfe der Berechtigungsnachweise.

|Feldname|Beschreibung|
|----------|-----------|
|`ca_certificate_base64` `(optional)`|Ein selbst signiertes Zertifikat in Base64-Codierung, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum entsprechenden Server herstellt. Das Zertifikat ist nur für Services vorhanden, die ein selbst signiertes Zertifikat anstelle eines Zertifikats von Let's Encrypt verwenden. Der Schlüssel muss vor seiner Verwendung decodiert werden, wie in der Beispielanwendung gezeigt.|
|`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.|
|`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `etcd`.|
|`name`|Der Name der Datenbankimplementierung.|
|`uri`|Der URI, der bei der Verbindungsherstellung zum Service verwendet werden soll. `uri` enthält das Schema (`amqps:), Administrator-Benutzernamen und Kennwort, den Hostnamen des Servers, die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, sowie den Namen des `virtuellen Hosts.|
|`uri_direct_1`|Ein sekundärer URI, der bei der Verbindungsherstellung zum Service verwendet werden kann. Format wie für `uri`.|
{: caption="Tabelle 1. Compose for etcd - Berechtigungsnachweise" caption-side="top"}

**Hinweis:** Zwei `haproxy`-Portale bieten Zugriff auf den etcd-Service. Sowohl `uri` als auch `uri_direct_1` können zum Herstellen der Verbindung verwendet werden. In Ihrer Anwendung wechseln Sie zwischen `uri` und `uri_direct_1`, um die Reaktionen auf Verbindungsfehler zu verwalten.
