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

# 支持多个机器学习引擎
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} 在单个实例中支持多个机器学习引擎。可以通过 {{site.data.keyword.aios_short}} 仪表板配置或 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) 来供应这些机器学习引擎。
{: shortdesc}

首次设置 {{site.data.keyword.aios_short}} 时，您可能已使用用户界面或自动设置选项来供应第一个机器学习引擎。添加机器学习引擎要求您使用 {{site.data.keyword.aios_short}} 仪表板上的配置选项卡或 Python SDK。

## 使用仪表板添加提供程序
{: #fmrk-workaround-multmleng-dashboard}

1. 打开 {{site.data.keyword.aios_short}} 后，请从**配置**选项卡单击**添加机器学习提供程序**按钮。

   ![在机器学习提供程序窗口上显示“添加提供程序”按钮](images/wos-configure-multi-providers.png)

2. 单击要添加的提供程序的磁贴，然后单击**下一步**。

   ![显示机器学习提供程序选择屏幕](images/wos-machine-learning-providers-selection.png)

3. 输入所需信息（例如凭证），然后单击**保存**。

保存配置后，可以选择转至仪表板，选择部署还是配置监视器。


## 使用 Python SDK 绑定方法添加机器学习提供程序
{: #fmrk-workaround-multmleng-binding}

您可以使用 Python API `client.data_mart.bindings.add` 方法将多个机器学习引擎绑定到 {{site.data.keyword.aios_short}}。 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- 要绑定 {{site.data.keyword.pm_full}} 机器学习引擎，请运行以下命令：

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- 要绑定 Azure ML Studio 机器学习引擎，请运行以下命令：

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon Sagemaker
{: #fmrk-workaround-multmleng-binding-aws}

- 要绑定 AWS Sagemaker 机器学习引擎，请运行以下命令：

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))`

### Microsoft Azure ML Service
{: #fmrk-workaround-multmleng-binding-azureservice}

- 要绑定 Azure ML Service 机器学习引擎，请运行以下命令：

  `binding_uid_4 = client.data_mart.bindings.add('My Azure ML Service engine', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### 生成机器学习提供程序列表
{: #fmrk-workaround-multmleng-binding-list}

要查看所有绑定的列表，请运行 `list` 方法：

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | My Azure ML Service engine | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="表 1. 服务绑定" caption-side="top"}


有关特定机器学习引擎的信息，请参阅以下主题：

- [绑定定制机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind)。
- [绑定 Microsoft Azure Machine Learning Studio 引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [绑定 Microsoft Azure Machine Learning Service 引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [绑定 Amazon SageMaker 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


有关实际笔记本的有效示例，请参阅 [{{site.data.keyword.aios_short}} 样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

