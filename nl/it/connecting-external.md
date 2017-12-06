---

copyright:
  years: 2017
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connessione a un'applicazione esterna
{: #connecting-external-app}

# SSL e Compose etcd

{{site.data.keyword.composeForEtcd_full}} utilizza i certificati firmati automaticamente per le connessioni SSL per consentire un'associazione certificato più precisa. Questo significa che esistono alcune differenze nei parametri di cui avrai bisogno per trasmettere la applicazioni confrontate agli esempi comuni nella documentazione etcd.

## Ottenimento del certificato SSL

Per effettuare una connessione SSL, devi ottenere il certificato SSL per il server, che puoi trovare nella pagina *Overview* del tuo servizio {{site.data.keyword.composeForEtcd}}.

Il certificato viene mostrato come un blocco di testo. Copia l'intero blocco di testo e incollalo in un file locale per creare il tuo file del certificato SSL.

**Nota:** nei seguenti esempi, abbiamo richiamato quel file `servercert.crt`.

## Programmi di utilità della riga di comando - curl e etcdctl

Per utilizzare i programmi di utilità della riga di comando trasmetti il percorso e il nome del file di tale certificato al programma di utilità.
Inizia con `curl`, il modo meno elaborato per utilizzare etcd. Aggiungi soltanto l'opzione e il parametro `-cacert certificate-filename` alla tua riga di comando per ottenere il certificato utilizzato:

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

Il comando `etcdctl`, che fornisce un modo più centrato con etcd per controllare il sistema ha un'opzione e un parametro simili ma differenti in `--ca-file certificate-filename` che dovrebbero emettere un comando simile a:

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

Il parametro del certificato può essere impostato con il valore di una variabile di ambiente `ETCDCTL_CA_FILE`. Ricorda di utilizzare un nome file e un percorso assoluti per puntare al certificato quando imposti la variabile.

## Applicazioni - Go

Se stai scrivendo il codice, come trasmetti le informazioni sul certificato dipenderà dal tuo linguaggio e driver. 

Questo è un estratto di codice per l'utilizzo di Go e il driver Go etcd. In questo esempio importiamo i pacchetti `crypto/tls` e `crypto/x509` per gestire il certificato SSL e [CoreOS etcd client for Go](https://godoc.org/github.com/coreos/etcd/client) in questo modo:

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

Il prossimo blocco di codice esegue la connessione effettiva. Il codice legge il file del certificato e lo aggiunge a un pool di certificati. Quindi aggiunge tutto a una struttura `tls.Config` come il certificato CA root, crea un trasporto HTTP e lo utilizza per avviare la connessione client etcd.

Tieni presente che `peerlist`, `cafile`, `username` e `password` che vengono trasmesse dalla riga di comando.

```go
  peers := strings.Split(*peerlist, ",")

	// Legge il certificato in un file
	caCert, err := ioutil.ReadFile(*cafile)
	if err != nil {
		log.Fatal(err)
			}

	// Crea un pool di certificati
	caCertPool := x509.NewCertPool()
	// e aggiunge il certificato appena letto al nuovo pool
	caCertPool.AppendCertsFromPEM(caCert)

	// Crea una struttura di configurazione TLS
	// con il pool di certificati così come è nell'elenco delle autorità di certificazione
	tlsConfig := &tls.Config{
		RootCAs: caCertPool,
	}

	// Quindi crea un trasporto HTTP con tale configurazione
	transport := &http.Transport{TLSClientConfig: tlsConfig}

	// Quando creiamo la configurazione client etcd, utilizza il trasporto
	cfg := client.Config{
		Endpoints:               peers,
		Transport:               transport,
		HeaderTimeoutPerRequest: time.Minute,
		Username:                *username,
		Password:                *password,
	}

	// E crea il tuo client normalmente.
	etcdclient, err := client.New(cfg)
```

Un esempio completo di utilizzo di questo codice è disponibile in [examplco3 repository](https://github.com/compose-ex/examplco3).
