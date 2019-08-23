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

# 支援多個機器學習引擎
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} 支援單一實例內有多個機器學習引擎。您可以透過 {{site.data.keyword.aios_short}} 儀表板配置或 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) 來佈建它們。
{: shortdesc}

在您第一次設置 {{site.data.keyword.aios_short}} 時，您可能使用了使用者介面或自動設置選項，來佈建您的第一個機器學習引擎。如果要新增機器學習引擎，則您需要使用 {{site.data.keyword.aios_short}} 儀表板上的配置標籤或使用 Python SDK。

## 使用儀表板來新增提供者
{: #fmrk-workaround-multmleng-dashboard}

1. 在您開啟 {{site.data.keyword.aios_short}} 之後，請從**配置**標籤，按一下**新增機器學習提供者**按鈕。

   ![機器學習提供者視窗中會顯示「新增提供者」按鈕](images/wos-configure-multi-providers.png)

2. 按一下您想新增之提供者的圖磚，並按**下一步**。

   ![會顯示機器學習提供者選擇畫面](images/wos-machine-learning-providers-selection.png)

3. 輸入必要資訊（例如：認證），並按一下**儲存**。

儲存配置之後，您可以選擇移至儀表板、選擇部署，或是配置監視器。

## 編輯機器學習提供者
{: #fmrk-workaround-editingproviders-dashboard}

您是否需要編輯機器學習提供者？請按一下圖磚功能表 ![「圖磚功能表」圖示](images/v-three-dots.png) 圖示，然後按一下**檢視及編輯明細**。

   ![會顯示機器學習提供者視圖和編輯選項](images/wos-machine-learning-providers-edit.png)

## 使用 Python SDK 連結方法來新增機器學習提供者
{: #fmrk-workaround-multmleng-binding}

您可以使用 Python API `client.data_mart.bindings.add` 方法，將多個機器學習引擎連結至 {{site.data.keyword.aios_short}}。 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- 如果要連結 {{site.data.keyword.pm_full}} 機器學習引擎，請執行下列指令：

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- 如果要連結 Azure ML Studio 機器學習引擎，請執行下列指令：

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon Sagemaker
{: #fmrk-workaround-multmleng-binding-aws}

- 如果要連結 AWS Sagemaker 機器學習引擎，請執行下列指令：

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

### Microsoft Azure ML Service
{: #fmrk-workaround-multmleng-binding-azureservice}

- 如果要連結 Azure ML Service 機器學習引擎，請執行下列指令：

  `binding_uid_4 = client.data_mart.bindings.add('My Azure ML Service engine', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### 產生機器學習提供者清單
{: #fmrk-workaround-multmleng-binding-list}

如果要檢視所有連結的清單，請執行 `list` 方法：

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | My Azure ML Service engine | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="表 1. 服務連結" caption-side="top"}


如需特定機器學習引擎的相關資訊，請參閱下列主題：

- [連結您的自訂機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind)
- [連結 Microsoft Azure Machine Learning Studio 引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [連結 Microsoft Azure Machine Learning Service 引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [連結您的 Amazon SageMaker 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


如需實際記事本的運作範例，請參閱 [{{site.data.keyword.aios_short}} 樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

