---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# 使用 Microsoft Azure ML Service 引擎记录有效内容
{: #cml-azsrvconfig}

## 绑定 Microsoft Azure ML Service 引擎
{: #cml-azsrvbind}

非 {{site.data.keyword.pm_full}} 引擎绑定为“定制”，意味着这只是元数据；没有任何与非 {{site.data.keyword.pm_full}} 服务的直接集成。
   
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

您可以使用以下命令查看服务绑定：

```
    client.data_mart.bindings.list()
    ```
{: codeblock}

样本输出：

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
## 添加 Microsoft Azure ML Service 预订
{: #cml-azsrvsub}

添加预订

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

获取预订列表

```
    subscriptions = client.data_mart.subscriptions.get_details()subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```
{: codeblock}

## 启用载荷日志记录
{: #cml-azsrvenlog}

在预订中启用载荷日志记录

```
    subscription.payload_logging.enable()
    ```
{: codeblock}

获取日志记录详细信息

```
    subscription.payload_logging.get_details()
    ```
{: codeblock}

## 评分和载荷日志记录
{: #cml-azsrvscore}

对模型进行评分。有关完整示例，请参阅[使用 Azure Machine Learning Service 引擎笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}。

在载荷日志记录表中存储请求和响应：

```
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))subscription.payload_logging.store(records=records_list)
    ```
{: codeblock}
{: python}
   
对于除 Python 以外的其他语言，您还可以使用 REST API 直接执行有效内容日志记录。
   
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

