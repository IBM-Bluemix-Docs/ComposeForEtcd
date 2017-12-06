---

copyright:
  years: 2016,2017
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Compose for etcd の概説
{: #getting-started-with-compose-for-etcd}

etcd は、分散サーバー構成管理のためにサーバー・クラスターの調整と管理に必要な、常に正確なデータを保持するキー/値ストアです。etcd は、RAFT コンセンサス・アルゴリズムを使用して、クラスター内のデータの整合性を保証します。データに対する操作の実行順序を強制することで、クラスター内のすべてのノードにおいて同じ方法で同じ結果が得られるようにします。{{site.data.keyword.composeForEtcd_full}} は、etcd に保管された構成データの自動バックアップを追加します。直感的な管理インターフェースで、デプロイメントのモニター、スケーリング、管理を簡単に行えます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、{{site.data.keyword.cloud}} アカウント内で直接アクセスして使用されます。

## Compose for Etcd サービス・インスタンスの作成

[{{site.data.keyword.composeForEtcd_full}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/)。

サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

{{site.data.keyword.composeForEtcd}} インスタンスをプロビジョンするときに、*「標準」*プランか*「エンタープライズ (Enterprise)」*プランかを選択できます。*「エンタープライズ (Enterprise)」*プランを選択した場合は、使用可能な {{site.data.keyword.composeEnterprise}} クラスターに {{site.data.keyword.composeForEtcd}} インスタンスをプロビジョンできます。{{site.data.keyword.composeEnterprise}} は、企業コンプライアンスで要求されるセキュリティーと分離を提供し、専用ネットワーキングを使用してデプロイ済みデータベースのパフォーマンスを確保します。詳しくは、[Compose Enterprise 文書](../ComposeEnterprise/index.html)を参照してください。

## Compose for Etcd の管理

サービス・ダッシュボードからサービスを管理できます。ダッシュボードには {{site.data.keyword.cloud_notm}} Compose データベースとそれへの接続方法に関する情報が示されます。また、以下の操作を行うこともできます。
- バックアップを管理する。
- サービスに割り振るリソースを増やす
- サービス・パスワードを変更する
- ホワイトリストを使用してデータベースへのアクセスを制限する。詳しくは、[設定](./dashboard-settings.html)を参照してください。

## Compose for Etcd への接続

サービスに接続するには、サービスと一緒に作成された資格情報を使用するか、サービス・ダッシュボードの*「概要」*タブに表示される接続ストリングとコマンド・ラインを使用します。

## Compose for Etcd への {{site.data.keyword.cloud_notm}} アプリケーションの接続

{{site.data.keyword.cloud_notm}} アプリケーションをサービスに接続するには、サービスと一緒に作成された資格情報を使用します。{{site.data.keyword.composeForEtcd}} サービスに {{site.data.keyword.cloud_notm}} アプリケーションを接続する方法が、[{{site.data.keyword.cloud_notm}} アプリケーションの接続](./connecting-bluemix-app.html)に記載されています。

## {{site.data.keyword.cloud_notm}} 外からの Compose for Etcd への接続

{{site.data.keyword.cloud_notm}} 外から {{site.data.keyword.composeForEtcd}} に接続する場合は、示された接続ストリングまたはコマンド・ラインを使用できます。接続方法については、[外部アプリケーションの接続](./connecting-external.html)を参照してください。
