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

# Übersicht über den Service

Auf der Seite _Übersicht_ finden Sie Informationen zu Ihrer {{site.data.keyword.cloud}} Compose-Datenbank. Die Übersicht enthält die zentralen Identifikationsinformationen sowie die aktuelle Ressourcennutzung. Außerdem finden Sie einen Abschnitt für Verbindungszeichenfolgen, die Sie mit Tools verwenden können, und Angaben zum Herstellen von Verbindungen zu Ihrer Datenbank mithilfe von Tools.

## Bereitstellungsdetails

Die Anzeige _Bereitstellungsdetails_ enthält Details zu Ihrem Service.

![Bereitstellungsdetails](./images/etcd-deployment-details.png "Ansicht der Anzeige 'Bereitstellungsdetails'")

### Typ

Der Datenbanktyp, der vom Service angeboten wird, und die Datenbankversion, die Ihr Service verwendet.

### Name

Eine interne ID für den Service.

### Nutzung

Die Größe Ihrer Datenbank und der von Ihrem Serviceplan bereitgestellte Speicherplatz.


## Verbindungszeichenfolgen

Verbindungszeichenfolgen können von bestimmten Clientbibliotheken verwendet werden und enthalten alle Informationen, die andere Bibliotheken zum Herstellen einer Verbindung benötigen. Informationen dazu, wie sich mithilfe einer Verbindungszeichenfolge eine Verbindung zu {{site.data.keyword.composeForEtcd_full}} herstellen lässt, finden Sie im Abschnitt [Externe Anwendung verbinden](./connecting-external.html).

Die einzelnen Verbindungszeichenfolgen für Ihren Service befinden sich jeweils auf einer eigenen Registerkarte der Anzeige _Verbindungszeichenfolgen_.

### HTTPS

Die **HTTPS**-Verbindungszeichenfolge kann von bestimmten Clientbibliotheken verwendet werden und enthält alle Informationen, die andere Bibliotheken zum Herstellen einer Verbindung benötigen. Informationen dazu, wie sich mithilfe der Verbindungszeichenfolge eine Verbindung herstellen lässt, finden Sie im Abschnitt [Externe Anwendung verbinden](./connecting-external.html).

### Befehlszeile

Die **Befehlszeile** ist ein vorformatierter Befehl, der `etcd` mit den korrekten Parametern aufruft. Um ihn verwenden zu können, müssen die etcd-Client-Tools auf dem lokalen System installiert sein. Informationen dazu, wie Sie dazu vorgehen müssen, finden Sie im Abschnitt [Externe Anwendung verbinden](./connecting-external.html).

### SSL-Zertifikat

Ihr Compose-{{site.data.keyword.cloud}}-Service stellt Ihnen ein SSL-Zertifikat bereit, mit dem Sie eine Verbindung zu Ihrer Datenbank herstellen können.
