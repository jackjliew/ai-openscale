---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# 将第三方 ML 引擎与 {{site.data.keyword.aios_short}} 集成
{: #fmrk-workaround}

{{site.data.keyword.aios_full}} 与外部机器学习服务引擎（例如 Microsoft Azure ML Studio、Microsoft Azure ML Service 和 Amazon SageMaker）集成。
{: shortdesc}

您可以通过以下方式将 {{site.data.keyword.aios_short}} 与第三方引擎集成：

- 引擎绑定级别：能够列出部署并获取部署详细信息。
  
- 部署预订级别：{{site.data.keyword.aios_short}} 需要能够以所需格式（例如 {{site.data.keyword.pm_full}} 格式）对预订部署进行评分，并以同一兼容格式接收输出。{{site.data.keyword.aios_short}} 必须配置为同时处理输入和输出格式。
   

- 有效内容日志记录：用户应用程序所触发的对已部署模型的各项输入和输出必须存储在有效内容库中。有效内容记录的格式遵循的规范与上一节中提及的有关部署预订级别的规范相同。
   
   {{site.data.keyword.aios_short}} 使用这些记录来计算偏差、解释和其他。{{site.data.keyword.aios_short}} 无法自动存储在 {{site.data.keyword.aios_short}} 系统外部的用户站点上执行的事务。这是 {{site.data.keyword.aios_short}} 保护专有信息的方法之一。请使用 {{site.data.keyword.aios_short}} Rest API 或 Python SDK 来处理安全数据。
   
## 实施此解决方案的步骤
{: #fmrk-workaround-steps}

1. [了解定制机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine)。
2. [设置有效内容日志记录](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload)。
3. [自动执行有效内容日志记录](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)。
4. 通过使用其中一个[定制机器学习引擎示例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)来设置定制机器学习引擎。

