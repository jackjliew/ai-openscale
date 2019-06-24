---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: Microsoft Azure, ml, machine learning, services

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

# 指定 Microsoft Azure ML Studio 实例
{: #connect-azure}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定 Microsoft Azure ML Studio 实例。Azure ML Studio 实例是存储 AI 模型和部署的位置。
{: shortdesc}

## 连接 Azure ML Studio 实例
{: #ca-connect}

{{site.data.keyword.aios_short}} 连接到 Azure ML Studio 实例中的 AI 模型和部署。

1.  从 {{site.data.keyword.aios_short}} 工具的主页中，单击**开始**。

    ![主页](images/gs-config-start.png)

1.  选择 **Microsoft Azure ML Studio** 磁贴，然后单击**下一步**。

    ![选择 Azure ML Studio](images/connect-azure.png)

1.  输入凭证：

    请参阅 [How to: Use the portal to create an Azure AD application and service principal that can access resources ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window} 以了解有关如何获取 Microsoft Azure 凭证的指示信息。
    {: note}

    ![输入 Azure ML Studio 凭证](images/connect-azure-cred.png)

1.  单击**下一步**。

1.  {{site.data.keyword.aios_short}} 将列出已部署的模型；选择要监视的模型

    ![选择已部署的 MS Azure 模型](images/connect-azure-deploys.png)

1.  单击**下一步**。

### 后续步骤
{: #ca-next}

{{site.data.keyword.aios_short}} 现在可供您用于[指定数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db)。
