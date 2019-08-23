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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #frmwrks-wml}

您可以使用 {{site.data.keyword.pm_full}}，在 {{site.data.keyword.aios_full}} 中執行內容記載、回饋記載，以及測量效能精確度、執行時期偏誤偵測、可解釋性，以及自動除去偏誤功能。

{{site.data.keyword.aios_full}} 完整支援下列的 {{site.data.keyword.pm_full}} 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|Apache Spark MLlib|分類|結構化|
|Apache Spark MLLib|迴歸|結構化|
|Keras 搭配 TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> |分類| 非結構化（影像、文字）|
|Keras 搭配 TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> |迴歸| 非結構化（影像、文字）|
|Python 功能|分類|結構化|
|Python 功能|迴歸|結構化|
|scikit-learn|分類|結構化|
|scikit-learn|迴歸|結構化|
|XGBoost|分類|結構化|
|XGBoost|迴歸|結構化|
{: caption="架構支援明細" caption-side="top"}

<sup>1</sup>Keras 支援不包括支援公平性。
{: note}

<sup>2</sup> 如果您的模型 / 架構會輸出預測機率，則支援可解釋性。
{: note}

## 指定 {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 服務實例
{: #wml-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個 {{site.data.keyword.pm_full}} 實例。您的 {{site.data.keyword.pm_short}} 實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

### 必要條件
{: #wml-prereq}

您應該已將 {{site.data.keyword.pm_full}} 實例佈建於 {{site.data.keyword.aios_short}} 服務實例所在的相同 {{site.data.keyword.Bluemix_notm}} 帳戶中。如果您是以其他帳戶來佈建 {{site.data.keyword.pm_full}} 實例，就無法使用 {{site.data.keyword.aios_short}} 將該實例配置成使用自動執行有效負載記載。

### 連接 {{site.data.keyword.pm_short}} 服務實例
{: #wml-config}

{{site.data.keyword.aios_short}} 會連接至 {{site.data.keyword.pm_full}} 實例中的 AI 模型和部署。

1.  從**配置**標籤，在導覽窗格中，按一下**機器學習提供者**。

    ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

2.  按一下**新增機器學習提供者**按鈕，然後按一下 {{site.data.keyword.pm_full}} 圖磚。{{site.data.keyword.aios_short}} 會檢查您的 {{site.data.keyword.Bluemix_notm}} 帳戶，以找出任何現有的 {{site.data.keyword.pm_full}} 實例。 
3. 從 **Watson Machine Learning 服務**下拉功能表中選取一個實例。

    ![選取 {{site.data.keyword.pm_short}} 服務](images/gs-set-wml.png)

4.  （選用）您也可以改以**選取不同的位置**，以指定位於您 {{site.data.keyword.Bluemix_notm}} 帳戶外的機器學習位置。請提供您位置的認證，以作為有效 JSON：

    ![設定 {{site.data.keyword.pm_short}} 實例](images/gs-get-wml.png)

    按一下**儲存**。

1.  {{site.data.keyword.aios_short}} 會列出您所部署的模型；請選取您想監視的模型，並按一下**配置**。

## 後續步驟
{: #wml-next}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
