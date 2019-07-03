---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# 指定 Amazon SageMaker ML 服务实例
{: #csm-connect}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定 Amazon SageMaker 服务实例。Amazon SageMaker 服务实例是存储 AI 模型和部署的位置。
{: shortdesc}

您还可以使用 Python SDK 来添加机器学习提供程序。有关以编程方式执行此操作的更多信息，请参阅[绑定 Amazon SageMaker 机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)。

## 连接 Amazon SageMaker 服务实例
{: #csm-config}

{{site.data.keyword.aios_short}} 连接到 Amazon SageMaker 服务实例中的 AI 模型和部署。

1.  从 {{site.data.keyword.aios_short}} 工具的主页中，单击**开始**。

    ![主页](images/gs-config-start.png)

1.  选择 **Amazon SageMaker** 磁贴，然后单击**下一步**。

    ![选择 Amazon SageMaker 服务](images/connect-sage.png)

1.  输入凭证：

    - 访问密钥标识：您的 AWS 访问密钥标识 `aws_access_key_id`，用于验证您的身份，并认证和授权您对 AWS 进行的呼叫。
    - 访问密钥：您的 AWS 访问密钥 `aws_secret_access_key`，需要此密钥才能验证您的身份，并认证和授权您对 AWS 进行的呼叫。
    - 区域：输入在其中创建了访问密钥标识的区域。密钥在其创建所在区域中进行存储和使用，并且不能转移到其他区域。

    ![输入 Amazon SageMaker 服务凭证](images/connect-sage-cred.png)

1.  单击**下一步**。

1.  {{site.data.keyword.aios_short}} 将列出已部署的模型；选择要监视的模型

    ![选择已部署的 Amazon SageMaker 模型](images/connect-sage-deploys.png)

1.  单击**下一步**。

### 后续步骤
{: #csm-next}

{{site.data.keyword.aios_short}} 现在可供您用于[指定数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db)。
