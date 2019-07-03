---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: payload, non-Watson, machine learning, services, subscription

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

# 非 {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 服务实例的有效内容日志记录
{: #cml-connect}

如果 AI 模型部署在除 {{site.data.keyword.pm_full}} 以外的其他机器学习引擎中，那么您必须使用 Python 客户机为外部机器学习引擎启用有效内容日志记录。
{: shortdesc}

请参阅 [{{site.data.keyword.aios_short}} Python 客户机文档](http://ai-openscale-python-client.mybluemix.net/){: external}以及样本 {{site.data.keyword.aios_short}} Python 客户机笔记本（包含在 [{{site.data.keyword.aios_short}} 教程中](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}），其中提供了更完整的信息。

## 开始之前
{: #cml-prereq}

您需要让 Db2 或 {{site.data.keyword.cos_full}} 能够使用您的模型的训练数据，这样才能监视模型的偏差。Python 函数不支持可解释性和准确性。有关训练数据的更多信息，请参阅 [ 为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- 导入并启动 {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  可以通过遵循“[创建凭证](/docs/services/ai-openscale?topic=ai-openscale-cred-create)”主题中显示的步骤来找到凭证。

- 在 PostgreSQL 数据库中创建模式名称

- 设置数据集市

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## 使用定制机器学习引擎
{: #cml-cusconfig}

### 绑定定制机器学习引擎
{: #cml-cusbind}

- 非 {{site.data.keyword.pm_full}} 引擎绑定为“定制”，意味着这只是元数据；没有任何与非 {{site.data.keyword.pm_full}} 服务的直接集成。您可以使用 `client.data_mart.bindings.add` 方法将多个机器学习引擎绑定到 {{site.data.keyword.aios_short}}。

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  您可以使用以下命令查看服务绑定：

    ```python
    client.data_mart.bindings.list()
    ```

    ![通用 ML 绑定](images/ml-generic-bind.png)

### 添加定制预订
{: #cml-cussub}

- 添加预订

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- 获取预订列表

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### 启用载荷日志记录
{: #cml-cusenlog}

- 在预订中启用载荷日志记录

    ```python
    subscription.payload_logging.enable()
    ```

- 获取日志记录详细信息

    ```python
    subscription.payload_logging.get_details()
    ```

有关更多信息，请参阅[有效内容日志记录]()。

### 评分和载荷日志记录
{: #cml-cusscore}

- 对模型进行评分。有关完整示例，请参阅 [IBM {{site.data.keyword.aios_full}} & 定制 ML 引擎笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}。

- 在载荷日志记录表中存储请求和响应

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **注意**：对于除 Python 以外的其他语言，您还可以使用 REST API 直接执行载荷日志记录。

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

## 使用 Microsoft Azure 机器学习引擎
{: #cml-azconfig}

### 绑定 Microsoft Azure 机器学习引擎
{: #cml-azbind}

- 非 {{site.data.keyword.pm_full}} 引擎绑定为“定制”，意味着这只是元数据；没有任何与非 {{site.data.keyword.pm_full}} 服务的直接集成。

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
  您可以使用以下命令查看服务绑定：

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML 绑定](images/ml-azure-bind.png)

### 添加 MS Azure ML 预订
{: #cml-azsub}

- 添加预订

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- 获取预订列表

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### 启用载荷日志记录
{: #cml-azenlog}

- 在预订中启用载荷日志记录

    ```python
    subscription.payload_logging.enable()
    ```

- 获取日志记录详细信息

    ```python
    subscription.payload_logging.get_details()
    ```

### 评分和载荷日志记录
{: #cml-azscore}

- 对模型进行评分。有关完整示例，请参阅[使用 Azure Machine Learning Studio Engine 笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}。

- 在载荷日志记录表中存储请求和响应：

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **注意**：对于除 Python 以外的其他语言，您还可以使用 REST API 直接执行载荷日志记录。

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

## 使用 Amazon SageMaker 机器学习引擎
{: #cml-smconfig}

### 绑定 Amazon SageMaker 机器学习引擎
{: #cml-smbind}

- 非 {{site.data.keyword.pm_full}} 引擎绑定为“定制”，意味着这只是元数据；没有任何与非 {{site.data.keyword.pm_full}} 服务的直接集成。

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  您可以使用以下命令查看服务绑定：

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker ML 绑定](images/ml-sagemaker-bind.png)

### 添加 Amazon SageMaker ML 预订
{: #cml-smsub}

- 添加预订

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- 获取预订列表

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### 启用载荷日志记录
{: #cml-smenlog}

- 在预订中启用载荷日志记录

    ```python
    subscription.payload_logging.enable()
    ```

- 获取日志记录详细信息

    ```python
    subscription.payload_logging.get_details()
    ```

### 评分和载荷日志记录
{: #cml-smscore}

- 对模型进行评分。有关完整示例，请参阅[使用 SageMaker 机器学习引擎笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}。


- 在载荷日志记录表中存储请求和响应：

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **注意**：对于除 Python 以外的其他语言，您还可以使用 REST API 直接执行载荷日志记录。

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

## 后续步骤
{: #cml-next}

- 要继续使用 {{site.data.keyword.aios_short}} 客户机，请参阅[指定数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db)。

- 要继续使用 Python 命令库，请参阅 [Python 客户机文档](http://ai-openscale-python-client.mybluemix.net/){: external}。
