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

# 外部アプリケーションの接続
{: #connecting-external-app}

# SSL と Compose etcd

{{site.data.keyword.composeForEtcd_full}} では、SSL 接続に自己署名証明書を使用して、より厳密な証明書固定が可能です。 これはまさに、etcd 資料の中の一般的な例に比べて、アプリケーションに渡す必要があるパラメーターにいくつかの違いがあるということになります。

## SSL 証明書の取得

SSL 接続を行うためには、サーバーの SSL 証明書を取得する必要があります。この証明書は、{{site.data.keyword.composeForEtcd}} サービスの*「概要」*ページにあります。

証明書はテキスト・ブロックとして示されます。 テキストのブロック全体をコピーし、それをローカル・ファイルに貼り付けて、SSL 証明書ファイルを作成します。

**注:** 以下の例では、そのファイルの名前を `servercert.crt` としています。

## コマンド・ライン・ユーティリティー - curl と etcdctl

コマンド・ライン・ユーティリティーを使用するには、その証明書のパスとファイル名をユーティリティーに渡します。 
`curl` から始めましょう。このユーティリティーは etcd と対話するための最もシンプルな手段です。 オプションとパラメーター `-cacert certificate-filename` をコマンド・ラインに追加するだけで、証明書が使用されるようになります。

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

`etcdctl` コマンドは、システムを制御するためのより etcd 中心の手段となりますが、`--ca-file certificate-filename` 内のオプションとパラメーターは似ているようで異なります。この場合は、次のようなコマンドになります。

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

証明書パラメーターは、環境変数 `ETCDCTL_CA_FILE` の値を使用して設定することもできます。 変数を設定するときは、必ず絶対パスとファイル名を使用して証明書を指すようにしてください。

## アプリケーション - Go

コードを書く場合、証明書情報をどのように渡すかは、使用する言語とドライバーによって決まります。 

etcd Go ドライバーを使用する Go のコードを抜き出したものを次に示します。 この例では、SSL 証明書と [Go 用 CoreOS etcd クライアント](https://godoc.org/github.com/coreos/etcd/client)を扱えるように、以下のように `crypto/tls` パッケージと `crypto/x509` パッケージをインポートします。

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

次のコード・ブロックが実際の接続を行います。 コードは証明書ファイルを読み取って証明書プールに追加します。 次にそれをルート CA 証明書として `tls.Config` 構造体に追加し、HTTP トランスポートを作成した後、そのトランスポートを使用して etcd クライアント接続を開始します。

`peerlist`、`cafile`、`username`、`password` は、コマンド・ラインから渡されるストリングであることに注意してください。

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

このコードを使用している完全な例は [examplco3 リポジトリー](https://github.com/compose-ex/examplco3)にあります。
