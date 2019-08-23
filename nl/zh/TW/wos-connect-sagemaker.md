---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# 指定 Amazon SageMaker ML 服務實例
{: #csm-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個 Amazon SageMaker 服務實例。您的 Amazon SageMaker 服務實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

您也可以使用 Python SDK 來新增機器學習提供者。如需透過程式來執行此項的相關資訊，請參閱[連結 Amazon SageMaker 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)。

## 連接您的 Amazon SageMaker 服務實例
{: #csm-config}

{{site.data.keyword.aios_short}} 會連接至 Amazon SageMaker 服務實例中的 AI 模型和部署。

1. 從**配置**標籤，按一下**機器學習提供者**。視您的環境而定，您不見得能看到下列所有的提供者：

   ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

1.  按一下 **Amazon SageMaker** 圖磚。

    ![輸入 Amazon SageMaker 服務認證](images/connect-sage-cred.png)

1.  輸入並儲存您的認證：

    - 存取金鑰 ID：您的 AWS 存取金鑰 ID `aws_access_key_id`，用來驗證您的身分，並針對您對 AWS 所發出的呼叫進行鑑別及授權。
    - 秘密存取金鑰：您的 AWS 秘密存取金鑰 `aws_secret_access_key`，需要提供此項，以便驗證您的身分，並針對您對 AWS 所發出的呼叫進行鑑別及授權。
    - 地區：輸入您「存取金鑰 ID」建立所在的地區。會儲存金鑰，並用在它們建立所在的地區，且無法傳送到另一個地區。
    - 服務提供者實例名稱：指派給這個服務提供者的特定名稱。
    - 說明：（選用）此服務提供者實例的純語言說明。如果您具有正式作業環境和測試環境，這會是一個提供該資訊的好位置。

1.  {{site.data.keyword.aios_short}} 會列出您所部署的模型；請選取您想監視的模型。

### 後續步驟
{: #csm-next}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
