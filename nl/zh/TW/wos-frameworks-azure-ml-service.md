---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

您可以使用 Microsoft Azure ML Service，在 {{site.data.keyword.aios_full}} 中執行內容記載、回饋記載，以及測量效能精確度、執行時期偏誤偵測、可解釋性，以及自動除去偏誤功能。

{{site.data.keyword.aios_full}} 完整支援下列的 Microsoft Azure Machine Learning Service 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|原生|分類|結構化|
|scikit-learn|分類|結構化|
|scikit-learn|迴歸|結構化|
{: caption="架構支援明細" caption-side="top"}

## 將 Microsoft Azure ML Service 新增至 {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

您可以使用下列其中一種方法，將 {{site.data.keyword.aios_short}} 配置成使用 Microsoft Azure ML Service：

- 如果您是第一次將機器學習提供者新增至 {{site.data.keyword.aios_short}}，您可以使用配置介面。如需相關資訊，請參閱[指定 Microsoft Azure ML Service 實例](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)。
- 您也可以使用 Python SDK 來新增機器學習提供者。如果您希望有多個提供者，必須使用此方法。如需透過程式來執行此項的相關資訊，請參閱[連結 Microsoft Azure 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)。


{{site.data.keyword.aios_short}} 會呼叫與 Azure ML Service 所需的各種不同 REST 端點。如果要這樣做，您必須連結 Azure Machine Learning Service {{site.data.keyword.aios_short}}。

1. 建立一個 Azure Active Directory 服務主體。
2. 在新增 Azure ML Service 服務連結時（不論是透過使用者介面或 Python {{site.data.keyword.aios_short}} SDK），請指定認證詳細資料。

## JSON 要求和回應檔案的需求
{: #frmwrks-azureservice-JSON}

若要讓 {{site.data.keyword.aios_short}} 能使用 Azure ML Service，您所建立的 Web 服務部署必須符合特定需求。根據以下所述的需求，您建立的 Web 服務部署必須接受 JSON 要求，並且傳回 JSON 回應。

### 必要的 Web 服務 JSON 要求格式
{: #frmwrks-azureservice-JSON-sample-request}

- REST API 要求內文必須是 JSON 文件，且含有一個由 JSON 物件組成的 JSON 陣列。
- JSON 陣列的名稱必須是 `"input"`。
- 每一個 JSON 物件只能包含一個簡式鍵值組，其中，值只能是字串、數字、`true`、`false`或 `null`
- 值不能是 JSON 物件或陣列
- 不論是否有非 `null` 值可用，陣列中每一個 JSON 物件所指定的索引鍵（從而索引鍵數目）必須相同


下列範例 JSON 檔案符合上述需求，而可作為用來建立您自己 JSON 要求檔的範本：


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### 必要的 Web 服務 JSON 回應格式
{: #frmwrks-azureservice-JSON-sample-response}

在您建立 JSON 回應檔時，請記下下列項目：

- REST API 回應內文必須是 JSON 文件，且含有一個由 JSON 物件組成的 JSON 陣列。
- JSON 陣列的名稱必須是 `"output"`。
- 每一個 JSON 物件只能包含鍵值組，其中，值只能是字串、數字、`true`、`false`、`null`，或一個不含其他任何 JSON 物件或陣列的陣列。
- 值不能是 JSON 物件
- 不論是否有非 `null` 值可用，陣列中每一個 JSON 物件所指定的索引鍵（以及索引鍵數目）必須相同
- 對於分類模型：Web 服務必須傳回每一個類別的機率陣列，且對於陣列中的每一個 JSON 物件，其機率排序必須一致。
  - 範例：假設您有一個用來預測貸方風險的二進位分類模型，其中的類別是 `Risk` 或 `No Risk`
  - 對於 "output" 陣列中所傳回的每一個結果，物件必須包含鍵值組，內含固定順序的機率，其格式如下：
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

為了與 Azure ML Studio 和 Service 兩者中使用的 Azure ML 視覺化工具一致，建議（但非必要）使用下列的索引鍵名稱：

- 索引鍵名稱 `"Scored Labels"`，用來表示模型預測值的輸出索引鍵
- 索引鍵名稱 `"Scored Probabilities"`，用來表示每一個類別之機率陣列的輸出索引鍵

下列範例 JSON 檔案符合上述需求，而可作為用來建立您自己 JSON 回應檔的範本：


```JSON
{
  "output": [
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## 樣本記事本
{: #frmwrks-azureservice-smpl-ntbks}

下列記事本顯示如何使用 Microsoft Azure ML Service：

- [MS Azure Service 模型評分範例](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## 指定 Microsoft Azure ML Service 實例
{: #connect-azureservice}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定 Microsoft Azure ML Service 實例。您的 Azure ML Service 實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

您也可以使用 Python SDK 來新增機器學習提供者。如需透過程式來執行此項的相關資訊，請參閱[連結 Microsoft Azure Service 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)。

## 連接 Azure ML Service 實例
{: #ca-connect}

{{site.data.keyword.aios_short}} 會連接至 Azure ML Service 實例中的 AI 模型和部署。

1.  從**配置**標籤，在導覽窗格中，按一下**機器學習提供者**。
1.  按一下**新增機器學習提供者**按鈕，然後按一下 **Microsoft Azure ML Service**圖磚。
1.  輸入並儲存您的認證：

    - 用戶端 ID：您用戶端 ID 的實際字串值，用來驗證您的身分，並針對您對 Azure Service 所發出的呼叫進行鑑別及授權。
    - 用戶端密碼：密碼的實際字串值，用來驗證您的身分，並針對您對 Azure Service 所發出的呼叫進行鑑別及授權。
    - 租戶：您的租戶 ID 會對應至您的組織，並且是一個專用的 Azure AD 實例。如果要尋找租戶 ID，請將游標放在您的帳戶名稱上，以取得目錄 / 租戶 ID，或是在 Azure 入口網站中，選取 Azure Active Directory > 內容 > 目錄 ID。
    - 訂閱 ID：用來唯一識別您 Microsoft Azure 訂閱的訂閱認證。訂閱 ID 形成了每一次服務呼叫中的 URI 部分。

    如需如何取得 Microsoft Azure 認證的指示，請參閱[作法：使用入口網站來建立可存取資源的 Azure AD 應用程式和服務主體](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}。{: note}

1.  {{site.data.keyword.aios_short}} 會列出您所部署的模型；請選取您想監視的模型，並按一下**配置**。

您已順利選取部署。

## 使用 Microsoft Azure ML Service 引擎來記載有效負載
{: #cml-azsrvconfig}

### 連結 Microsoft Azure ML Service 引擎
{: #cml-azsrvbind}

會將非 {{site.data.keyword.pm_full}} 引擎當成「自訂」來連結，也就是說，這僅僅是 meta 資料；不會與非 {{site.data.keyword.pm_full}} 服務直接整合。
   
```
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

binding_uid = client.data_mart.bindings.add('My Azure ML Service engine', AzureMachineLearningServiceInstance(AZURE_ENGINE_CREDENTIALS))


    bindings_details = client.data_mart.bindings.get_details()
    ```
{: codeblock}

您可以使用下列指令來查看您的服務連結：

```
    client.data_mart.bindings.list()
    ```
{: codeblock}

範例輸出：

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### 新增 Microsoft Azure ML Service 訂閱
{: #cml-azsrvsub}

新增訂閱

```
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```
{: codeblock}

取得訂閱清單

```
    subscriptions = client.data_mart.subscriptions.get_details()subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```
{: codeblock}

### 啟用有效負載記載
{: #cml-azsrvenlog}

在訂閱中啟用有效負載記載

```
    subscription.payload_logging.enable()
    ```
{: codeblock}

取得記載明細

```
    subscription.payload_logging.get_details()
    ```
{: codeblock}

### 評分和有效負載記載
{: #cml-azsrvscore}

對您的模型評分。如需完整範例，請參閱[使用 Azure Machine Learning Service 引擎記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}。

將要求和回應儲存在有效負載記載表格中：

```
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))subscription.payload_logging.store(records=records_list)
    ```
{: codeblock}
{: python}
   
對於 Python 以外的語言，您也可以使用 REST API 來直接執行有效負載記載。
   
```
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
{: codeblock}
{: json}


```
    import requests, uuidPAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])payload = [{
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
{: codeblock}



## 後續步驟
{: #ca-next}

-{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
- [AzureMachine Learning 服務與 Studio 有何不同？](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

