---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Amazon SageMaker 架構
{: #frmwrks-aws-sage}

您可以使用 Amazon SageMaker，在 {{site.data.keyword.aios_full}} 中執行內容記載、回饋記載，以及測量效能精確度、執行時期偏誤偵測、可解釋性，以及自動除去偏誤功能。

{{site.data.keyword.aios_full}} 完整支援下列的 Amazon SageMaker 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|原生|分類|結構化|
|原生|迴歸<sup>1</sup> |結構化|
{: caption="架構支援明細" caption-side="top"}

<sup>1</sup>迴歸模型支援不包括漂移幅度。

## 新增 Amazon SageMaker 至 {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

您可以使用下列其中一種方法，將 {{site.data.keyword.aios_short}} 配置成使用 Amazon SageMaker：

- 如果您是第一次將機器學習提供者新增至 {{site.data.keyword.aios_short}}，您可以使用配置介面。如需相關資訊，請參閱[指定 Amazon SageMaker 實例](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)。
- 您也可以使用 Python SDK 來新增機器學習提供者。如果您希望有多個提供者，必須使用此方法。如需透過程式來執行此項的相關資訊，請參閱[連結 Amazon SageMaker 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)。


## 樣本記事本
{: #frmwrks-aws-sage-smpl-ntbks}

下列記事本顯示如何使用 Amazon SageMaker：

- [建立及部署信用風險預測模型](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [建立資料集區、監視模型部署，以及分析資料](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## 指定 Amazon SageMaker ML 服務實例
{: #csm-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個 Amazon SageMaker 服務實例。您的 Amazon SageMaker 服務實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

您也可以使用 Python SDK 來新增機器學習提供者。如需透過程式來執行此項的相關資訊，請參閱[連結 Amazon SageMaker 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)。

### 連接您的 Amazon SageMaker 服務實例
{: #csm-config}

{{site.data.keyword.aios_short}} 會連接至 Amazon SageMaker 服務實例中的 AI 模型和部署。

1.  從**配置**標籤，在導覽窗格中，按一下**機器學習提供者**。

    ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

1.  按一下**新增機器學習提供者**按鈕，然後按一下 **Amazon SageMaker** 圖磚。

    ![輸入 Amazon SageMaker 服務認證](images/connect-sage-cred.png)

1.  輸入並儲存您的認證：

    - 存取金鑰 ID：您的 AWS 存取金鑰 ID `aws_access_key_id`，用來驗證您的身分，並針對您對 AWS 所發出的呼叫進行鑑別及授權。
    - 秘密存取金鑰：您的 AWS 秘密存取金鑰 `aws_secret_access_key`，需要提供此項，以便驗證您的身分，並針對您對 AWS 所發出的呼叫進行鑑別及授權。
    - 地區：輸入您「存取金鑰 ID」建立所在的地區。會儲存金鑰，並用在它們建立所在的地區，且無法傳送到另一個地區。

1.  {{site.data.keyword.aios_short}} 會列出您所部署的模型；請選取您想監視的模型。

## 使用 Amazon SageMaker 機器學習引擎來記載有效負載
{: #cml-smconfig}

### 連結您的 Amazon SageMaker 機器學習引擎
{: #cml-smbind}

- 會將非 {{site.data.keyword.pm_full}} 引擎當成「自訂」來連結，也就是說，這僅僅是 meta 資料；不會與非 {{site.data.keyword.pm_full}} 服務直接整合。

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

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

- 對您的模型評分。如需完整範例，請參閱[使用 SageMaker 機器學習引擎記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}。


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
{: #csm-next}

- {{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
- [使用 Watson OpenScale 來監視 Sagemaker 機器學習](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
