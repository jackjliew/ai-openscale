---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, azure

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Microsoft Azure ML Service フレームワーク
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} は、以下の Microsoft Azure Machine Learning Service フレームワークを完全にサポートしています。
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| ネイティブ | 分類 | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

## {{site.data.keyword.aios_short}} への Microsoft Azure ML Service の追加
{: #frmwrks-azure-add}

次のいずれかの方法を使用して、Microsoft Azure ML Service と連携するように {{site.data.keyword.aios_short}} を構成できます。

- 初めて機械学習プロバイダーを {{site.data.keyword.aios_short}} に追加する場合は、構成インターフェースを使用すると良いでしょう。詳しくは、[Microsoft Azure ML Studio インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)を参照してください。
- Python SDK を使用して、機械学習プロバイダーを追加することもできます。複数のプロバイダーが必要な場合は、この方法を使用する必要があります。この操作をプログラムで実行する方法については、[Microsoft Azure 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)を参照してください。


メタデータとして必要なユーザー・ペイロードをオンボーディングします。
モデルの作成
モニタリングを構成するためのオンボーディング UI
OpenScale が情報を必要としている訓練データ/ノートブックのアップロード
ペイロード・ロギングの実行、
UI - 更新

インプリメンターの責任 

MJS: Lukasz & Clifford Chu のフォローアップ

A

## サンプル・ノートブック
{: #frmwrks-azure-smpl-ntbks}

以下のノートブックは、Microsoft Azure ML Service と連携する方法を示しています。

- [データマートの作成、モデル・デプロイメントのモニター、およびデータ分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure Service model scoring examples](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 詳細
{: #frmwrks-azure-mediumblogs}

[Watson OpenScale による Azure 機械学習のモニター](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
