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

# 定制 ML 框架
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} 完全支持以下定制机器学习框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| 等同于 {{site.data.keyword.pm_full}} |分类| 结构化 |
{: caption="框架支持详细信息" caption-side="top"}

## 将定制机器学习引擎添加到 {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

您可以使用以下方法之一将 {{site.data.keyword.aios_short}} 配置为使用定制机器学习提供程序：

- 如果这是首次将定制机器学习提供程序添加到 {{site.data.keyword.aios_short}}，那么可以使用配置接口。有关更多信息，请参阅[指定定制机器学习实例](/docs/services/ai-openscale?topic=ai-openscale-co-connect)。
- 您还可以使用 Python SDK 来添加机器学习提供程序。如果您希望具有多个提供程序，那么必须使用此方法。有关以编程方式执行此操作的更多信息，请参阅[绑定定制机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)。


## 样本笔记本
{: #frmwrks-custom-smpl-ntbks}

- [使用 Kubernetes 集群创建定制机器学习引擎](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [数据集市创建、模型部署监视和数据分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## 深入探索
{: #frmwrks-custom-mediumblogs}

[使用 Watson OpenScale 监视定制机器学习引擎](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
