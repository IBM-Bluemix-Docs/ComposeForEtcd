---

copyright:
  years: 2017,2018
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Externe Anwendung verbinden
{: #connecting-external-app}

## SSL und Compose für Etcd

{{site.data.keyword.composeForEtcd_full}} verwendet selbst signierte Zertifikate für SSL-Verbindungen, um eine präzisere Zertifikatfixierung zu ermöglichen. Dies bedeutet, dass Sie andere Parameter an Anwendungen übergeben müssen als diejenigen, die in den allgemeinen Beispielen in der Dokumentation für etcd verwendet werden.

## SSL-Zertifikat abrufen

Zum Herstellen einer SSL-Verbindung müssen Sie das SSL-Zertifikat für den Server abrufen. Sie finden es auf der Seite *Übersicht* Ihres {{site.data.keyword.composeForEtcd}}-Service.

Das Zertifikat wird als Textblock angezeigt. Kopieren Sie den ganzen Textblock und fügen Sie ihn in eine lokale Datei ein, um Ihre SSL-Zertifikatsdatei zu erstellen.

**Hinweis:** In den nachfolgenden Beispielen hat die Datei, die das Zertifikat enthält, den Namen `servercert.crt`.

## Befehlszeilendienstprogramme - curl und etcdctl

Wenn Sie Befehlszeilendienstprogramme verwenden möchten, übergeben Sie den Pfad und den Dateinamen des Zertifikats an das Dienstprogramm.
Bei der Verwendung von `curl` fügen Sie `-cacert certificate-filename` als Kombination aus Option und Parameter zu Ihrer Befehlszeile hinzu, um das verwendete Zertifikat abzurufen:

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

Durch den Befehl `etcdctl` wird eine stärker etcd-zentrierte Art zum Steuern des Systems bereitgestellt. Mit `--ca-file certificate-filename` weist er eine eine ähnliche, nicht aber identische Kombination aus Option und Parameter auf.

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

Für den Zertifikatsparameter kann auch der Wert einer Umgebungsvariablen `ETCDCTL_CA_FILE` angegeben werden. Achten Sie darauf, mit einem absoluten Pfad und Dateinamen auf das Zertifikat zu verweisen, wenn Sie die Variable festlegen.

## Anwendungen - Go

Wenn Sie Code schreiben, richtet sich das Verfahren, mit dem Sie anschließend die Zertifikatsinformationen übergeben, nach der verwendeten Programmiersprache und dem entsprechenden Treiber. 

Nachstehend finden Sie einen Codeauszug für Go, bei dem der etcd Go-Treiber verwendet wird. Im vorliegenden Beispiel werden die Pakete `crypto/tls` und `crypto/x509` importiert, um das SSL-Zertifikat und den [CoreOS-etcd-Client für Go](https://godoc.org/github.com/coreos/etcd/client) zu bearbeiten.

```go
import (
	"crypto/tls"
	"crypto/x509"
	"io/ioutil"
	"net/http"
...
	"github.com/coreos/etcd/client"
	...
)
```

Der nächste Codeblock stellt die eigentliche Verbindung her. Der Code liest die Zertifikatsdatei und fügt sie zu einem Zertifikatpool hinzu. Dann fügt er sie als Root-CA-Zertifikat zu einer `tls.Config`-Struktur hinzu, erstellt einen HTTP-Transport und startet mit diesem Transport die etcd-Clientverbindung.

**Hinweis:** Im vorliegenden Codebeispiel sind `peerlist`, `cafile`, `username` und `password` Zeichenfolgen, die über die Befehlszeile übergeben werden.


```go
  peers := strings.Split(*peerlist, ",")

	// Read the certificate into a file
	caCert, err := ioutil.ReadFile(*cafile)
	if err != nil {
		log.Fatal(err)
	}

	// Create a certificate pool
	caCertPool := x509.NewCertPool()
	// and add the freshly read certificate to the new pool
	caCertPool.AppendCertsFromPEM(caCert)

	// Create a TLS configuration structure
	// with the certificate pool as it's a list of certificate authorities
	tlsConfig := &tls.Config{
		RootCAs: caCertPool,
	}

	// Then create a HTTP transport with that configuration
	transport := &http.Transport{TLSClientConfig: tlsConfig}

	// When we create the etcd client configuration, use that transport
	cfg := client.Config{
		Endpoints:               peers,
		Transport:               transport,
		HeaderTimeoutPerRequest: time.Minute,
		Username:                *username,
		Password:                *password,
	}

	// And create your client as normal. 
	etcdclient, err := client.New(cfg)
```

Ein vollständiges Beispiel, in dem dieser Code verwendet wird, ist im [examplco3-Repository](https://github.com/compose-ex/examplco3) verfügbar.
