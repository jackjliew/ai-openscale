---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: FAQs, frequently asked questions, questions

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

- [如何将预测列从整数数据类型转换为分类数据类型？](#wos-faqs-convert-data-types)
- [为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](#trainingdata)

### 如何将预测列从整数数据类型转换为分类数据类型？
{: #wos-faqs-convert-data-types}

在为模型配置公平性监视时，尽管预测标签为分类方式，预测列也仅允许整数数字值。如何为分类功能（非数字）配置此项？是否需要手动转换？ 

训练数据可能具有类标签，例如“Loan Denied”或“Loan Granted”。WML 评分端点返回的预测值为“0.0”、“0.1”等值。该评分端点还具有可选列，其中包含预测的文本表示。例如，如果 prediction=1.0，那么 predictionLabel 列的值可能为“Loan Granted”。如果此类列可用，那么在为模型配置有利和不利结果时，可以指定字符串值“Loan Granted”和“Loan Denied”。如果此类列不可用，那么需要为有利/不利类分别指定整数/双精度值 1.0 和 0.0。

WML 具有输出模式的概念，该概念定义 WML 评分端点的输出模式以及不同列的角色。角色用于识别哪列包含预测值，哪列包含预测概率，以及类标签值等。对于使用模型构建器创建的模型，将会自动设置输出模式。此外，也可使用 WML Python 客户机对其进行设置。用户可以使用输出模式来定义包含预测的字符串表示的列。这通过将列的 modeling_role 设置为“decoded-target”来完成。WML Python 客户机的文档可在以下位置获取：http://wml-api-pyclient-dev.mybluemix.net/#repository。搜索“OUTPUT_DATA_SCHEMA”以了解输出模式，并且要使用的 API 是接受 OUTPUT_DATA_SCHEMA 作为参数的 store_model API。

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


