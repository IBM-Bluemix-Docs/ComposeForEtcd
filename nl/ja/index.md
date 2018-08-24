---

copyright:
  years: 2016,2018
lastupdated: "2018-03-26"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.composeForEtcd}} の概要
{: #about-compose-for-etcd}

etcd は、分散サーバー構成管理のためにサーバー・クラスターの調整と管理に必要な、常に正確なデータを保持するキー/値ストアです。 etcd は、RAFT コンセンサス・アルゴリズムを使用して、クラスター内のデータの整合性を保証します。 データに対する操作の実行順序を強制することで、クラスター内のすべてのノードにおいて同じ方法で同じ結果が得られるようにします。 {{site.data.keyword.composeForEtcd_full}} は、etcd に保管された構成データの自動バックアップを追加します。 直感的な管理インターフェースで、デプロイメントのモニター、スケーリング、管理を簡単に行えます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。 その時点以降にプロビジョンされた Compose サービス・インスタンスは、{{site.data.keyword.cloud}} アカウント内で直接アクセスして使用されます。

## {{site.data.keyword.composeForEtcd}} サービス・インスタンスの作成

{{site.data.keyword.composeForEtcd}} サービスは、{{site.data.keyword.cloud_notm}} カタログの [{{site.data.keyword.composeForEtcd}} ページ](https://console.{DomainName}/catalog/services/compose-for-etcd/)から作成できます。

サービス名、およびサービスをプロビジョンする地域、組織、スペースを選択します。 **「データベースのバージョンの選択 (Select a database version)」**フィールドを使用して、データベースの使用できるバージョンを選択できます。

{{site.data.keyword.composeForEtcd}} インスタンスをプロビジョンするときに、*「標準」*プランか*「エンタープライズ (Enterprise)」*プランかを選択できます。 *「エンタープライズ (Enterprise)」*プランを選択した場合は、使用可能な {{site.data.keyword.composeEnterprise}} クラスターに {{site.data.keyword.composeForEtcd}} インスタンスをプロビジョンできます。 {{site.data.keyword.composeEnterprise}} は、企業コンプライアンスで要求されるセキュリティーと分離を提供し、専用ネットワーキングを使用してデプロイ済みデータベースのパフォーマンスを確保します。 詳しくは、[{{site.data.keyword.composeEnterprise}} 文書](/docs/services/ComposeEnterprise/index.html)を参照してください。

## {{site.data.keyword.composeForEtcd}} の管理

サービス・ダッシュボードからサービスを管理できます。 ダッシュボードには {{site.data.keyword.cloud_notm}} Compose データベースとそれへの接続方法に関する情報が示されます。 また、以下の操作を行うこともできます。
- バックアップを管理する。
- サービスに割り振るリソースを増やす
- サービス・パスワードを変更する
- ホワイトリストを使用してデータベースへのアクセスを制限する。 

詳しくは、[設定](./dashboard-settings.html)を参照してください。

{{site.data.keyword.composeForEtcd}} は、Cloud Foundry の役割を利用して、サービスへのアクセスを管理します。 開発者役割を持つユーザーのみが、サービス・ダッシュボードを表示または使用できます。 Cloud Foundry の役割について詳しくは、『[Cloud Foundry アクセス権限](https://console.{DomainName}/docs/iam/cfaccess.html#cfaccess)』および 『[Cloud Foundry のアクセス権限の管理](https://console.{DomainName}/docs/iam/mngcf.html#mngcf)』のページを参照してください。
{: .tip}

## {{site.data.keyword.composeForEtcd}} への接続

サービスに接続するには、サービスと一緒に作成された資格情報を使用するか、サービス・ダッシュボードの*「概要」*タブに表示される接続ストリングとコマンド・ラインを使用します。

## {{site.data.keyword.composeForEtcd}} への {{site.data.keyword.cloud_notm}} アプリケーションの接続

{{site.data.keyword.cloud_notm}} アプリケーションをサービスに接続するには、サービスと一緒に作成された資格情報を使用します。 {{site.data.keyword.composeForEtcd}} サービスに {{site.data.keyword.cloud_notm}} アプリケーションを接続する方法が、[{{site.data.keyword.cloud_notm}} アプリケーションの接続](./connecting-bluemix-app.html)に記載されています。

## {{site.data.keyword.cloud_notm}} 外からの {{site.data.keyword.composeForEtcd}} への接続

{{site.data.keyword.cloud_notm}} 外から {{site.data.keyword.composeForEtcd}} に接続する場合は、示された接続ストリングまたはコマンド・ラインを使用できます。 接続方法については、[外部アプリケーションの接続](./connecting-external.html)を参照してください。
