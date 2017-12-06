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

# Connexion d'une application externe
{: #connecting-external-app}

# SSL et Compose etcd

{{site.data.keyword.composeForEtcd_full}} utilise des certificats autosignés pour les connexions SSL afin de permettre un épinglage plus précis des certificats. Cela implique certaines différences au niveau des paramètres que vous devrez transmettre aux applications par rapport aux exemples classiques de la documentation etcd.

## Obtention du certificat SSL

Pour établir une connexion SSL, vous avez besoin d'un certificat SSL pour le serveur, disponible sur la page *Vue d'ensemble* de votre service {{site.data.keyword.composeForEtcd}}.

Le certificat se présente comme un bloc de texte. Copiez l'intégralité du bloc et collez-le dans un fichier local pour créer votre fichier de certificat SSL.

**Remarque :** Dans les exemples suivants, ce fichier se nomme `servercert.crt`.

## Utilitaires de ligne de commande - curl et etcdctl

Pour utiliser les utilitaires de ligne de commande, transmettez le chemin et le nom de fichier de ce certificat aux utilitaires.
Commençons avec `curl`, le moyen le plus simple de communiquer avec etcd. Ajoutez simplement l'option et le paramètre `-cacert certificate-filename` à votre ligne de commande pour obtenir le certificat utilisé :

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

La commande `etcdctl`, qui fournit une méthode plus axée sur etcd de contrôle du système, propose une option et un paramètre similaires, bien que différents, dans `--ca-file certificate-filename` qui donne une comme du type :

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

Le paramètre de certificat peut également être défini avec la valeur d'une variable d'environnement `ETCDCTL_CA_FILE`. N'oubliez pas que vous devez utiliser un chemin d'accès absolu et un nom de fichier pour pointer sur le certificat lorsque vous définissez la variable.

## Applications - Go

Lorsque vous écrivez du code, la manière de transmettre les informations de certificat dépendra du langage et du pilote utilisé. 

Voici un extrait de code pour Go qui utilise le pilote Go etcd. Dans cet exemple, nous importons les pacakges `crypto/tls` et `crypto/x509` pour gérer le certificat SSL et le [client CoreOS etcd pour Go](https://godoc.org/github.com/coreos/etcd/client) comme suit :

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

Le bloc de code suivant effectue la connexion effective. Le code lit le fichier certificat et l'ajoute à un pool de certificats. Ensuite, il ajoute cet élément à une structure `tls.Config` en tant que certificat d'autorité de certification racine, crée un transport HTTP et utilise ce transport pour démarrer la connexion client etcd.

Notez les `peerlist`, `cafile`, `username` et `password` transmises depuis la ligne de commande.

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

Vous trouverez un exemple complet d'utilisation de ce code dans le [référentiel examplco3](https://github.com/compose-ex/examplco3).
