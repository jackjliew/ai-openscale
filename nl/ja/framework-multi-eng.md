---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: multiple engines, non-Watson, machine learning, frameworks, provision

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

# 複数の機械学習エンジンのサポート
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} では、[Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) によってプロビジョニングを実行する場合に、単一インスタンス内で複数の機械学習エンジンを使用できます。
{: shortdesc}

{{site.data.keyword.aios_short}} の初回セットアップ時に、ユーザー・インターフェースまたは自動セットアップ・オプションを使用して、最初の機械学習エンジンをプロビジョンしている場合があります。 機械学習エンジンを追加するには、Python SDK を使用する必要があります。 具体的には、`client.data_mart.bindings.add` メソッドを使用して、機械学習エンジンを {{site.data.keyword.aios_short}} に追加できます。

## バインド・メソッド
{: #fmrk-workaround-multmleng-binding}

Python API の `client.data_mart.bindings.add` メソッドを使用して、複数の機械学習エンジンを {{site.data.keyword.aios_short}} にバインドできます。 

- {{site.data.keyword.pm_full}} 機械学習エンジンをバインドするには、以下のコマンドを実行します。

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- Azure ML Studio 機械学習エンジンをバインドするには、以下のコマンドを実行します。

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- AWS Sagemaker 機械学習エンジンをバインドするには、以下のコマンドを実行します。

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

すべてのバインディングのリストを表示するには、`list` メソッドを実行します。

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="表 1. サービス・バインディング" caption-side="top"}


特定の機械学習エンジンについては、以下のトピックを参照してください。

- [カスタム機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)
- [Microsoft Azure Machine Learning エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [Amazon SageMaker 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


実際のノートブックの作業例については、[{{site.data.keyword.aios_short}} サンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)を参照してください。

