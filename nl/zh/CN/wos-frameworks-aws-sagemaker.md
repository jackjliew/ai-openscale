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

# Amazon SageMaker 框架
{: #frmwrks-aws-sage}

您可以使用 Amazon SageMaker 在 {{site.data.keyword.aios_full}} 中执行有效内容日志记录、反馈日志记录以及度量性能准确性、运行时偏差检测、可解释性和自动除偏功能。

{{site.data.keyword.aios_full}} 完全支持以下 Amazon SageMaker 框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| 本机 |分类| 结构化 |
| 本机 | 回归<sup>1</sup> | 结构化 |
{: caption="框架支持详细信息" caption-side="top"}

<sup>1</sup>对于回归模型的支持不包括漂移量级。

## 将 Amazon SageMaker 添加到 {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

您可以使用以下方法之一将 {{site.data.keyword.aios_short}} 配置为使用 Amazon SageMaker：

- 如果这是首次将机器学习提供程序添加到 {{site.data.keyword.aios_short}}，那么可以使用配置接口。有关更多信息，请参阅[指定 Amazon SageMaker 实例](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)。
- 您还可以使用 Python SDK 来添加机器学习提供程序。如果您希望具有多个提供程序，那么必须使用此方法。有关以编程方式执行此操作的更多信息，请参阅[绑定 Amazon SageMaker 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)。


## 样本笔记本
{: #frmwrks-aws-sage-smpl-ntbks}

以下笔记本显示如何使用 Amazon SageMaker：

- [创建和部署信用风险预测模型](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [数据集市创建、模型部署监视和数据分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## 指定 Amazon SageMaker ML 服务实例
{: #csm-connect}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定 Amazon SageMaker 服务实例。Amazon SageMaker 服务实例是存储 AI 模型和部署的位置。
{: shortdesc}

您还可以使用 Python SDK 来添加机器学习提供程序。有关以编程方式执行此操作的更多信息，请参阅[绑定 Amazon SageMaker 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)。

### 连接 Amazon SageMaker 服务实例
{: #csm-config}

{{site.data.keyword.aios_short}} 连接到 Amazon SageMaker 服务实例中的 AI 模型和部署。

1.  从导航窗格的**配置**选项卡中，单击**机器学习提供程序**。

    ![显示“选择机器学习服务提供程序”屏幕，其中包含受支持的机器学习引擎的磁贴](images/wos-machine-learning-providers-selection.png)

1.  单击**添加机器学习提供程序**按钮，然后单击 **Amazon SageMaker** 磁贴。

    ![输入 Amazon SageMaker 服务凭证](images/connect-sage-cred.png)

1.  输入并保存凭证：

    - 访问密钥标识：您的 AWS 访问密钥标识 `aws_access_key_id`，用于验证您的身份，并认证和授权您对 AWS 进行的呼叫。
    - 访问密钥：您的 AWS 访问密钥 `aws_secret_access_key`，需要此密钥才能验证您的身份，并认证和授权您对 AWS 进行的呼叫。
    - 区域：输入在其中创建了访问密钥标识的区域。密钥在其创建所在区域中进行存储和使用，并且不能转移到其他区域。

1.  {{site.data.keyword.aios_short}} 列出已部署模型；选择要监视的模型。

## 使用 Amazon SageMaker 机器学习引擎记录有效内容
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

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

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
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

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
{: #csm-next}

- {{site.data.keyword.aios_short}} 现在可供您用于[配置监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
- [使用 Watson OpenScale 监视 Sagemaker 机器学习](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
