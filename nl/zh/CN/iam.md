---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## 身份和访问管理角色和操作

对您帐户中用户的 {{site.data.keyword.aios_full}} 服务实例的访问权由 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 控制。必须为访问您帐户中的 {{site.data.keyword.aios_short}} 服务的每个用户分配一个定义了 IAM 角色的访问策略。该策略确定用户可以在您选择的服务或实例的上下文中执行的操作。允许的操作由 {{site.data.keyword.Bluemix_notm}} 服务进行定制，并定义为允许在服务上执行的操作。然后，这些操作将映射到 IAM 用户角色。

策略支持在不同级别授予访问权。其中一些选项包括： 

* 对帐户中所有服务实例的访问权
* 对帐户中个别服务实例的访问权
* 对实例中特定资源的访问权

定义访问策略的作用域后，您可分配一个角色，用于确定用户的访问级别。复查下表，其中概述每个角色在 {{site.data.keyword.aios_short}} 服务中允许的操作。

下表详述映射到平台管理角色的操作。平台管理角色支持用户在平台级别对服务资源执行任务，例如为用户分配对服务的访问权，创建或删除实例，以及将实例绑定到应用程序。

| 平台管理角色 | 操作描述 | 示例操作                                                 |
|--------------------------|------------------------|-----------------------------------------------------------------|
| 查看者                   |描述| <ul><li>示例 1</li><li>示例 2</li></ul>                   |
| 编辑者                   |描述|<ul><li>示例 1</li><li>示例 2</li></ul>                    |
| 操作员                   |描述| <ul><li>示例 1</li><li>示例 2</li><li>示例 3</li></ul> |
| 管理员                   |描述|<ul><li>示例 1</li><li>示例 2</li><li>示例 3</li></ul>  |
{: caption="表 1. IAM 用户角色和操作" caption-side="top"}


下表详述映射到服务访问角色的操作。服务访问角色支持用户访问 {{site.data.keyword.aios_short}}，以及能够调用 {{site.data.keyword.aios_short}} API。

| 服务访问角色 | 操作描述 | 示例操作                                                 |
|---------------------|------------------------|-----------------------------------------------------------------|
| 读取者                |描述| <ul><li>示例 1</li><li>示例 2</li></ul>                   |
| 写入者                |描述|<ul><li>示例 1</li><li>示例 2</li></ul>                    |
| 管理者              |描述| <ul><li>示例 1</li><li>示例 2</li><li>示例 3</li></ul> |
{: caption="表 2. IAM 服务访问角色和操作" caption-side="top"}


有关在 UI 中分配用户角色的信息，请参阅[管理对资源的访问权](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)。

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
