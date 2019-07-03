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

# 支援多個機器學習引擎
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} 支援單一實例內有多個機器學習引擎，但前提是必須透過 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) 來執行佈建。
{: shortdesc}

在您第一次設置 {{site.data.keyword.aios_short}} 時，您可能使用了使用者介面或自動設置選項，來佈建您的第一個機器學習引擎。如果要新增機器學習引擎，則您需要使用 Python SDK。具體來說，您可以使用 `client.data_mart.bindings.add` 方法，將機器學習引擎新增至 {{site.data.keyword.aios_short}}。

## 連結方法
{: #fmrk-workaround-multmleng-binding}

您可以使用 Python API `client.data_mart.bindings.add` 方法，將多個機器學習引擎連結至 {{site.data.keyword.aios_short}}。 

- 如果要連結 {{site.data.keyword.pm_full}} 機器學習引擎，請執行下列指令：

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- 如果要連結 Azure ML Studio 機器學習引擎，請執行下列指令：

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- 如果要連結 AWS Sagemaker 機器學習引擎，請執行下列指令：

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

如果要檢視所有連結的清單，請執行 `list` 方法：

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="表 1. 服務連結" caption-side="top"}


如需特定機器學習引擎的相關資訊，請參閱下列主題：

- [連結您的自訂機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)
- [連結您的 Microsoft Azure 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [連結您的 Amazon SageMaker 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


如需實際記事本的運作範例，請參閱 [{{site.data.keyword.aios_short}} 樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

