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

# 支持多个机器学习引擎
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} 在单个实例中支持多个机器学习引擎，前提是通过 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) 来执行供应。
{: shortdesc}

首次设置 {{site.data.keyword.aios_short}} 时，您可能已使用用户界面或自动设置选项来供应第一个机器学习引擎。添加机器学习引擎要求您使用 Python SDK。具体而言，您可以使用 `client.data_mart.bindings.add` 方法将机器学习引擎添加到 {{site.data.keyword.aios_short}}。

## 绑定方法
{: #fmrk-workaround-multmleng-binding}

您可以使用 Python API `client.data_mart.bindings.add` 方法将多个机器学习引擎绑定到 {{site.data.keyword.aios_short}}。 

- 要绑定 {{site.data.keyword.pm_full}} 机器学习引擎，请运行以下命令：

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- 要绑定 Azure ML Studio 机器学习引擎，请运行以下命令：

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- 要绑定 AWS Sagemaker 机器学习引擎，请运行以下命令：

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))`

要查看所有绑定的列表，请运行 `list` 方法：

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="表 1. 服务绑定" caption-side="top"}


有关特定机器学习引擎的信息，请参阅以下主题：

- [绑定定制机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)。
- [绑定 Microsoft Azure 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [绑定 Amazon SageMaker 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


有关实际笔记本的有效示例，请参阅 [{{site.data.keyword.aios_short}} 样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

