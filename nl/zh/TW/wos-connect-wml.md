---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# 指定 {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 服務實例
{: #wml-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個 {{site.data.keyword.pm_full}} 實例。您的 {{site.data.keyword.pm_short}} 實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

## 必要條件
{: #wml-prereq}

您應該已將 {{site.data.keyword.pm_full}} 實例佈建於 {{site.data.keyword.aios_short}} 服務實例所在的相同 {{site.data.keyword.Bluemix_notm}} 帳戶中。如果您是以其他帳戶來佈建 {{site.data.keyword.pm_full}} 實例，就無法使用 {{site.data.keyword.aios_short}} 將該實例配置成使用自動執行有效負載記載。

## 連接 {{site.data.keyword.pm_short}} 服務實例
{: #wml-config}

{{site.data.keyword.aios_short}} 會連接至 {{site.data.keyword.pm_full}} 實例中的 AI 模型和部署。

1.  從**配置**標籤，按一下**機器學習提供者**。

    ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

2.  選取 {{site.data.keyword.pm_full}} 圖磚。{{site.data.keyword.aios_short}} 會檢查您的 {{site.data.keyword.Bluemix_notm}} 帳戶，以找出任何現有的 {{site.data.keyword.pm_full}} 實例。 
3. 從 **Watson Machine Learning 服務**下拉功能表中選取一個實例。

    ![選取 {{site.data.keyword.pm_short}} 服務](images/gs-set-wml.png)

4.  （選用）您也可以改以**選取不同的位置**，以指定位於您 {{site.data.keyword.Bluemix_notm}} 帳戶外的機器學習位置。請提供您位置的認證，以作為有效 JSON：

    ![設定 {{site.data.keyword.pm_short}} 實例](images/gs-get-wml.png)

    按一下**儲存**。

1.  {{site.data.keyword.aios_short}} 會列出您所部署的模型；請選取您想監視的模型，並按一下**配置**。

### 後續步驟
{: #wml-next}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
