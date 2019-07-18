---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Amazon SageMaker 架構
{: #frmwrks-aws-sage}

{{site.data.keyword.aios_full}} 完整支援下列的 Amazon SageMaker 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|原生|分類|結構化|
{: caption="架構支援明細" caption-side="top"}


## 新增 Amazon SageMaker 至 {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

您可以使用下列其中一種方法，將 {{site.data.keyword.aios_short}} 配置成使用 Amazon SageMaker：

- 如果您是第一次將機器學習提供者新增至 {{site.data.keyword.aios_short}}，您可以使用配置介面。如需相關資訊，請參閱[指定 Amazon SageMaker 實例](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)。
- 您也可以使用 Python SDK 來新增機器學習提供者。如果您希望有多個提供者，必須使用此方法。如需透過程式來執行此項的相關資訊，請參閱[連結 Amazon SageMaker 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)。


## 樣本記事本
{: #frmwrks-aws-sage-smpl-ntbks}

下列記事本顯示如何使用 Amazon SageMaker：

- [建立及部署信用風險預測模型](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [建立資料集區、監視模型部署，以及分析資料](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## 進一步探索
{: #frmwrks-aws-sage-mediumblogs}

[使用 Watson OpenScale 來監視 Sagemaker 機器學習](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
