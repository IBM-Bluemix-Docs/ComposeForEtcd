---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Verfügbare Berechtigungsnachweise
{: #available-credentials}

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispielapp [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit einem {{site.data.keyword.composeForEtcd}}-Service mithilfe der Berechtigungsnachweise. 

Feldname|Beschreibung
----------|-----------
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine App eine Verbindung zum geeigneten Server herstellt. Das Zertifikat ist base64-codiert. Der Schlüssel muss vor der Verwendung decodiert werden, wie in der Beispiel-App gezeigt.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `etcd`.
`name`|Der Name der Datenbankimplementierung.
`uri`|Der URI, der bei der Verbindungsherstellung zum Service verwendet werden soll. `uri` enthält das Schema (`amqps:), Administrator-Benutzernamen und Kennwort, den Hostnamen des Servers, die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, sowie den Namen des `virtuellen Hosts.
{: caption="Tabelle 1. Compose for etcd - Berechtigungsnachweise" caption-side="top"}
