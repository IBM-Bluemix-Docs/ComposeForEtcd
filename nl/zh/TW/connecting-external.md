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

# 連接外部應用程式
{: #connecting-external-app}

# SSL 及 Compose for Etcd

{{site.data.keyword.composeForEtcd_full}} 使用自簽憑證來進行 SSL 連線，以容許更精準的憑證綁定。這的確表示相較於 Etcd 文件中的一般範例，您需要傳遞至應用程式的參數中有一些差異。

## 取得 SSL 憑證

若要建立 SSL 連線，則需要取得伺服器的「SSL 憑證」，您可以在 {{site.data.keyword.composeForEtcd}} 服務的*概觀* 頁面中找到該憑證。

憑證會顯示為文字區塊。請複製整個文字區塊，並將它貼到本端檔案，以建立 SSL 憑證檔。

**附註：**在下列範例中，我們將該檔案稱為 `servercert.crt`。

## 指令行公用程式 - curl 及 etcdctl

若要使用指令行公用程式，請將該憑證的路徑及檔名傳遞至公用程式。讓我們從 `curl` 開始，這是與 Etcd 交談的最原始方式。只需將選項及參數 `-cacert certificate-filename` 新增至指令行，即可取得所使用的憑證：

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt
```

`etcdctl` 指令提供其他以 Etcd 為中心的方式來控制系統，而且在提供如下指令的 `--ca-file certificate-filename` 中具有類似但不同的選項及參數：

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /
```

也可以使用環境變數 `ETCDCTL_CA_FILE` 的值來設定憑證參數。設定變數時，請記得使用絕對路徑及檔名來指向憑證。

## 應用程式 - Go

如果您要撰寫程式碼，則傳遞憑證資訊的方式將視您的語言及驅動程式而定。 

以下摘錄使用 Etcd Go 驅動程式來擷取 Go 的程式碼。在此範例中，我們匯入 `crypto/tls` 及 `crypto/x509` 套件，來處理 SSL 憑證及[適用於 Go 的 CoreOS Etcd 用戶端](https://godoc.org/github.com/coreos/etcd/client)，例如：

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

下一個程式碼區塊會執行實際的連線。此程式碼會讀取憑證檔，並將它新增至憑證儲存區。然後，將它新增至 `tls.Config` 結構作為主要 CA 憑證、建立 HTTP 傳輸，並使用該傳輸來啟動 Etcd 用戶端連線。

請注意，`peerlist`、`cafile`、`username` 及 `password` 是從指令行傳入的字串。

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

使用此程式碼的完整範例可在 [examplco3 儲存庫](https://github.com/compose-ex/examplco3)中取得。
