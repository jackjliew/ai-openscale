---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

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

# WML 架構
{: #frmwrks-wml}

{{site.data.keyword.aios_full}} 完整支援下列的 {{site.data.keyword.pm_full}} 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|Apache Spark MLlib|分類|結構化|
|Python 功能|分類|結構化|
|Python 功能|迴歸|結構化|
|XGBoost|分類|結構化|
|XGBoost|迴歸|結構化|
| Keras 搭配 TensorFlow<sup>1</sup> |分類| 非結構化（影像、文字）|
| Keras 搭配 TensorFlow<sup>1</sup> |迴歸| 非結構化（影像、文字）|
{: caption="架構支援明細" caption-side="top"}

<sup>1</sup>Keras 支援不包括支援公平性。
{: note}



