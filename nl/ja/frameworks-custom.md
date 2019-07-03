---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# カスタム ML フレームワーク
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} では、以下のカスタム機械学習フレームワークが完全にサポートされています。
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| {{site.data.keyword.pm_full}} と同等 | 分類 | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

## {{site.data.keyword.aios_short}} へのカスタム機械学習エンジンの追加
{: #frmwrks-custom-add}

次のいずれかの方法を使用して、カスタム機械学習プロバイダーと連携するように {{site.data.keyword.aios_short}} を構成できます。

- 初めてカスタム機械学習プロバイダーを {{site.data.keyword.aios_short}} に追加する場合は、構成インターフェースを使用すると良いでしょう。詳しくは、[カスタム機械学習インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-co-connect)を参照してください。
- Python SDK を使用して、機械学習プロバイダーを追加することもできます。複数のプロバイダーが必要な場合は、この方法を使用する必要があります。この操作をプログラムで実行する方法については、[カスタム機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)を参照してください。


## サンプル・ノートブック
{: #frmwrks-custom-smpl-ntbks}

- [Kubernetes クラスターを使用したカスタム機械学習エンジンの作成](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [データマートの作成、モデル・デプロイメントのモニター、およびデータ分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## 詳細
{: #frmwrks-custom-mediumblogs}

[Watson OpenScale によるカスタム機械学習エンジンのモニター](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
