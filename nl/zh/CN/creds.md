---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 创建凭证
{: #cred-create}

为访问 {{site.data.keyword.aios_short}} REST API，需要 Platform API 密钥和数据集市（服务实例）标识。通过该 Platform API 密钥，个人用户能够访问 {{site.data.keyword.cloud_notm}} 中的资源。

对于企业帐户，管理员可以创建数据集市，然后邀请其他用户进入该帐户，从而授予这些用户对特定 {{site.data.keyword.aios_short}} 数据集市的访问权。然后，用户可以创建其自己的 Platform API 密钥，并可访问同一 {{site.data.keyword.aios_short}} 数据集市；没有任何冲突或安全风险。

要创建 Platform API 密钥，请完成以下步骤：

- 登录到 [{{site.data.keyword.cloud_notm}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}){: new_window}。

- 选择**管理** --> **安全性** --> **Platform API 密钥**

    ![Platform API 密钥](images/cred-api-key.png)

- 创建并保存 Platform API 密钥。

要查找数据集市（或服务实例）标识，请执行以下操作：

- 在 {{site.data.keyword.aios_short}} **配置 --> 摘要**页面中，第一个条目即是数据集市（服务实例）标识。

    ![数据集市标识](images/data-mart-id.png)
