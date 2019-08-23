---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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

# 常见问题解答
{: #wos-faqs}

此处您将从 {{site.data.keyword.aios_full}} 的用户找到一些最常见问题解答。
{: shortdesc}

## 问题
{: #wos-faqs-questions}

- [什么是 {{site.data.keyword.aios_short}}？](#faq-whatsa)
- [{{site.data.keyword.aios_short}} 如何定价？](#faq-pricing)
- [{{site.data.keyword.aios_short}} 是否可以免费试用？](#faq-freetrial)
- [我的所有 AI 模型都在 Azure 中。我是否可以将 Microsoft Azure ML 引擎与 {{site.data.keyword.aios_short}} 配合使用？](#faq-azure)
- [我的所有 AI 模型都在 Amazon 中。我是否可以将 Amazon SageMaker ML 引擎与 {{site.data.keyword.aios_short}} 配合使用？](#faq-sagemaker)
- [{{site.data.keyword.aios_short}} 在 {{site.data.keyword.icp4dfull_notm}} 上是否可用？](#faq-icp)
- [我想要在自己的服务器上运行 {{site.data.keyword.aios_short}}。我应该分配多少计算机处理能力？](#faq-sizing)
- [如何将预测列从整数数据类型转换为分类数据类型？](#wos-faqs-convert-data-types)
- [为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](#trainingdata)

### 什么是 {{site.data.keyword.aios_short}}
{: #faq-whatsa}

对于在任何位置构建并运行的模型，Watson OpenScale 在 AI 的整个生命周期内对其产生的结果进行跟踪和度量，并根据变化的业务情况调整和管理 AI。

通过观看此视频快速概览 {{site.data.keyword.aios_short}}。

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Trust and Transparency in AI" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

### {{site.data.keyword.aios_short}} 如何定价？
{: #faq-pricing}

当您准备就绪从 Lite 套餐进行转换时，存在一个**标准**定价计划，其中包括最多监视 24 个已部署模型，并且对于可解释性所对应的有效内容、反馈行或事务的数量没有任何限制。最新信息可在 [{{site.data.keyword.Bluemix}} 目录](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external}中获取。


### {{site.data.keyword.aios_short}} 是否可以免费试用？
{: #faq-freetrial}

{{site.data.keyword.aios_short}} 通过 Lite 套餐提供免费试用。要注册，请访问 [{{site.data.keyword.aios_short}} Web 页面](https://www.ibm.com/cloud/watson-openscale/){: external}，然后单击**立即入门**。您将能够任意长期使用 Lite 套餐（遵守每月刷新的每月使用限制）。

### 我的所有 AI 模型都在 Azure 中。我是否可以将 Microsoft Azure ML 引擎与 {{site.data.keyword.aios_short}} 配合使用？
{: #faq-azure}

{{site.data.keyword.aios_short}} 同时支持 Microsoft Azure ML Studio 引擎和 Microsoft Azure ML Service 引擎。有关更多信息，请参阅 [Microsoft Azure ML Studio 框架](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure)和 [Microsoft Azure ML Service 框架](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service)。

### 我的所有 AI 模型都在 Amazon 中。我是否可以将 Amazon SageMaker ML 引擎与 {{site.data.keyword.aios_short}} 配合使用？
{: #faq-sagemaker}

{{site.data.keyword.aios_short}} 支持 Amazon SageMaker ML 引擎。有关更多信息，请参阅 [Amazon SageMaker 框架](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage)。

### {{site.data.keyword.aios_short}} 在 {{site.data.keyword.icp4dfull_notm}} 上是否可用？
{: #faq-icp}

{{site.data.keyword.aios_short}} 是 {{site.data.keyword.icp4dfull_notm}} 的其中一个高级附加组件。 

### 我想要在自己的服务器上运行 {{site.data.keyword.aios_short}}。我应该分配多少计算机处理能力？
{: #faq-sizing}

针对三节点和六节点配置的[硬件配置](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#inst-hwt)，存在特定准则。IBM 技术销售团队还可帮助您调整特定配置的规模。由于 {{site.data.keyword.aios_short}} 作为 {{site.data.keyword.icp4dfull_notm}} 的附加组件运行，因此需要考虑两种软件产品的需求。

### 如何将预测列从整数数据类型转换为分类数据类型？
{: #wos-faqs-convert-data-types}

在为模型配置公平性监视时，尽管预测标签为分类方式，预测列也仅允许整数数字值。如何为分类功能（非数字）配置此项？是否需要手动转换？ 

训练数据可能具有类标签，例如“Loan Denied”或“Loan Granted”。{{site.data.keyword.pm_full}} 评分端点返回的预测值为“0.0”、“0.1”等值。该评分端点还具有一个可选列，其中包含预测的文本表示。例如，如果 prediction=1.0，那么 predictionLabel 列的值可能为“Loan Granted”。如果此类列可用，那么在为模型配置有利和不利结果时，可以指定字符串值“Loan Granted”和“Loan Denied”。如果此类列不可用，那么需要为有利/不利类分别指定整数/双精度值 1.0 和 0.0。

{{site.data.keyword.pm_full}} 具有输出模式的概念，该概念定义 {{site.data.keyword.pm_full}} 评分端点的输出模式以及不同列的角色。角色用于识别哪列包含预测值，哪列包含预测概率，以及类标签值等。对于使用模型构建器创建的模型，将会自动设置输出模式。此外，也可使用 {{site.data.keyword.pm_full}} Python 客户机对其进行设置。用户可以使用输出模式来定义包含预测的字符串表示的列。这通过将列的 modeling_role 设置为“decoded-target”来完成。{{site.data.keyword.pm_full}} Python 客户机的文档可在以下位置获取：http://wml-api-pyclient-dev.mybluemix.net/#repository。搜索“OUTPUT_DATA_SCHEMA”以了解输出模式，并且要使用的 API 是接受 OUTPUT_DATA_SCHEMA 作为参数的 store_model API。

### 为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？
{: #trainingdata}

您必须让 {{site.data.keyword.aios_short}} 能够访问存储在 Db2 或 {{site.data.keyword.cos_full_notm}} 中的训练数据，或者您必须运行一个能够访问训练数据的笔记本。{{site.data.keyword.aios_short}} 需要访问训练数据的原因是：

- 生成有对比的解释：要创建解释，需要访问统计信息，例如训练数据中的中值、标准差以及不同值。
- 显示训练数据统计信息：要填充偏差详细信息页面，{{site.data.keyword.aios_short}} 必须具有用于生成统计信息的训练数据。

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

在基于笔记本的方法中，您应该在 {{site.data.keyword.aios_short}} 中配置部署时上载统计信息和其他信息。 这意味着 {{site.data.keyword.aios_short}} 无法再访问位于环境中运行的笔记本外部的训练数据。其只能访问在配置期间上载的信息。


