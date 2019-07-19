---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} frameworks
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
| scikit-learn | Classification | Structured |
| scikit-learn | Regression | Structured |
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Classification | Unstructured (image, text) |
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Regression | Unstructured (image, text) |
{: caption="Framework support details" caption-side="top"}

<sup>1</sup>Keras support does not include support for fairness.
{: note}

<sup>2</sup>If your model / framework outputs prediction probabilities.
{: note}



