---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-25"

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

# WML frameworks
{: #frmwrks-wml}

{{site.data.keyword.aios_full}} fully supports the following {{site.data.keyword.pm_full}} frameworks: 
{: shortdesc}

Table 1. Framework support details

| Framework | Problem type | Data type |
|:---|:---:|:---:|
| Apache Spark MLlib | Classification | Structured |
| Python function | Classification | Structured |
| Python function | Regression | Structured |
| XGBoost | Classification | Structured |
| XGBoost | Regression | Structured |
| Keras with TensorFlow<sup>1</sup> | Classification | Structured |
| Keras with TensorFlow<sup>1</sup> | Regression | Structured |
{: caption="Framework support details" caption-side="top"}

<sup>1</sup>Keras support does not include support for fairness.
{: note}



