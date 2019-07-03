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

# Microsoft Azure ML Studio 框架
{: #frmwrks-azure}

{{site.data.keyword.aios_full}} 完全支持以下 Microsoft Azure Machine Learning Studio 框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| 本机 |分类| 结构化 |
{: caption="框架支持详细信息" caption-side="top"}

## 将 Microsoft Azure ML Studio 添加到 {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

您可以使用以下方法之一将 {{site.data.keyword.aios_short}} 配置为使用 Microsoft Azure ML Studio：

- 如果这是首次将机器学习提供程序添加到 {{site.data.keyword.aios_short}}，那么可以使用配置接口。有关更多信息，请参阅[指定 Microsoft Azure ML Studio 实例](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)。
- 您还可以使用 Python SDK 来添加机器学习提供程序。如果您希望具有多个提供程序，那么必须使用此方法。有关以编程方式执行此操作的更多信息，请参阅[绑定 Microsoft Azure 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)。


## 样本笔记本
{: #frmwrks-azure-smpl-ntbks}

以下笔记本显示如何使用 Microsoft Azure ML Studio：

- [数据集市创建、模型部署监视和数据分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure 服务模型评分示例](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 深入探索
{: #frmwrks-azure-mediumblogs}

[使用 Watson OpenScale 监视 Azure 机器学习](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
