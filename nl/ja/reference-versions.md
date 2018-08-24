---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# バージョン
{: #versions}

デプロイ可能バージョン | 推奨バージョン
----------|-----------
3.2.18. 3.3.3 | 3.2.18、3.3.3
{: caption="表 1. {{site.data.keyword.composeForEtcd}} バージョン" caption-side="top"}

## 推奨バージョン

通常、推奨バージョンは、{{site.data.keyword.composeForEtcd}} で使用可能な etcd データベースの最新バージョンです。 このバージョンは、カタログ・ページ上のドロップダウン・バージョン・セレクターのデフォルトです。 また、API の呼び出しでバージョンを指定しない場合は、自動的にこのバージョンがプロビジョンされます。

### 新しい推奨バージョンのプロトコル

新しいバージョンが入手可能になると、そのリリースが発表され、デプロイメントでそのバージョンを使用できるようになります。 リリース以降、最新バージョンを入手できる期間が約 7 日間ありますが、これは推奨バージョンとしてリストされません。 ユーザーはこの期間に新しいバージョンをデプロイしたりテストしたりできますが、引き続き現行バージョンも使用できます。 さらにこの期間に、Compose エンジニアが新しいバージョンで発生した問題を発見して修正することもできます。 この 7 日間の期間の終わりに、新しいバージョンが推奨バージョンとして設定されるか、この変更に関する新しい日付が発表されます。

プロビジョンで使用可能なバージョンのリストは、{{site.data.keyword.composeForEtcd}} の[カタログ・ページ](https://console.{DomainName}/catalog/services/compose-for-etcd)にあります。

ご使用の {{site.data.keyword.composeForEtcd}} サービスで使用できるバージョンの現行リストを取得するには、
[GET /2016-07/deployments/:id/versions](https://apidocs.compose.com/v1.0/reference#2016-07-get-deployments-versions) エンドポイントを使用できます。
