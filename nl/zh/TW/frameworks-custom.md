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

# 自訂 ML 架構
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} 完整支援下列的自訂機器學習架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|相當於 {{site.data.keyword.pm_full}}|分類|結構化|
{: caption="架構支援明細" caption-side="top"}

## 將自訂機器學習引擎新增至 {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

您可以使用下列其中一種方法，配置 {{site.data.keyword.aios_short}} 以使用自訂機器學習提供者：

- 如果您是第一次將自訂機器學習提供者新增至 {{site.data.keyword.aios_short}}，您可以使用配置介面。如需相關資訊，請參閱[指定自訂機器學習實例](/docs/services/ai-openscale?topic=ai-openscale-co-connect)。
- 您也可以使用 Python SDK 來新增機器學習提供者。如果您希望有多個提供者，必須使用此方法。如需透過程式來執行此項的相關資訊，請參閱[連結自訂機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)。


## 樣本記事本
{: #frmwrks-custom-smpl-ntbks}

- [使用 Kubernetes 叢集來建立自訂機器學習引擎](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [建立資料集區、監視模型部署，以及分析資料](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## 進一步探索
{: #frmwrks-custom-mediumblogs}

[使用 Watson OpenScale 來監視自訂機器學習引擎](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
