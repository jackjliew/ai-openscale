---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# WML 框架
{: #frmwrks-wml}

{{site.data.keyword.aios_full}} 完全支持以下 {{site.data.keyword.pm_full}} 框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| Apache Spark MLlib |分类| 结构化 |
| Python 函数 |分类| 结构化 |
| Python 函数 | 回归 | 结构化 |
| XGBoost |分类| 结构化 |
| XGBoost | 回归 | 结构化 |
| scikit-learn |分类| 结构化 |
| scikit-learn | 回归 | 结构化 |
| Keras，含 TensorFlow<sup>1</sup> |分类| 非结构化（图像，文本）|
| Keras，含 TensorFlow<sup>1</sup> | 回归 | 非结构化（图像，文本）|
{: caption="框架支持详细信息" caption-side="top"}

<sup>1</sup>Keras 支持不包括对公平性的支持。
{: note}



