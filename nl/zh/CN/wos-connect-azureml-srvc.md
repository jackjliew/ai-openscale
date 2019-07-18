---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure ML service, ml, machine learning, services

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

# 指定 Microsoft Azure ML Service 实例
{: #connect-azureservice}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定 Microsoft Azure ML Service 实例。Azure ML Service 实例是存储 AI 模型和部署的位置。
{: shortdesc}

您还可以使用 Python SDK 来添加机器学习提供程序。有关以编程方式执行此操作的更多信息，请参阅[绑定 Microsoft Azure 服务机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)。

## 连接 Azure ML Service 实例
{: #ca-connect}

{{site.data.keyword.aios_short}} 连接到 Azure ML Service 实例中的 AI 模型和部署。

1.  从**配置**选项卡中，单击**机器学习提供程序**。
1.  单击 **Microsoft Azure ML Service** 磁贴。
1.  输入并保存凭证：

    - 客户机标识：客户机标识的实际字符串值，用于验证您的身份，并认证和授权您对 Azure Service 进行的呼叫。
    - 客户机私钥：私钥的实际字符串值，用于验证您的身份，并认证和授权您对 Azure Service 进行的呼叫。
    - 租户：租户标识与组织对应，并且是 Azure AD 的专用实例。要查找租户标识，请将鼠标悬停在帐户名称上以获取目录/租户标识，或者选择 Azure 门户网站中的 Azure Active Directory >“属性”>“目录标识”。
    - 预订标识：用于唯一识别 Microsoft Azure 预订的预订凭证。预订标识构成每个服务调用的 URI 的一部分。

    请参阅[操作方法：使用门户网站来创建能够访问资源的 Azure AD 应用程序和服务主体](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} 以了解有关如何获取 Microsoft Azure 凭证的指示信息。{: note}

1.  {{site.data.keyword.aios_short}} 列出已部署模型；选择要监视的模型，然后单击**配置**。

您已成功选择部署。

### 后续步骤
{: #ca-next}

{{site.data.keyword.aios_short}} 现在可供您用于[配置监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
