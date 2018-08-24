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

# Conectando um aplicativo externo
{: #connecting-external-app}

## SSL e Compose para Etcd

O {{site.data.keyword.composeForEtcd_full}} usa certificados autoassinados para conexões SSL para permitir uma fixação mais precisa de certificado. Isso significa que os parâmetros que você precisa passar para os aplicativos são diferentes de exemplos comuns na documentação do etcd.

## Obtendo o certificado SSL

Para fazer uma conexão SSL, você precisa obter o Certificado SSL para o servidor, que é possível localizar na página *Visão geral* do serviço {{site.data.keyword.composeForEtcd}}.

O certificado é mostrado como um bloco de texto. Copie o bloco inteiro de texto e cole-o em um arquivo local para criar seu arquivo de certificado SSL.

**Nota:** nos exemplos a seguir, o arquivo que contém o certificado é chamado de `servercert.crt`.

## Utilitários de linha de comandos - curl e etcdctl

Para usar os utilitários de linha de comandos, passe o caminho e o nome do arquivo do certificado para o utilitário. 
Quando você está usando `curl`, inclua a opção e o parâmetro `-cacert certificate-filename` em sua linha de comandos para obter o certificado usado:

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

O comando `etcdctl` fornece uma maneira mais centrada no etcd para controlar o sistema. Ele tem uma opção e um parâmetro semelhantes, mas diferentes, em `--ca-file certificate-filename`.

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

O parâmetro de certificado também pode ser configurado com o valor de uma variável de ambiente `ETCDCTL_CA_FILE`. Lembre-se de usar um caminho absoluto e o nome do arquivo para apontar para o certificado quando configurar a variável.

## Aplicativos- Go

Se você estiver gravando código, a forma de passar as informações de certificado dependerá de sua linguagem de programação e do driver. 

Aqui está uma extração de código para Go usando o driver etcd Go. Este exemplo importa os pacotes `crypto/tls` e `crypto/x509` para manipular o certificado SSL e o [cliente CoreOS etcd para o Go](https://godoc.org/github.com/coreos/etcd/client).

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

O próximo bloco de código executa a conexão real. O código lê o arquivo de certificado e o inclui em um conjunto de certificado. Em seguida, ele inclui isso em uma estrutura `tls.Config` como o certificado de autoridade de certificação raiz, cria um transporte HTTP e utiliza-o para iniciar a conexão do cliente etcd.

**Nota:** no exemplo de código, `peerlist`, `cafile`, `username` e `password` são sequências passadas por meio da linha de comandos.


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

Um exemplo completo que usa esse código está disponível no [repositório examplco3](https://github.com/compose-ex/examplco3).
