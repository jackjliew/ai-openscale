---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


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

通过平台管理角色，可以为用户分配各种不同级别的许可权，以在帐户中和服务上执行平台操作。例如，为目录资源分配的平台管理角色使用户能够完成诸如创建、删除、编辑和查看服务实例之类的操作。并且，为帐户管理服务分配的平台管理角色使用户能够完成诸如邀请和移除用户、使用资源组以及查看计费信息之类的操作。有关帐户管理服务的更多信息，请参阅[分配对帐户管理服务的访问权](/docs/iam?topic=iam-account-services#account-services){: external}。

选择创建策略时应用的所有角色。每个角色允许完成不同的操作，并且不会继承次要角色的操作。
{: tip}

下表提供用户在目录资源和资源组的上下文中可以采取的一些平台管理操作的示例。请参阅每个目录产品的文档，以了解这些角色如何在所使用的服务上下文中应用于用户。


|  | 一个或所有已启用 IAM 的服务 | 资源组中的所选服务 | 所选资源组 |
|:--------------|:------------|:-------------|:-------------|
| 查看者角色 | 查看实例、别名、绑定和凭证 | 仅查看资源组中的指定实例 | 查看资源组 |
| 操作员角色  | 查看实例并管理别名、绑定和凭证 | 不适用 | 不适用 |
| 编辑者角色 | 创建、删除、编辑和查看实例。管理别名、绑定和凭证 | 仅创建、删除、编辑、暂挂、恢复、查看和绑定资源组中的指定实例 | 查看和编辑资源组的名称 |
| 管理员角色  | 服务的所有管理操作 | 资源组中指定实例的所有管理操作 | 查看、编辑和管理资源组的访问权 |
| 集群管理员角色（仅特定于 {{site.data.keyword.wos4d_full}}）| 具有 IBM Cloud Private 平台的完整访问权 | 具有资源组中指定实例的完整访问权 | 以下操作只能由集群管理员来完成：连接到 LDAP 目录，添加用户并为其分配 IAM 角色，跨所有名称空间管理工作负载、基础结构和应用程序，创建名称空间，分配配额，添加 pod 安全策略，添加内部 Helm 存储库，删除内部 Helm 存储库，将 Helm chart 添加到内部 Helm 存储库，从内部 Helm 存储库中移除 Helm chart，以及同步内部和外部 Helm 存储库 |
{: row-headers}
{: class="comparison-table"}
{: caption="表 1. 帐户中的服务的示例平台管理角色和操作" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


对于支持用户访问 {{site.data.keyword.aios_short}} 以及能够调用 REST API 的服务访问角色，{{site.data.keyword.aios_short}} 遵从上表中所列的平台管理角色。有关在 UI 中分配用户角色的信息，请参阅[管理对资源的访问权](/docs/iam?topic=iam-iammanidaccser#iammanidaccser){: external}。

 
