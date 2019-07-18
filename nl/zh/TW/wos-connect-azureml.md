---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure studio, ml, machine learning, services, studio

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

# 指定 Microsoft Azure ML Studio 實例
{: #connect-azure}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定 Microsoft Azure ML Studio 實例。您的 Azure ML Studio 實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

您也可以使用 Python SDK 來新增機器學習提供者。如需透過程式來執行此項的相關資訊，請參閱[連結 Microsoft Azure 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)。

## 連接 Azure ML Studio 實例
{: #ca-connect}

{{site.data.keyword.aios_short}} 會連接至 Azure ML Studio 實例中的 AI 模型和部署。

1.  從**配置**標籤，按一下**機器學習提供者**。

    ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

1.  按一下 **Microsoft Azure ML Studio** 圖磚。

    ![輸入 Azure ML Studio 認證](images/connect-azure-cred.png)

1.  輸入並儲存您的認證：

    - 用戶端 ID：您用戶端 ID 的實際字串值，用來驗證您的身分，並針對您對 Azure Studio 所發出的呼叫進行鑑別及授權。
    - 用戶端密碼：密碼的實際字串值，用來驗證您的身分，並針對您對 Azure Studio 所發出的呼叫進行鑑別及授權。
    - 租戶：您的租戶 ID 會對應至您的組織，並且是一個專用的 Azure AD 實例。如果要尋找租戶 ID，請將游標放在您的帳戶名稱上，以取得目錄 / 租戶 ID，或是在 Azure 入口網站中，選取 Azure Active Directory > 內容 > 目錄 ID。
    - 訂閱 ID：用來唯一識別您 Microsoft Azure 訂閱的訂閱認證。訂閱 ID 形成了每一次服務呼叫中的 URI 部分。

    如需如何取得 Microsoft Azure 認證的指示，請參閱[作法：使用入口網站來建立可存取資源的 Azure AD 應用程式和服務主體](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}。{: note}

1.  {{site.data.keyword.aios_short}} 會列出您所部署的模型；請選取您想監視的模型，並按一下**配置**。

您已順利選取部署。

### 後續步驟
{: #ca-next}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
