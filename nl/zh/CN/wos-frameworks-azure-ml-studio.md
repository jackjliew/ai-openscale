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

# Microsoft Azure ML Studio 框架
{: #frmwrks-azure}

您可以使用 Microsoft Azure ML Studio 在 {{site.data.keyword.aios_full}} 中执行有效内容日志记录、反馈日志记录以及度量性能准确性、运行时偏差检测、可解释性和自动除偏功能。

{{site.data.keyword.aios_full}} 完全支持以下 Microsoft Azure Machine Learning Studio 框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| 本机 |分类| 结构化 |
| 本机 | 回归 | 结构化 |
{: caption="框架支持详细信息" caption-side="top"}

## 将 Microsoft Azure ML Studio 添加到 {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

您可以使用以下方法之一将 {{site.data.keyword.aios_short}} 配置为使用 Microsoft Azure ML Studio：

- 如果这是首次将机器学习提供程序添加到 {{site.data.keyword.aios_short}}，那么可以使用配置接口。有关更多信息，请参阅[指定 Microsoft Azure ML Studio 实例](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)。
- 您还可以使用 Python SDK 来添加机器学习提供程序。如果您希望具有多个提供程序，那么必须使用此方法。有关以编程方式执行此操作的更多信息，请参阅[绑定 Microsoft Azure 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)。


## 样本笔记本
{: #frmwrks-azure-smpl-ntbks}

以下笔记本显示如何使用 Microsoft Azure ML Studio：

- [数据集市创建、模型部署监视和数据分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure 服务模型评分示例](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 深入探索
{: #frmwrks-azure-mediumblogs}

-[使用 Watson OpenScale 监视 Azure Machine Learning](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Consume an Azure Machine Learning model deployed as a web service](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## 指定 Microsoft Azure ML Studio 实例
{: #connect-azure}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定 Microsoft Azure ML Studio 实例。Azure ML Studio 实例是存储 AI 模型和部署的位置。
{: shortdesc}

您还可以使用 Python SDK 来添加机器学习提供程序。有关以编程方式执行此操作的更多信息，请参阅[绑定 Microsoft Azure 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)。

### 连接 Azure ML Studio 实例
{: #ca-connect}

{{site.data.keyword.aios_short}} 连接到 Azure ML Studio 实例中的 AI 模型和部署。

1.  从导航窗格的**配置**选项卡中，单击**机器学习提供程序**。

    ![显示“选择机器学习服务提供程序”屏幕，其中包含受支持的机器学习引擎的磁贴](images/wos-machine-learning-providers-selection.png)

1.  单击**添加机器学习提供程序**按钮，然后单击 **Microsoft Azure ML Studio** 磁贴。

    ![输入 Azure ML Studio 凭证](images/connect-azure-cred.png)

1.  输入并保存凭证：

    - 客户机标识：客户机标识的实际字符串值，用于验证您的身份，并认证和授权您对 Azure Studio 进行的呼叫。
    - 客户机私钥：私钥的实际字符串值，用于验证您的身份，并认证和授权您对 Azure Studio 进行的呼叫。
    - 租户：租户标识与组织对应，并且是 Azure AD 的专用实例。要查找租户标识，请将鼠标悬停在帐户名称上以获取目录/租户标识，或者选择 Azure 门户网站中的 Azure Active Directory >“属性”>“目录标识”。
    - 预订标识：用于唯一识别 Microsoft Azure 预订的预订凭证。预订标识构成每个服务调用的 URI 的一部分。

    请参阅[操作方法：使用门户网站来创建能够访问资源的 Azure AD 应用程序和服务主体](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} 以了解有关如何获取 Microsoft Azure 凭证的指示信息。{: note}

1.  {{site.data.keyword.aios_short}} 列出已部署模型；选择要监视的模型，然后单击**配置**。

您已成功选择部署。

## 使用 Microsoft Azure Machine Learning Studio 引擎记录有效内容
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

    binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  您可以使用以下命令查看服务绑定：

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML 绑定](images/ml-azure-bind.png)

### 添加 Microsoft Azure ML Studio 预订
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
{: #ca-next}

{{site.data.keyword.aios_short}} 现在可供您用于[配置监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
