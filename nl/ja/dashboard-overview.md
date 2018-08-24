---

Copyright:
  years: 2017,2018
lastupdated: "2018-05-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# サービス概要

_「概要」_ページには、{{site.data.keyword.cloud}} Compose データベースに関する情報が表示されます。例えば、重要な識別情報や現在のリソース使用率などの情報です。 さらに、データベースに接続するためのツールで使用できる接続ストリングも表示されます。

## デプロイメントの詳細 (Deployment Details)

_「デプロイメントの詳細 (Deployment Details)」_パネルには、サービスの詳細が表示されます。

![「デプロイメントの詳細 (Deployment Details)」](./images/etcd-deployment-details.png "「デプロイメントの詳細 (Deployment Details)」パネルのビュー")

### タイプ

サービスによって提供されるデータベースのタイプ、およびサービスが使用するデータベースのバージョン。 より新しいバージョンのデータベースが利用可能な場合は、通知が表示され、サービス・ダッシュボードの[「バージョンのアップグレード」](/docs/services/ComposeForEtcd/dashboard-settings.html#upgrade-version)セクションへのリンクが示されます。

### ID

サービスの内部 ID。

### 使用法

データベース・サイズとご使用のサービス・プランで利用可能なストレージ容量。

## 現行ジョブ

サービスに関する管理上の変更 (スケーリングや手動バックアップなど) を行うと、ジョブが開始されます。 ジョブの実行中に、_「概要 (Overview)」_ページに_「現行ジョブ (Current Jobs)」_パネルが表示され、ジョブ名と進行状況表示バーが示されます。 ジョブが完了すると、_「現行ジョブ (Current Jobs)」_パネルは_「概要 (Overview)」_ページに表示されなくなります。

## 接続ストリング (Connection Strings)

接続ストリングはいくつかのクライアント・ライブラリーで使用でき、他のライブラリーが接続するために必要なすべての情報を含んでいます。 [外部アプリケーションの接続](./connecting-external.html)に、接続ストリングを使用して {{site.data.keyword.composeForEtcd_full}} に接続する方法が記載されています。

_「接続ストリング」_パネルの各タブで、サービスで使用できるそれぞれの接続ストリングを確認できます。

### HTTPS

**HTTPS** 接続ストリングは、いくつかのクライアント・ライブラリーで使用でき、他のライブラリーが接続するために必要なすべての情報を含んでいます。 接続ストリングを使用して接続する方法については、[外部アプリケーションの接続](./connecting-external.html)を参照してください。

### コマンド・ライン

**コマンド・ライン**は、適切なパラメーターを使用して `etcd` を呼び出す事前フォーマット設定コマンドです。 これを使用するには、ローカル・システムに etcd クライアント・ツールがインストールされている必要があります。 その方法については、[外部アプリケーションの接続](./connecting-external.html)を参照してください。

### SSL 証明書

Compose {{site.data.keyword.cloud}} サービスは、データベースに接続するために使用できる SSL 証明書を提供します。


## インスタンス管理 API

{{site.data.keyword.composeForEtcd}} サービスは {{site.data.keyword.cloud_notm}} Compose API で管理できます。

### ファウンデーション・エンドポイント

ファウンデーション・エンドポイントは、サービスが存在する地域とサービス・インスタンス ID で構成されます。 これは、すべてのエンドポイントの先頭にあります。

### デプロイメント ID

デプロイメント ID はほとんどの呼び出しで必要であり、特定のデプロイメント・インスタンスを識別します。

### 参照

{{site.data.keyword.cloud_notm}} Compose サービス全体にわたる {{site.data.keyword.cloud_notm}} Compose API の使用についての詳しい資料やリファレンスは、[ {{site.data.keyword.cloud_notm}} Compose API](https://www.compose.com/articles/the-ibm-cloud-compose-api/) を参照してください。
