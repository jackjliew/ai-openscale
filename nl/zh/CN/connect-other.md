---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: machine learning, services, ml, custom 

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

# 指定定制 ML 服务实例
{: #co-connect}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定服务实例。服务实例是存储 AI 模型和部署的位置。
{: shortdesc}

## 连接定制服务实例
{: #co-config}

{{site.data.keyword.aios_short}} 连接到服务实例中的 AI 模型和部署。

1.  从 {{site.data.keyword.aios_short}} 工具的主页中，单击**开始**。

    ![主页](images/gs-config-start.png)

2.  选择**定制**磁贴，然后单击**下一步**。

    ![选择定制](images/connect-custom.png)

3.  通过选择以下选项之一来连接到部署：

    ![选择定制](images/connect-custom-deploy.png)

4.  如果选择了“输入个别评分端点”磁贴，请输入凭证：

    ![输入服务凭证](images/connect-custom-cred.png)

5.  单击**下一步**。

    - 如果选择了“输入个别评分端点”磁贴，那么必须提供部署名称和端点：

      ![输入服务凭证](images/connect-custom-endpoint.png)

      单击**下一步**。

    - 如果选择了“请求部署列表”磁贴，那么必须提供主机名或 IP 地址以及端口号：

      ![输入服务凭证](images/connect-custom-apiendpoint.png)

      单击**下一步**。

      然后，从部署列表中进行选择：

      ![输入服务凭证](images/connect-custom-apiendpoint2.png)

6.  查看所选部署。

    ![输入服务凭证](images/connect-custom-deploy2.png)

7.  单击**下一步**。

### 工作方式
{: #co-works}

此图像显示定制环境支持：

![定制的工作方式](images/custom-how-works.png)

您还可以参考以下链接：

[AIOS 载荷日志记录 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[定制部署 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[Python 客户机绑定 SDK ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[Working with Custom Machine Learning engine ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[Python SDK for IBM Watson OpenScale ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

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

  以上评分输出应当可从 {{site.data.keyword.aios_short}} 能够通过 REST 调用的实时评分端点进行访问。对于 AzureML、SageMaker 和 WML，{{site.data.keyword.aios_short}} 直接连接到本机评分端点，（因此您不必担心如何实施评分规范）

### 后续步骤
{: #co-next}

{{site.data.keyword.aios_short}} 现在可供您用于[指定数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db)。
