---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: credentials, REST API, data mart

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

# 为 {{site.data.keyword.aios_short}} 创建凭证
{: #cred-create}

要访问 {{site.data.keyword.aios_full}} REST API，需要平台 API 密钥和数据集市（也称为服务实例）标识。通过该 Platform API 密钥，个人用户能够访问 {{site.data.keyword.cloud_notm}} 中的资源。
{: shortdesc}

对于企业帐户，管理员可以创建数据集市，邀请用户进入帐户，并为这些用户提供对特定 {{site.data.keyword.aios_short}} 数据集市的访问权。然后，用户可以创建其自身平台的 API 密钥，并可访问同一 {{site.data.keyword.aios_short}} 数据集市。没有任何冲突或安全风险。

## 创建平台 API 秘钥
{: #cred-create-apikey}

要创建 Platform API 密钥，请完成以下步骤：

- 登录到 [{{site.data.keyword.cloud_notm}}](https://{DomainName}){: external}。

- 选择**管理** --> **安全性** --> **Platform API 密钥**

    ![Platform API 密钥](images/cred-api-key.png)

- 创建并保存 Platform API 密钥。

要查找数据集市（或服务实例）标识，请执行以下操作：

- 在 {{site.data.keyword.aios_short}} **配置 --> 摘要**页面中，第一个条目即是数据集市（服务实例）标识。

    ![数据集市标识](images/data-mart-id.png)

## 使用命令控制台创建服务实例凭证
{: #cred-creds}

要为 {{site.data.keyword.aios_short}} 创建凭证，请使用 {{site.data.keyword.cloud_notm}} [命令控制台](/docs/cli?topic=cloud-cli-ibmcloud-cli)完成以下步骤：

1. 通过运行以下命令来检索 API 密钥：

    ```curl
    ibmcloud login --sso
    ibmcloud iam api-key-create 'my_key'
    ```

    将显示以下信息：

    ```bash
    Name         my_key
    Created At   2018-10-09T14:04+0000
    API Key      Tg4Gxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxQU-nE
    Locked       false
    UUID         ApiKey-xxxxxxxxx-afd7-xxxxx-b0e1-xxxxxxxxxxx
    ```
2. 验证您在 {{site.data.keyword.cloud_notm}} 帐户中使用的资源组。

  ![云中的资源组](images/cloud-resource.png)

  如果未在使用 `Default` 资源组，那么运行以下命令来获取 {{site.data.keyword.aios_short}} 的凭证：

   ```curl
   ibmcloud target -g myResourceGroup
   ```

  其中，`myResourceGroup` 是与 {{site.data.keyword.aios_short}} 实例关联的资源组的名称。

3. 通过运行以下命令来检索 {{site.data.keyword.aios_short}} 实例标识：

    ```curl
    ibmcloud resource service-instance '<Your_Watson_OpenScale_instance_name>'
    ```
    **注**：如果您是在 Windows 上使用 {{site.data.keyword.cloud_notm}} 命令控制台，请将以上命令中的单引号 (') 替换为双引号 (")。

    将显示以下信息：

    ```bash
    Name:                  AI OpenScale-my_instance
    ID:                    crn:v1:ibmcloud:public:aiopenscale:us-south:a/c2f2xxxxxxxxxxxx867::
    GUID:                  03daxxxx-xxxx-xxxx-xxxx-xxxxxxxx38a7
    Location:              us-south
    Service Name:          aiopenscale
    Service Plan Name:     lite
    Resource Group Name:   Default
    State:                 active
    Type:                  service_instance
    Sub Type:
    Tags:
    Created at:            2018-09-17T13:58:43Z
    Updated at:
    ```

    `GUID` 值是您的 {{site.data.keyword.aios_short}} 实例标识。
        
## 后续步骤
{: #cred-create-next-steps}

指定机器学习提供程序：

- [指定 IBM Watson Machine Learning 服务实例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-wml-connect)
- [指定 Microsoft Azure ML Studio 实例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-connect-azure)
- [指定 Amazon SageMaker ML 服务实例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-csm-connect)
- [指定定制 ML 服务实例](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-co-connect)
