---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: credentials, REST API, data mart

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

# 建立 {{site.data.keyword.aios_short}} 的認證
{: #cred-create}

如果要存取 {{site.data.keyword.aios_full}} REST API，則需要平台 API 金鑰和資料集區（亦稱為服務實例）ID。「平台 API 金鑰」可讓個別使用者能夠存取 {{site.data.keyword.cloud_notm}} 中的資源。
{: shortdesc}

對於企業帳戶，管理者可以建立資料集區，邀請使用者加入該帳戶，以便提供特定 {{site.data.keyword.aios_short}} 資料集區的存取權給那些使用者。之後使用者就可以建立自己的平台 API 金鑰，並且可以存取相同的 {{site.data.keyword.aios_short}} 資料集區。這不會有任何的衝突或安全風險。

## 建立平台 API 金鑰
{: #cred-create-apikey}

如果要建立「平台 API 金鑰」，請完成下列步驟：

1. 登入 [{{site.data.keyword.cloud_notm}}](https://{DomainName}){: external}。

2. 選取**管理** --> **安全** --> **平台 API 金鑰**

    ![平台 API 金鑰](images/cred-api-key.png)

3. 建立並儲存「平台 API 金鑰」。

如果要尋找資料集區（或服務實例）ID，請執行下列動作：

1. 按一下模型部署圖磚。
2. 按一下**配置** ![配置圖示](images/configure-deployment-button.png) 圖示。
3. 按一下**檢視有效負載記載端點**。
4. 在 {{site.data.keyword.aios_short}} **有效負載記載**頁面上，尋找**資料集區 ID** 欄位。

    ![資料集區 ID](images/data-mart-id.png)

## 使用指令主控台來建立服務實例認證
{: #cred-creds}

如果要為 {{site.data.keyword.aios_short}} 建立認證，請使用 {{site.data.keyword.cloud_notm}} [指令主控台](/docs/cli?topic=cloud-cli-ibmcloud-cli)來完成下列步驟：

1. 執行下列指令，以擷取您的 API 金鑰：

    ```curl
    ibmcloud login --sso
    ibmcloud iam api-key-create 'my_key'
    ```

    會顯示下列資訊：

    ```bash
    Name         my_key
    Created At   2018-10-09T14:04+0000
    API Key      Tg4Gxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxQU-nE
    Locked       false
    UUID         ApiKey-xxxxxxxxx-afd7-xxxxx-b0e1-xxxxxxxxxxx
    ```
2. 驗證您在 {{site.data.keyword.cloud_notm}} 帳戶中使用的「資源群組」。

  ![雲端中的資源群組](images/cloud-resource.png)

  如果您沒有使用 `Default` 資源群組，請執行下列指令，以取得您的 {{site.data.keyword.aios_short}} 認證：

   ```curl
   ibmcloud target -g myResourceGroup
   ```

  其中 `myResourceGroup` 是您 {{site.data.keyword.aios_short}} 實例相關聯的資源群組。

3. 執行下列指令，以擷取您的 {{site.data.keyword.aios_short}} 實例 ID：

    ```curl
    ibmcloud resource service-instance '<Your_Watson_OpenScale_instance_name>'
    ```
    **附註**：如果您是在 Windows 上使用 {{site.data.keyword.cloud_notm}} 指令主控台，請以雙引號 (") 取代上述指令中的單引號 (')。

    會顯示下列資訊：

    ```bash
    Name:                  AI OpenScale-my_instance
    ID:                    crn:v1:ibmcloud:public:aiopenscale:us-south:a/c2f2xxxxxxxxxxxx867::
    GUID:                  03daxxxx-xxxx-xxxx-xxxx-xxxxxxxx38a7
    Location:              us-south
    Service Name:          aiopenscale
    Service Plan Name:     lite
    Resource Group Name:   Default
    State:                 active
    Type:                  service_instance
    Sub Type:
    Tags:
    Created at:            2018-09-17T13:58:43Z
    Updated at:
    ```

    `GUID` 值是您的 {{site.data.keyword.aios_short}} 實例 ID。
        
## 後續步驟
{: #cred-create-next-steps}

指定您的機器學習提供者：

- [指定 IBM Watson Machine Learning 服務實例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-wml-connect)
- [指定 Microsoft Azure ML Studio 實例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-connect-azure)
- [指定 Microsoft Azure ML Service 實例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)
- [指定 Amazon SageMaker ML 服務實例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-csm-connect)
- [指定「自訂」ML 服務實例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-co-connect)