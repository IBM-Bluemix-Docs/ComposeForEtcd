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

# Connecting an external application
{: #connecting-external-app}

# SSL and Compose etcd

{{site.data.keyword.composeForEtcd_full}} uses self-signed certificates for SSL connections to allow for more precise certificate pinning. This does mean that there are some differences in the parameters you will need to pass to applications compared to common examples in the etcd documentation.

## Obtaining the SSL Certificate

To make an SSL connection, you need to obtain the SSL Certificate for the server, which you can find ion the *Overview* page of your {{site.data.keyword.composeForEtcd}} service.

The certificate is shown as a text block. Copy the whole block of text and paste it to a local file to create your SSL certificate file.

**Note:** In the following examples, we have called that file `servercert.crt`.

## Command line utilities - curl and etcdctl

To use command-line utilities pass the path and filename of that certificate to the utility. 
Let's start with `curl`, the rawest way to talk to etcd. Just add the option and parameter `-cacert certificate-filename` to your command line to get the certificate used:

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

The `etcdctl` command, which provides a more etcd-centric way to control the system has a similar, but different, option and parameter in `--ca-file certificate-filename` which would give a command like like:

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

The certificate parameter can also be set with the value an environment variable `ETCDCTL_CA_FILE`. Remember to use an absolute path and filename to point to the certificate when setting the variable.

## Applications - Go

If you are writing code then how you pass the certificate information will depend on your language and driver. 

Here's an extract of code for Go using the etcd Go driver. In this example we import the `crypto/tls` and `crypto/x509` pacakges to handle the SSL certificate and the [CoreOS etcd client for Go](https://godoc.org/github.com/coreos/etcd/client) like so:

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

The next block of code performs the actual connection. The code reads the certificate file, and adds it to a certificate pool. It then adds that to a `tls.Config` structure as the root CA certificate, creates a HTTP transport and uses that transport to start the etcd client connection.

Note that `peerlist`, `cafile`, `username` and `password` are strings being passed in from the command-line.

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

A full example using this code is available in the [examplco3 repository](https://github.com/compose-ex/examplco3).
