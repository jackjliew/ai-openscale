---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

{{site.data.keyword.aios_short}} は、単一インスタンスで複数の機械学習エンジンに対応できます。機械学習エンジンは {{site.data.keyword.aios_short}} ダッシュボードの構成または [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) を使用してプロビジョンできます。
{: shortdesc}

{{site.data.keyword.aios_short}} の初回セットアップ時に、ユーザー・インターフェースまたは自動セットアップ・オプションを使用して、最初の機械学習エンジンをプロビジョンしている場合があります。 機械学習エンジンを追加するには、{{site.data.keyword.aios_short}} ダッシュボードの構成タブを使用するか、Python SDK を使用する必要があります。

## ダッシュボードを使用したプロバイダーの追加
{: #fmrk-workaround-multmleng-dashboard}

1. {{site.data.keyword.aios_short}} を開いた後に、**「構成」**タブで、**「機械学習プロバイダーの追加 (Add machine learning providers)」**ボタンをクリックします。

   ![機械学習プロバイダーのウィンドウにプロバイダーの追加ボタンが表示されています](images/wos-configure-multi-providers.png)

2. 追加するプロバイダーのタイルをクリックして、**「次へ」**をクリックします。

   ![機械学習プロバイダーの選択画面が表示されています](images/wos-machine-learning-providers-selection.png)

3. 必要な情報 (資格情報など) を入力して、**「保存」**をクリックします。

構成を保存したら、ダッシュボードに移動したり、デプロイメントを選択したり、モニターを構成したりできます。


## Python SDK バインディング・メソッドを使用した機械学習プロバイダーの追加
{: #fmrk-workaround-multmleng-binding}

Python API の `client.data_mart.bindings.add` メソッドを使用して、複数の機械学習エンジンを {{site.data.keyword.aios_short}} にバインドできます。 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- {{site.data.keyword.pm_full}} 機械学習エンジンをバインドするには、以下のコマンドを実行します。

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- Azure ML Studio 機械学習エンジンをバインドするには、以下のコマンドを実行します。

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon Sagemaker
{: #fmrk-workaround-multmleng-binding-aws}

- AWS Sagemaker 機械学習エンジンをバインドするには、以下のコマンドを実行します。

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

### Microsoft Azure ML Service
{: #fmrk-workaround-multmleng-binding-azureservice}

- Azure ML Service 機械学習エンジンをバインドするには、以下のコマンドを実行します。

  `binding_uid_4 = client.data_mart.bindings.add('My Azure ML Service engine', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### 機械学習プロバイダーのリストの生成
{: #fmrk-workaround-multmleng-binding-list}

すべてのバインディングのリストを表示するには、`list` メソッドを実行します。

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | My Azure ML Service engine | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="表 1. サービス・バインディング" caption-side="top"}


特定の機械学習エンジンについては、以下のトピックを参照してください。

- [カスタム機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind)
- [Microsoft Azure Machine Learning Studio エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [Microsoft Azure Machine Learning Service エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [Amazon SageMaker 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


実際のノートブックの作業例については、[{{site.data.keyword.aios_short}} サンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)を参照してください。

