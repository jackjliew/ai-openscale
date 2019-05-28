---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# 指定 Watson Machine Learning 服務實例
{: #wml-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個 Watson Machine Learning (WML) 實例。您的 WML 實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

## 必要條件
{: #wml-prereq}

您應該已將 WML 實例佈建於 {{site.data.keyword.aios_short}} 服務實例所在的相同 {{site.data.keyword.Bluemix_notm}} 帳戶中。如果您是將 WML 實例佈建於其他帳戶中，就無法使用 {{site.data.keyword.aios_short}} 來配置該實例。

## 連接 Watson Machine Learning 服務實例
{: #wml-config}

{{site.data.keyword.aios_short}} 會連接至 WML 實例中的 AI 模型和部署。

1.  從 {{site.data.keyword.aios_short}} 工具首頁，按一下**開始**。

    ![首頁](images/gs-config-start.png)

2.  選取 Watson Machine Learning 圖磚。

    ![圖磚選擇](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} 會檢查您的 {{site.data.keyword.Bluemix_notm}} 帳戶，以找出任何現有的 WML 實例。然後您可以從 **Watson Machine Learning 服務**下拉功能表中選取一個實例。

    ![選取 WML 服務](images/gs-set-wml.png)

4.  （選用）您也可以改以**選取不同的位置**，以指定位於您 {{site.data.keyword.Bluemix_notm}} 帳戶外的機器學習位置。請提供您位置的認證，以作為有效 JSON：

    ![設定 WML 實例](images/gs-get-wml.png)

    按**下一步**。

5.  {{site.data.keyword.aios_short}} 會檢查您選取的「機器學習」實例，以找出儲存在該實例中的部署清單。從部署清單中，選取您要監視的部署。

    ![選取部署](images/gs-config-deploy.png)

6.  按**下一步**。
7.  按一下**儲存**。

### 後續步驟
{: #wml-next}

{{site.data.keyword.aios_short}} 現在已備妥可供您[指定資料庫](/docs/services/ai-openscale?topic=ai-openscale-connect-db)。
