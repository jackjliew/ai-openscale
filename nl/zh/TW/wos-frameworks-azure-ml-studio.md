---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

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

# Microsoft Azure ML Studio 架構
{: #frmwrks-azure}

您可以使用 Microsoft Azure ML Studio，在 {{site.data.keyword.aios_full}} 中執行內容記載、回饋記載，以及測量效能精確度、執行時期偏誤偵測、可解釋性，以及自動除去偏誤功能。

{{site.data.keyword.aios_full}} 完整支援下列的 Microsoft Azure Machine Learning Studio 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|原生|分類|結構化|
|原生|迴歸|結構化|
{: caption="架構支援明細" caption-side="top"}

## 將 Microsoft Azure ML Studio 新增至 {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

您可以使用下列其中一種方法，配置 {{site.data.keyword.aios_short}} 以使用 Microsoft Azure ML Studio :

- 如果您是第一次將機器學習提供者新增至 {{site.data.keyword.aios_short}}，您可以使用配置介面。如需相關資訊，請參閱[指定 Microsoft Azure ML Studio 實例](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)。
- 您也可以使用 Python SDK 來新增機器學習提供者。如果您希望有多個提供者，必須使用此方法。如需透過程式來執行此項的相關資訊，請參閱[連結 Microsoft Azure 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)。


## 樣本記事本
{: #frmwrks-azure-smpl-ntbks}

下列記事本顯示如何使用 Microsoft Azure ML Studio：

- [建立資料集區、監視模型部署，以及分析資料](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure Service 模型評分範例](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 進一步探索
{: #frmwrks-azure-mediumblogs}

-[使用 Watson OpenScale 來監視 Azure 機器學習](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [AzureMachine Learning 服務與 Studio 有何不同？](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [取用部署成 Web 服務的 Azure 機器學習模型](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## 指定 Microsoft Azure ML Studio 實例
{: #connect-azure}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定 Microsoft Azure ML Studio 實例。您的 Azure ML Studio 實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

您也可以使用 Python SDK 來新增機器學習提供者。如需透過程式來執行此項的相關資訊，請參閱[連結 Microsoft Azure 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)。

### 連接 Azure ML Studio 實例
{: #ca-connect}

{{site.data.keyword.aios_short}} 會連接至 Azure ML Studio 實例中的 AI 模型和部署。

1.  從**配置**標籤，在導覽窗格中，按一下**機器學習提供者**。

    ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

1.  按一下**新增機器學習提供者**按鈕，然後按一下 **Microsoft Azure ML Studio** 圖磚。

    ![輸入 Azure ML Studio 認證](images/connect-azure-cred.png)

1.  輸入並儲存您的認證：

    - 用戶端 ID：您用戶端 ID 的實際字串值，用來驗證您的身分，並針對您對 Azure Studio 所發出的呼叫進行鑑別及授權。
    - 用戶端密碼：密碼的實際字串值，用來驗證您的身分，並針對您對 Azure Studio 所發出的呼叫進行鑑別及授權。
    - 租戶：您的租戶 ID 會對應至您的組織，並且是一個專用的 Azure AD 實例。如果要尋找租戶 ID，請將游標放在您的帳戶名稱上，以取得目錄 / 租戶 ID，或是在 Azure 入口網站中，選取 Azure Active Directory > 內容 > 目錄 ID。
    - 訂閱 ID：用來唯一識別您 Microsoft Azure 訂閱的訂閱認證。訂閱 ID 形成了每一次服務呼叫中的 URI 部分。

    如需如何取得 Microsoft Azure 認證的指示，請參閱[作法：使用入口網站來建立可存取資源的 Azure AD 應用程式和服務主體](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}。{: note}

1.  {{site.data.keyword.aios_short}} 會列出您所部署的模型；請選取您想監視的模型，並按一下**配置**。

您已順利選取部署。

## 使用 Microsoft Azure Machine Learning Studio 引擎來記載有效負載
{: #cml-azconfig}

### 連結您的 Microsoft Azure 機器學習引擎
{: #cml-azbind}

- 會將非 {{site.data.keyword.pm_full}} 引擎當成「自訂」來連結，也就是說，這僅僅是 meta 資料；不會與非 {{site.data.keyword.pm_full}} 服務直接整合。

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  您可以使用下列指令來查看您的服務連結：

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML 連結](images/ml-azure-bind.png)

### 新增 Microsoft Azure ML Studio 訂閱
{: #cml-azsub}

- 新增訂閱

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- 取得訂閱清單

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### 啟用有效負載記載
{: #cml-azenlog}

- 在訂閱中啟用有效負載記載

    ```python
    subscription.payload_logging.enable()
    ```

- 取得記載明細

    ```python
    subscription.payload_logging.get_details()
    ```

### 評分和有效負載記載
{: #cml-azscore}

- 對您的模型評分。如需完整範例，請參閱[使用 Azure Machine Learning Studio 引擎記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}。

- 將要求和回應儲存在有效負載記載表格中：

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **附註**：對於 Python 以外的語言，您也可以使用 REST API 來直接執行有效負載記載。

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```


## 後續步驟
{: #ca-next}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
