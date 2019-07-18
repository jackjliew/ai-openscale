---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Amazon SageMaker フレームワーク
{: #frmwrks-aws-sage}

{{site.data.keyword.aios_full}} では、以下の Amazon SageMaker フレームワークが完全にサポートされています。
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| ネイティブ | 分類 | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}


## {{site.data.keyword.aios_short}} への Amazon SageMaker の追加
{: #frmwrks-aws-sage-add}

次のいずれかの方法を使用して、Amazon SageMaker と連携するように {{site.data.keyword.aios_short}} を構成できます。

- 初めて機械学習プロバイダーを {{site.data.keyword.aios_short}} に追加する場合は、構成インターフェースを使用すると良いでしょう。 詳しくは、[Amazon SageMaker インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)を参照してください。
- Python SDK を使用して、機械学習プロバイダーを追加することもできます。 複数のプロバイダーが必要な場合は、この方法を使用する必要があります。 この操作をプログラムで実行する方法については、[Amazon SageMaker 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)を参照してください。


## サンプル・ノートブック
{: #frmwrks-aws-sage-smpl-ntbks}

以下のノートブックは、Amazon SageMaker と連携する方法を示しています。

- [信用リスク予測モデルの作成とデプロイメント](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [データマートの作成、モデル・デプロイメントのモニター、およびデータ分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## 詳細
{: #frmwrks-aws-sage-mediumblogs}

[Monitor Sagemaker machine learning with Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
