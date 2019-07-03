---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Microsoft Azure ML Service 架構
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} 完整支援下列的 Microsoft Azure Machine Learning Service 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|原生|分類|結構化|
{: caption="架構支援明細" caption-side="top"}

## 將 Microsoft Azure ML Service 新增至 {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

您可以使用下列其中一種方法，將 {{site.data.keyword.aios_short}} 配置成使用 Microsoft Azure ML Service：

- 如果您是第一次將機器學習提供者新增至 {{site.data.keyword.aios_short}}，您可以使用配置介面。如需相關資訊，請參閱[指定 Microsoft Azure ML Studio 實例](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)。
- 您也可以使用 Python SDK 來新增機器學習提供者。如果您希望有多個提供者，必須使用此方法。如需透過程式來執行此項的相關資訊，請參閱[連結 Microsoft Azure 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)。


將 meta 資料所需的使用者有效負載上架。
建立模型上架使用者介面，以配置成監視上傳訓練資料/記事本 OpenScale 需求資訊執行有效負載記載，使用者介面 - 重新整理

實作者的責任 

MJS：請與 Lukasz & Clifford Chu 保持聯繫

A

## 樣本記事本
{: #frmwrks-azure-smpl-ntbks}

下列記事本顯示如何使用 Microsoft Azure ML Service：

- [建立資料集區、監視模型部署，以及分析資料](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure Service 模型評分範例](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 進一步探索
{: #frmwrks-azure-mediumblogs}

[使用 Watson OpenScale 來監視 Azure 機器學習](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
