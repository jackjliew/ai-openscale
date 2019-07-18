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

# Microsoft Azure ML Service 框架
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} 完全支持以下 Microsoft Azure Machine Learning Service 框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| 本机 |分类| 结构化 |
| scikit-learn |分类| 结构化 |
| scikit-learn | 回归 | 结构化 |
{: caption="框架支持详细信息" caption-side="top"}

## 将 Microsoft Azure ML Service 添加到 {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

您可以使用以下方法之一将 {{site.data.keyword.aios_short}} 配置为使用 Microsoft Azure ML Service：

- 如果这是首次将机器学习提供程序添加到 {{site.data.keyword.aios_short}}，那么可以使用配置接口。有关更多信息，请参阅[指定 Microsoft Azure ML Service 实例](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)。
- 您还可以使用 Python SDK 来添加机器学习提供程序。如果您希望具有多个提供程序，那么必须使用此方法。有关以编程方式执行此操作的更多信息，请参阅[绑定 Microsoft Azure 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)。


{{site.data.keyword.aios_short}} 调用与 Azure ML Service 进行交互所需的各种 REST 端点。为此，必须绑定 Azure Machine Learning Service {{site.data.keyword.aios_short}}。

1. 创建 Azure Active Directory 服务主体。
2. 通过 UI 或 {{site.data.keyword.aios_short}} Python SDK 在创建 Azure ML Service 服务绑定时指定凭证详细信息。

## JSON 请求和响应文件的需求
{: #frmwrks-azureservice-JSON}

要使 {{site.data.keyword.aios_short}} 使用 Azure ML Service，您创建的 Web Service 部署必须满足特定需求。您创建的 Web Service 部署必须根据下面描述的需求来接受 JSON 请求并返回 JSON 响应。

### 必需 Web Service JSON 请求格式
{: #frmwrks-azureservice-JSON-sample-request}

- REST API 请求主体必须是包含 JSON 对象的一个 JSON 数组的 JSON 文档
- JSON 数组必须命名为 `"input"`。
- 每个 JSON 对象只能包含简单键/值对，其中值可以为字符串、数字、`true`、`false` 或 `null`
- 值不能为 JSON 对象或数组
- 无论是否有可用的非 `null` 值，数组中的每个 JSON 对象全都必须指定相同的键（和键数）


以下样本 JSON 文件满足上述需求，并可用作用于创建您自己的 JSON 请求文件的模板：


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


### 必需 Web Service JSON 响应格式
{: #frmwrks-azureservice-JSON-sample-response}

创建 JSON 请求文件时，请注意以下事项：

- REST API 响应主体必须是包含 JSON 对象的一个 JSON 数组的 JSON 文档
- JSON 数组必须命名为 `"output"`。
- 每个 JSON 对象只能包含键/值对，其中值可以为字符串、数字、`true`、`false`、`null` 或者不含任何其他 JSON 对象或数组的数组
- 值不能为 JSON 对象
- 无论是否有可用的非 `null` 值，数组中的每个 JSON 对象全都必须指定相同的键（和键数）
- 对于分类模型：Web Service 必须为每个类返回概率数组，并且概率的排序对于数组中的每个 JSON 对象必须一致
  - 例如：假设您具有一个用于预测信用风险的二元分类模型，其中类为 `Risk` 或 `No Risk`
  - 对于“output”数组中返回的每个结果，对象必须包含键/值对，其中含有固定顺序的概率，格式如下：
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

要与 Azure ML Studio 和 Service 中使用的 Azure ML 可视工具一致，建议使用以下键名（虽然不要求）：

- 针对表示模型的预测值的输出键使用键名 `"Scored Labels"`
- 针对表示每个类的概率数组的输出键使用键名 `"Scored Probabilities"`

以下样本 JSON 文件满足上述需求，并可用作用于创建您自己的 JSON 响应文件的模板：


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

## 样本笔记本
{: #frmwrks-azureservice-smpl-ntbks}

以下笔记本显示如何使用 Microsoft Azure ML Service：

- [数据集市创建、模型部署监视和数据分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure 服务模型评分示例](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 深入探索
{: #frmwrks-azureservice-mediumblogs}

- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
