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

# 외부 애플리케이션 연결
{: #connecting-external-app}

# SSL 및 Compose etcd

{{site.data.keyword.composeForEtcd_full}}에서는 SSL 연결을 위한 자체 서명된 인증서를 사용하여 보다 정확한 인증서 고정을 허용합니다. 이는 애플리케이션에 전달해야 하는 매개변수가 etcd 문서의 일반 예제와 비교할 때 일부 차이가 있음을 의미합니다.

## SSL 인증서 얻기

SSL 연결을 작성하려면 서버에 대한 SSL 인증서를 얻어야 합니다. 이는 {{site.data.keyword.composeForEtcd}} 서비스의 *개요* 페이지에서 찾을 수 있습니다.

인증서는 텍스트 블록에 표시됩니다. 전체 텍스트 블록을 복사하여 로컬 파일에 붙여넣어 SSL 인증서 파일을 작성하십시오.

**참고:** 다음 예제에서는 이 파일을 `servercert.crt`라고 했습니다.

## 명령행 유틸리티 - curl 및 etcdctl

명령행 유틸리티를 사용하려면 해당 인증서의 경로와 파일 이름을 유틸리티에 전달하십시오. 
etcd와 통신하는 가장 원시적인 방법인 `curl`부터 시작합니다. 인증서를 사용하려면 단순히 옵션과 `-cacert certificate-filename` 매개변수를 명령행에 추가하십시오.

```shell
curl -L https://user:pass@hostname:port/v2/keys/ --cacert ./servercert.crt

```

시스템을 제어하기 위한 보다 etcd 중심적인 방법을 제공하는 `etcdctl` 명령에서는 `--ca-file certificate-filename`의 옵션 및 매개변수가 유사하지만 다릅니다. 다음과 같은 명령을 제공할 수 있습니다.

```shell
etcdctl --ca-file servercert.crt --no-sync --peers https://host1:port1,https://host2:post2 -u user:pass ls /

```

환경 변수 `ETCDCTL_CA_FILE`의 값으로 인증서 매개변수를 설정할 수도 있습니다. 변수를 설정할 때 절대 경로와 파일 이름을 사용하여 인증서를 가리키십시오.

## 애플리케이션 - Go

코드를 작성 중인 경우 인증서 정보를 전달하는 방법은 언어 및 드라이버에 따라 다릅니다. 

다음은 etcd Go 드라이버를 사용하는 Go 코드를 추출한 것입니다. 이 예제에서는 다음과 같이 SSL 인증서 및 [Go용 CoreOS etcd 클라이언트](https://godoc.org/github.com/coreos/etcd/client)를 처리하기 위해 `crypto/tls` 및 `crypto/x509` 패키지를 가져옵니다.

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

다음 코드 블록에서 실제 연결을 수행합니다. 코드가 인증서 파일을 읽고 인증서 풀에 추가합니다. 그런 다음, `tls.Config` 구조에 루트 CA 인증서로 추가하고 HTTP 전송을 작성하여 해당 전송을 사용하여 etcd 클라이언트 연결을 시작합니다.

`peerlist`, `cafile`, `username` 및 `password`는 명령행에서 잔달되는 문자열입니다.

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

이 코드를 사용하는 전체 예제는 [examplco3 저장소](https://github.com/compose-ex/examplco3)에 있습니다.
