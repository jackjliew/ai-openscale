---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 解释非结构化文本模型
{: #ie-unstruct}

{{site.data.keyword.aios_short}} 支持非结构化文本数据的可解释性。
{: shortdesc}

## 使用非结构化文本模型
{: #ie-unstruct-steps}

1. 设置环境。
   2. 安装 {{site.data.keyword.aios_short}} 和 {{site.data.keyword.pm_full}} 软件包。
   3. 配置凭证。
   4. 安装创建模型和执行分析所需的库。其中包括以下库：
      - `pandas`
      - `pyspark`（如果使用的不是 {{site.data.keyword.DSX}}）

1. 创建并部署基于图像的模型。
   2. 将训练数据装入到 pandas 框架中。
   2. 按照数据对模型进行训练。
   3. 发布模型。
   4. 部署模型并对其进行评分。

7. 通过分配 `APIClient`、预订资产并对模型进行评分来配置 {{site.data.keyword.aios_short}}。
8. 配置可解释性。
   9. 启用可解释性。
   10. 获取事务的可解释性。

## 解释非结构化文本事务
{: #ie-unstruct-xplan}

以下可解释性示例显示用于评估非结构化文本的分类模型。此解释显示对于模型预测具有有利或不利影响的关键字。我们还会在作为输入馈送到模型的原始文本中显示已识别的关键字的位置。

![显示可解释性图像分类图表。它显示非结构化文本的置信度级别](images/insight-explain-text.png)

## 非结构化文本模型示例
{: #ie-unstruct-ntbkssample}

使用以下笔记本来查看详细代码样本并开发您自己的 {{site.data.keyword.aios_short}} 部署：

- [有关生成基于文本的模型的解释的教程](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

