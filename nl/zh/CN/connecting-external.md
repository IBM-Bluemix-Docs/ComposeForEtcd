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

# 连接外部应用程序
{: #connecting-external-app}

# SSL 和 Compose etcd

{{site.data.keyword.composeForEtcd_full}} 使用自签名证书进行 SSL 连接，以允许更精确的证书锁定。这意味着与 etcd 文档中的常见示例相比，您需要传递给应用程序的参数存在一些差异。

## 获取 SSL 证书

要进行 SSL 连接，需要获取服务器的 SSL 证书，您可以在 {{site.data.keyword.composeForEtcd}} 服务的*概述*页面中找到该证书。

证书将显示为文本块。复制整个文本块，并将其粘贴到本地文件，以创建 SSL 证书文件。

**注：**在以下示例中，我们已调用文件 `servercert.crt`。

## 命令行实用程序 - curl 和 etcdctl

要使用命令行实用程序，请将该证书的路径和文件名传递到该实用程序。
让我们从 `curl` 开始，这是与 etcd 进行交谈的最原始的方法。只要将选项和参数 `-cacert certificate-filename` 添加到命令行以获取使用的证书：

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

`etcdctl` 命令提供了一种更为以 etcd 为中心的方式来控制系统，其在 `--ca-file certificate-filename` 中具有类似但不同的选项和参数，因此命令类似于：

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

还可以使用环境变量 `ETCDCTL_CA_FILE` 的值来设置证书参数。请记住在设置变量时，使用绝对路径和文件名来指向证书。

## 应用程序 - Go

如果您正在编写代码，那么如何传递证书信息将取决于您的语言和驱动程序。 

以下是使用 etcd Go 驱动程序的代码摘录。在此示例中，我们导入 `crypto/tls` 和 `crypto/x509` 软件包来处理 SSL 证书和[适用于 Go 的 CoreOS etcd 客户机](https://godoc.org/github.com/coreos/etcd/client)，如下所示：

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

下一个代码块将执行实际连接。该代码会读取证书文件，并将其添加到证书池。然后，该代码将证书文件作为根 CA 证书添加到 `tls.Config` 结构，创建一个 HTTP 传输并使用该传输来启动 etcd 客户机连接。

请注意，`peerlist`、`cafile`、`username` 和 `password` 是从命令行传入的字符串。

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

在 [examplco3 存储库](https://github.com/compose-ex/examplco3)中提供了使用此代码的完整示例。
