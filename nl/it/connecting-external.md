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

# Connessione a un'applicazione esterna
{: #connecting-external-app}

## SSL e Compose for Etcd

{{site.data.keyword.composeForEtcd_full}} utilizza i certificati firmati automaticamente per le connessioni SSL per consentire un'associazione certificato più precisa. Questo significa che i parametri che devi passare alle applicazioni sono diversi dagli esempi comuni nella documentazione etcd.

## Ottenimento del certificato SSL

Per effettuare una connessione SSL, devi ottenere il certificato SSL per il server, che puoi trovare nella pagina *Overview* del tuo servizio {{site.data.keyword.composeForEtcd}}.

Il certificato viene mostrato come un blocco di testo. Copia l'intero blocco di testo e incollalo in un file locale per creare il tuo file del certificato SSL.

**Nota:** nei seguenti esempi, il file che contiene i certificati è denominato `servercert.crt`.

## Programmi di utilità della riga di comando - curl e etcdctl

Per utilizzare i programmi di utilità della riga di comando, passa il percorso e il nome file del certificato al programma di utilità. 
Quando stai utilizzando `curl`, aggiungi soltanto l'opzione e il parametro `-cacert certificate-filename` alla tua riga di comando per ottenere il certificato utilizzato:

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

Il comando `etcdctl` fornisce un modo maggiormente basato su etcd per controllare il sistema. Ha un'opzione e un parametro simili, ma differenti, in `--ca-file certificate-filename`.

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

Il parametro del certificato può essere impostato con il valore di una variabile di ambiente `ETCDCTL_CA_FILE`. Ricorda di utilizzare un nome file e un percorso assoluti per puntare al certificato quando imposti la variabile.

## Applicazioni - Go

Se stai scrivendo il codice, il modo in cui passi le informazioni sul certificato dipende dal tuo linguaggio di programmazione e dal tuo driver. 

Questo è un estratto di codice per l'utilizzo di Go e il driver Go etcd. Questo esempio importa i pacchetti `crypto/tls` e `crypto/x509` per gestire il certificato SSL e il [client etcd CoreOS per Go](https://godoc.org/github.com/coreos/etcd/client).

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

Il prossimo blocco di codice esegue la connessione effettiva. Il codice legge il file del certificato e lo aggiunge a un pool di certificati. Ne esegue quindi l'aggiunta a una struttura `tls.Config` come il certificato CA root, crea un trasporto HTTP e lo utilizza per avviare la connessione client etcd.

**Nota:** nell'esempio di codice, `peerlist`, `cafile`, `username` e `password` sono stringhe che vengono passate dalla riga di comando.


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

Un esempio completo che utilizza questo codice è disponibile nel [repository examplco3](https://github.com/compose-ex/examplco3).
