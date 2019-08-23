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

# 定制 ML 框架
{: #frmwrks-custom}

您可以使用定制机器学习框架在 {{site.data.keyword.aios_full}} 中执行有效内容日志记录、反馈日志记录以及度量性能准确性、运行时偏差检测、可解释性和自动除偏功能。定制机器学习框架必须相当于 {{site.data.keywor.pm_full}}。

{{site.data.keyword.aios_full}} 完全支持以下定制机器学习框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| 等同于 {{site.data.keyword.pm_full}} |分类| 结构化 |
{: caption="框架支持详细信息" caption-side="top"}

## 将定制机器学习引擎添加到 {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

您可以使用以下方法之一将 {{site.data.keyword.aios_short}} 配置为使用定制机器学习提供程序：

- 如果这是首次将定制机器学习提供程序添加到 {{site.data.keyword.aios_short}}，那么可以使用配置接口。有关更多信息，请参阅[指定定制机器学习实例](/docs/services/ai-openscale?topic=ai-openscale-co-connect)。
- 您还可以使用 Python SDK 来添加机器学习提供程序。如果您希望具有多个提供程序，那么必须使用此方法。有关以编程方式执行此操作的更多信息，请参阅[绑定定制机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)。


## 样本笔记本
{: #frmwrks-custom-smpl-ntbks}

- [使用 Kubernetes 集群创建定制机器学习引擎](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [数据集市创建、模型部署监视和数据分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## 深入探索
{: #frmwrks-custom-mediumblogs}

[使用 Watson OpenScale 监视定制机器学习引擎](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}

## 定制机器学习引擎
{: #fmrk-workaround-customengine}

定制机器学习引擎为机器学习模型和 Web 应用程序提供基础结构和托管功能。{{site.data.keyword.aios_short}} 支持的定制机器学习引擎必须符合以下需求：

- 公开两种类型的 REST API 端点：

   * 发现端点（执行 GET 操作以获取部署和详细信息的列表）
   * 评分端点（在线和实时评分）

- 所有端点需要兼容 Swagger 规范才能受支持。

- 以部署作为目标或来源的输入有效内容和输出必须符合规范中描述的 JSON 文件格式。

目前，仅支持 `BasicAuth` 或 `none` 格式。
{: Note}

以下示例显示 REST API 端点规范：

![从 Swagger 文档中显示 REST API 端点规范](images/wosdeployments.png)


以下示例显示输入有效内容的格式：

![显示输入有效内容示例](images/wosinputdata.png)


## 定制机器学习引擎何时是我的最佳选项？
{: #fmrk-workaround-enging-choice}

当以下情况成立时，定制机器学习引擎是最佳选项：

- 您不是使用任何可用的现成产品来为机器学习模型提供服务。您只是开发了自己的系统来执行此操作。{{site.data.keyword.aios_short}} 中没有且将来也不会有与此对应的直接支持。
- {{site.data.keyword.aios_short}} 尚不支持您使用的来自第三方供应商的服务引擎。在此情况下，请考虑开发定制机器学习引擎作为原始或本机部署的包装器。

## 指定定制 ML 服务实例
{: #co-connect}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定服务实例。服务实例是存储 AI 模型和部署的位置。
{: shortdesc}

## 连接定制服务实例
{: #co-config}

{{site.data.keyword.aios_short}} 连接到服务实例中的 AI 模型和部署。您可以连接定制服务

1.  从导航窗格的**配置**选项卡中，单击**机器学习提供程序**。

   ![显示“选择机器学习服务提供程序”屏幕，其中包含受支持的机器学习引擎的磁贴](images/wos-machine-learning-providers-selection.png)

2. 单击**添加机器学习提供程序**按钮，然后单击**定制环境**磁贴。

   ![显示定制机器学习提供程序配置屏幕，其中包含表示凭证、实例名称和描述的字段](images/ml-custom-provider.png)

3. 输入定制机器学习提供程序的名称和描述，然后单击**下一步**。 

4. 选择[通过请求列表](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list)还是[通过输入个别评分端点](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints)来连接到部署。

   ![显示“连接到部署”屏幕，其中包含用于请求部署列表或输入个别评分端点的选项](images/ml-custom-connect-deployments.png)
    
5. 单击**下一步**。

### 请求部署列表
{: #co-config-request-list}

1. 如果选择了**请求部署列表**磁贴，请输入凭证和 API 端点，然后单击**保存**。

   ![显示部署列表屏幕，其中包含用于输入服务凭证和 API 端点的字段](images/connect-custom-cred.png)

2. 保存机器学习设置后，返回到**仪表板**，单击**洞察**选项卡，然后单击**添加到仪表板**按钮。

3. 从列表中选择部署，然后单击**配置**。

现在，您即可配置监视器。

### 提供个别评分端点
{: #co-config-scoring-endpoints}

1. 如果选择了**输入个别评分端点**磁贴，请输入 API 端点的凭证，然后单击**保存**。

2. 保存机器学习设置后，返回到**仪表板**，单击**洞察**选项卡，然后单击**添加到仪表板**按钮。

3. 单击**添加端点**按钮。

4. 从下拉菜单中，选择定制环境，输入部署名称和 API 端点，然后单击**保存**。

现在，您即可配置监视器。

### 工作方式
{: #co-works}

以下图像显示定制环境支持：

![显示“定制工作方式”图表。它显示包含客户机 API 和 Watson OpenScale API 的定制环境的对应框](images/custom-how-works.png)

您还可以参考以下链接：

[{{site.data.keyword.aios_short}} 有效内容日志记录 API](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[定制部署 API](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[Python 客户机绑定 SDK](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[使用定制机器学习引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[Python SDK for IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **模型的用于支持监视器的输入条件**

  模型应将特征向量作为输入，它本质上是命名字段及其值的集合（其中一个字段是针对偏差进行监视的字段）：

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

  在此示例中，`“age”`可能是某人用于评估公平性的字段。

  如果输入是从输入特征空间变换而来的张量/矩阵（在文本或图像的深度学习中通常情况如此），那么该模型无法由当前发行版中的 {{site.data.keyword.aios_short}} 平台来处理。通过扩展，无法处理具有文本或图像输入的深度学习模型以进行偏差检测和缓解。

  此外，还应装入训练数据以支持可解释性。

  要获取文本的可解释性，其中一个特征应是全文。在当前发行版中不支持定制模型的图像的可解释性。
  {: note}

- **模型的用于支持监视器的输出条件**

  模型应将输入特征向量随该模型中各种类的预测概率一起输出。

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

  在此示例中，`“personal”`和`“camping”`是可能的类，并且每个评分输出中的分数会分配给这两个类。如果缺少预测概率，那么偏差检测将起作用，但自动除偏不会起作用。

  以上评分输出应当可从 {{site.data.keyword.aios_short}} 能够通过 REST 调用的实时评分端点进行访问。对于 AzureML、SageMaker 和 {{site.data.keyword.pm_full}}，{{site.data.keyword.aios_short}} 直接连接到本机评分端点（因此您不必担心如何实施评分规范）。

## 定制机器学习引擎示例
{: #fmrk-workaround-cstmmlsengex}

使用以下示例来设置您自己的定制机器学习引擎。
{: shortdesc}

### Python 和 Flask
{: #fmrk-workaround-pandflask}

[git 上发布的定制 ML 引擎示例](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}使用 Python 和 Flask 来为 scikit-learn 模型提供服务。

[自述文件](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}描述如何能够在本地部署该应用程序以进行测试，以及如何在 IBM Cloud 上部署 cf 应用程序。可以在 [app.py 文件](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py){: external}中找到 REST API 端点的实施。

### Node.js
{: #fmrk-workaround-nodejs}

您还可以在[此处](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs){: external}找到以 Node.js 编写的定制机器学习引擎的示例。

### End2end 代码模式
{: #fmrk-workaround-e2ecode}

显示定制引擎部署的 end2end 示例以及与 {{site.data.keyword.aios_short}} 的集成的[代码模式](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale){: external}。

## 使用定制机器学习引擎记录有效内容
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

有关更多信息，请参阅[有效内容日志记录](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)。

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


## 后续步骤
{: #fmrk-workaround-nxt-steps-over}

{{site.data.keyword.aios_short}} 现在可供您用于[配置监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。

通过使用其中一个[定制机器学习示例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)来实施您自己的解决方案。
