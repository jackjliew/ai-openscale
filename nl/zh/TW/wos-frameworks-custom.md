---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

您可以使用自訂機器學習架構，在 {{site.data.keyword.aios_full}} 中執行內容記載、回饋記載，以及測量效能精確度、執行時期偏誤偵測、可解釋性，以及自動除去偏誤功能。自訂機器學習架構必須具有 {{site.data.keywor.pm_full}} 的同等項目。

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

## 自訂機器學習引擎
{: #fmrk-workaround-customengine}

自訂機器學習引擎可提供機器學習模型和 Web 應用程式的基礎架構和代管功能。{{site.data.keyword.aios_short}} 支援的自訂機器學習引擎必須符合下列需求：

- 顯現兩種類型的 REST API 端點：

   * 探索端點（GET 部署和明細清單）
   * 評分端點（線上和即時評分）

- 所有端點都需要相容於所要支援的 Swagger 規格。

- 與部署之間往來的輸入有效負載和輸出必須符合規格中說明的 JSON 檔案格式。

在這個階段，只支援 `BasicAuth` 或 `none` 格式。
{: Note}

下列範例顯示 REST API 端點規格：

![Swagger 文件中顯示的 REST API 端點規格](images/wosdeployments.png)


下列範例顯示輸入有效負載的格式：

![顯示輸入有效負載範例](images/wosinputdata.png)


## 自訂機器學習引擎何時會是最佳選擇？
{: #fmrk-workaround-enging-choice}

若為下列情況，則自訂機器學習引擎會是最佳選擇：

- 您並沒有使用任何可用的現成產品，來處理您的機器學習模型。您才剛開發了自己的系統來處理這件事。對此，{{site.data.keyword.aios_short}} 不提供直接支援，未來也不會。
- {{site.data.keyword.aios_short}} 尚不支援您用來處理模型的協力廠商引擎。在此情況下，請考量開發一個自訂機器學習引擎，以作為您原始或原生部署的封套。

## 指定「自訂」ML 服務實例
{: #co-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個服務實例。您的服務實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

## 連接您的「自訂」服務實例
{: #co-config}

{{site.data.keyword.aios_short}} 會連接至服務實例中的 AI 模型和部署。您可以連接自訂服務

1.  從**配置**標籤，在導覽窗格中，按一下**機器學習提供者**。

   ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

2. 按一下**新增機器學習提供者**按鈕，然後按一下**自訂環境**圖磚。

   ![會顯示「自訂機器學習提供者配置」畫面，其中具有認證、實例名稱和說明的相關欄位](images/ml-custom-provider.png)

3. 輸入您自訂機器學習提供者的名稱和說明，並按**下一步**。 

4. [要求取得清單](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list)或[輸入個別的評分端點](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints)，以選擇是否連接至您的部署。

   ![會顯示「連接至部署」畫面，其中具有一些選項，以用來要求取得部署清單，或用來輸入個別的評分端點](images/ml-custom-connect-deployments.png)
    
5. 按**下一步**。

### 要求取得部署清單
{: #co-config-request-list}

1. 如果您選取**要求取得部署清單**圖磚，請輸入您的認證和 API 端點，然後按一下**儲存**。

   ![會顯示「部署清單」畫面，其中具有一些欄位，以用來輸入服務認證和 API 端點](images/connect-custom-cred.png)

2. 儲存您的機器學習設置之後，請回到**儀表板**，按一下**洞察**標籤，然後按一下**新增至儀表板**按鈕。

3. 從清單中選取部署，並按一下**配置**。

現在，您可準備配置監視器。

### 提供個別的評分端點
{: #co-config-scoring-endpoints}

1. 如果您選取**輸入個別的評分端點**圖磚，請輸入您的 API 端點認證，然後按一下**儲存**。

2. 儲存您的機器學習設置之後，請回到**儀表板**，按一下**洞察**標籤，然後按一下**新增至儀表板**按鈕。

3. 按一下**新增端點**按鈕。

4. 從下拉功能表中，選取自訂環境，輸入部署名稱和 API 端點，然後按一下**儲存**。

現在，您可準備配置監視器。

### 如何運作
{: #co-works}

下列影像顯示「自訂」環境支援：

![會顯示「自訂如何運作」圖表。其中針對自訂環境，顯示一些與用戶端 API 和 Watson OpenScale API 有關的方框](images/custom-how-works.png)

您也可以參考下列鏈結：

[{{site.data.keyword.aios_short}} 有效負載記載 API](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[自訂部署 API](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[Python 用戶端連結 SDK](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[使用自訂機器學習引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[Python SDK for IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **支援監視器的模型輸入準則**

  您的模型應以特性向量作為輸入，這其實就是具名欄位和其值的集合（要監視其偏誤的欄位，就會成為這其中一個欄位）：

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  在本例中，`"age"` 可能就是某人要評估其公平性的欄位。

  如果輸入是一個張量/矩陣，而從輸入特性空間轉換而來（若是從文字或影像深度學習，往往就是如此），在現行版本中，{{site.data.keyword.aios_short}} 平台無法處理該模型。乃至於，如果深度學習模型含有文字或影像輸入，就無法處理以進行偏誤的偵測和減輕。

  此外，應載入訓練資料，以支援「可解釋性」。

  對於文字的可解釋性，完整文字應為其中一項特性。在現行版本中，若為「自訂」模型，則不支援影像的可解釋性。
  {: note}

- **支援監視器的模型輸出準則**

  除了您模型中各種類別的預測機率，該模型也應該輸出輸入特性向量。

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  在本例中，`"personal"` 和 `"camping"` 是可能的類別，每一個評分輸出中的評分都會指派給這兩個類別。如果遺漏預測機率，偏誤偵測將會運作，但自動除去偏誤不會運作。

  上述評分輸出應可從作用中的評分端點來存取，而 {{site.data.keyword.aios_short}} 可透過 REST 來呼叫該端點。若為 AzureML、SageMaker 和 {{site.data.keyword.pm_full}}，{{site.data.keyword.aios_short}} 會直接連接至原生評分端點（因此您不用擔心評分規格的實作）。

## 自訂機器學習引擎範例
{: #fmrk-workaround-cstmmlsengex}

使用下列範例，來設置您自己的自訂機器學習引擎。
{: shortdesc}

### Python 和 Flask
{: #fmrk-workaround-pandflask}

[發佈到 Git 上的自訂 ML 引擎範例](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}使用 Python 和 Flask 來處理 scikit-learn 模型。

[README 檔](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}說明基於測試用途，如何將應用程式部署在本端，以及如何將 cf 應用程式部署在 IBM Cloud 上。REST API 端點的實作可以在 [app.py 檔](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py){: external}中找到。

### Node.js
{: #fmrk-workaround-nodejs}

您也可以找到自訂機器學習引擎範例，它撰寫在[這裡的 Node.js](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs){: external} 中。

### 端對端程式碼型樣
{: #fmrk-workaround-e2ecode}

[程式碼型樣](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale){: external}顯示自訂引擎部署以及與 {{site.data.keyword.aios_short}} 整合的端對端範例。

## 使用自訂機器學習引擎來記載有效負載
{: #cml-cusconfig}

### 連結您的「自訂」機器學習引擎
{: #cml-cusbind}

- 會將非 {{site.data.keyword.pm_full}} 引擎當成「自訂」來連結，也就是說，這僅僅是 meta 資料；不會與非 {{site.data.keyword.pm_full}} 服務直接整合。您可以使用 `client.data_mart.bindings.add` 方法，將多個機器學習引擎連結至 {{site.data.keyword.aios_short}}。

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  您可以使用下列指令來查看您的服務連結：

    ```python
    client.data_mart.bindings.list()
    ```

    ![一般 ML 連結](images/ml-generic-bind.png)

### 新增「自訂」訂閱
{: #cml-cussub}

- 新增訂閱

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- 取得訂閱清單

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### 啟用有效負載記載
{: #cml-cusenlog}

- 在訂閱中啟用有效負載記載

    ```python
    subscription.payload_logging.enable()
    ```

- 取得記載明細

    ```python
    subscription.payload_logging.get_details()
    ```

如需相關資訊，請參閱[有效負載記載](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)。

### 評分和有效負載記載
{: #cml-cusscore}

- 對您的模型評分。如需完整範例，請參閱 [IBM {{site.data.keyword.aios_full}} 和自訂 ML 引擎記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}。

- 將要求和回應儲存在有效負載記載表格中

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

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
{: #fmrk-workaround-nxt-steps-over}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。

使用這些[自訂機器學習範例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)之一，來實作您自己的解決方案。
