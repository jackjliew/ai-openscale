---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: payload, non-Watson, machine learning, services, subscription

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 非 Watson Machine Learning 服務實例的有效負載記載
{: #cml-connect}

如果您的 AI 模型部署在 Watson Machine Learning (WML) 以外的機器學習引擎中，您必須使用 Python 用戶端，針對外部機器學習引擎啟用有效負載記載。
{: shortdesc}

請參閱 [{{site.data.keyword.aios_short}} Python 用戶端說明文件 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](http://ai-openscale-python-client.mybluemix.net/){: new_window}，以及樣本 {{site.data.keyword.aios_short}} Python 用戶端記事本（為 [{{site.data.keyword.aios_short}} 指導教學![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: new_window} 的一部分），以取得更完整的資訊。

## 開始之前
{: #cml-prereq}

Db2 或 Cloud Object Storage 中需要有模型訓練資料可用，才能監視您模型的偏誤。對於 Python 函數，不支援可解釋性和精確度。如需訓練資料的相關資訊，請參閱 [{{site.data.keyword.aios_short}} 為何需要存取我的訓練資料？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- 匯入並起始 {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  只要遵循「[建立認證](/docs/services/ai-openscale?topic=ai-openscale-cred-create)」主題中的步驟，即可找到認證。

- 在 PostgreSQL 資料庫中建立綱目名稱

- 設置資料集區

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## 使用「自訂」機器學習引擎
{: #cml-cusconfig}

### 連結您的「自訂」機器學習引擎
{: #cml-cusbind}

- 會將非 WML 引擎當成「自訂」來連結，也就是說，這僅僅是 meta 資料；不會與非 WML 服務直接整合。

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

### 評分和有效負載記載
{: #cml-cusscore}

- 對您的模型評分。如需完整範例，請參閱 [IBM {{site.data.keyword.aios_full}} 和「自訂」ML 引擎記事本 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}。

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

- 將要求和回應儲存在有效負載記載表格中

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **附註**：對於 Python 以外的語言，您也可以使用 REST API 來直接執行有效負載記載。

    ```json
    token_endpoint = "https://iam.bluemix.net/identity/token"
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

## 使用 Microsoft Azure 機器學習引擎
{: #cml-azconfig}

### 連結您的 MS Azure ML 引擎
{: #cml-azbind}

- 會將非 WML 引擎當成「自訂」來連結，也就是說，這僅僅是 meta 資料；不會與非 WML 服務直接整合。

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  您可以使用下列指令來查看您的服務連結：

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML 連結](images/ml-azure-bind.png)

### 新增 MS Azure ML 訂閱
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

- 對您的模型評分。如需完整範例，請參閱[使用 Azure Machine Learning Studio Engine 記事本 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: new_window}。

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

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
    token_endpoint = "https://iam.bluemix.net/identity/token"
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

## 使用 Amazon SageMaker 機器學習引擎
{: #cml-smconfig}

### 連結您的 AWS SageMaker ML 引擎
{: #cml-smbind}

- 會將非 WML 引擎當成「自訂」來連結，也就是說，這僅僅是 meta 資料；不會與非 WML 服務直接整合。

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  您可以使用下列指令來查看您的服務連結：

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker ML 連結](images/ml-sagemaker-bind.png)

### 新增 Amazon SageMaker ML 訂閱
{: #cml-smsub}

- 新增訂閱

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
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
{: #cml-smenlog}

- 在訂閱中啟用有效負載記載

    ```python
    subscription.payload_logging.enable()
    ```

- 取得記載明細

    ```python
    subscription.payload_logging.get_details()
    ```

### 評分和有效負載記載
{: #cml-smscore}

- 對您的模型評分。如需完整範例，請參閱[使用 SageMaker Machine Learning Engine 記事本 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: new_window}。

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

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
    token_endpoint = "https://iam.bluemix.net/identity/token"
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
{: #cml-next}

- 如果要繼續執行 {{site.data.keyword.aios_short}} 用戶端，請參閱[指定資料庫](/docs/services/ai-openscale?topic=ai-openscale-connect-db)。

- 如果要繼續執行 Python 指令程式庫，請參閱 [Python 用戶端說明文件 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](http://ai-openscale-python-client.mybluemix.net/){: new_window}。
