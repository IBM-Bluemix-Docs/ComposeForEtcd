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

# Conexión de una aplicación externa
{: #connecting-external-app}

# SSL y Compose etcd

{{site.data.keyword.composeForEtcd_full}} utiliza certificados autofirmados para conexiones SSL para permitir es establecimiento de certificados más precisos. Esto significa que hay algunas diferencias en los parámetros que deberá pasar a las aplicaciones en comparación con los ejemplos comunes de la documentación de etcd.

## Obtención del certificado SSL

Para establecer una conexión SSL, debe obtener el certificado SSL para el servidor, que encontrará en la página *Visión general* del servicio {{site.data.keyword.composeForEtcd}}.

El certificado se muestra como un bloque de texto. Copie todo el bloque de texto y péguelo en un archivo local para crear su archivo de certificado SSL.

**Nota:** En los ejemplos siguientes, hemos llamado a este archivo `servercert.crt`.

## Programas de utilidad de línea de mandatos - curl y etcdctl

Para utilizar los programas de utilidad de línea de mandatos, pase la vía de acceso y el nombre de archivo del certificado al programa de utilidad. 
Empezaremos que `curl`, el método más básico de establecer comunicación con etcd. Solo tiene que añadir la opción y el parámetro `-cacert certificate-filename` a la línea de mandatos para obtener el certificado utilizado:

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

El mandato `etcdctl`, que proporciona una forma más específica de etcd de controlar el sistema, tiene una opción y un parámetro parecidos, pero diferentes, en `--ca-file certificate-filename`, que hacen que la línea de mandatos quede así:

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

El parámetro de certificado también se puede establecer con el valor de una variable de entorno `ETCDCTL_CA_FILE`. No olvide utilizar una vía de acceso absoluta y un nombre de archivo para apuntar al certificado cuando defina la variable.

## Aplicaciones - Go

Si va a escribir código, la forma de pasar la información del certificado dependerá del lenguaje y del controlador. 

A continuación encontrará un extracto de código correspondiente a Go que utiliza el controlador Go de etcd. En este ejemplo, se importan los paquetes `crypto/tls` y `crypto/x509` para manejar el certificado SSL y el [cliente etcd de CoreOS para Go](https://godoc.org/github.com/coreos/etcd/client) de este modo:

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

El siguiente bloque de código establece la conexión real. El código lee el archivo de certificado y lo añade a una agrupación de certificados. Luego añade esto a una estructura `tls.Config` como certificado de CA raíz, crea un transporte HTTP y utiliza el transporte para iniciar la conexión del cliente etcd.

Tenga en cuenta que `peerlist`, `cafile`, `username` y `password` son series que se pasan desde la línea de mandatos.

```go
  peers := strings.Split(*peerlist, ",")

	// Leer el certificado en un archivo
	caCert, err := ioutil.ReadFile(*cafile)
	if err != nil {
		log.Fatal(err)
	}

	// Crear una agrupación de certificados
	caCertPool := x509.NewCertPool()
	// y añadir el certificado recién leído a la nueva agrupación
	caCertPool.AppendCertsFromPEM(caCert)

	// Crear una estructura de configuración de TLS
	// con la agrupación de certificados, ya que es una lista de entidades emisoras de certificados
	tlsConfig := &tls.Config{
		RootCAs: caCertPool,
	}

	// Luego crear un transporte HTTP con esta configuración
	transport := &http.Transport{TLSClientConfig: tlsConfig}

	// Cuando cree la configuración del cliente etcd, utilice dicho transporte
	cfg := client.Config{
		Endpoints:               peers,
		Transport:               transport,
		HeaderTimeoutPerRequest: time.Minute,
		Username:                *username,
		Password:                *password,
	}

	// Y cree el cliente de la forma habitual. 
	etcdclient, err := client.New(cfg)
```

Encontrará un ejemplo sobre cómo utilizar este código en el [repositorio examplco3](https://github.com/compose-ex/examplco3).
