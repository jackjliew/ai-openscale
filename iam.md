---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"


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

## Identity and Access Management roles and actions

Access to {{site.data.keyword.aios_full}} service instances for users in your account is controlled by {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.aios_short}} service in your account must be assigned an access policy with an IAM role defined. The policy determines what actions a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.Bluemix_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

Policies enable access to be granted at different levels. Some of the options include the following: 

* Access across all instances of the service in your account
* Access to an individual service instance in your account
* Access to a specific resource within an instance

After you define the scope of the access policy, you assign a role which determines the user's level of access. Review the following tables which outline what actions each role allows within the {{site.data.keyword.aios_short}} service.

With platform management roles, users can be assigned varying levels of permission for performing platform actions within the account and on a service. For example, platform management roles that are assigned for catalog resources enable users to complete actions such as creating, deleting, editing, and viewing service instances. And, the platform management roles that are assigned for account management services enable users to complete actions such as inviting and removing users, working with resource groups, and viewing billing information. For more information about the account management services, see [Assigning access to account management services](/docs/iam?topic=iam-account-services#account-services).

Select all roles that apply when creating a policy. Each role allows separate actions to be completed and doesn't inherit the actions of the lesser roles.
{: tip}

The following table provides examples for some of the platform management actions that users can take within the context of catalog resources and resource groups. See the documentation for each catalog offering to understand how the roles apply to users within the context of the service that is being used.


|  | One or all IAM-enabled services | Selected service in a resource group | Selected resource group |
|:--------------|:------------|:-------------|:-------------|
| Viewer role | View instances, aliases, bindings, and credentials | View only specified instances in the resource group | View resource group |
| Operator role |  View instances and manage aliases, bindings, and credentials |  Not applicable | Not applicable |
| Editor role |  Create, delete, edit, and view instances. Manage aliases, bindings, and credentials | Create, delete, edit, suspend, resume, view, and bind only specified instances in the resource group | View and edit name of resource group |
| Administrator role |  All management actions for services | All management actions for the specified instances in the resource group | View, edit, and manage access for the resource group |
| Cluster administrator role (specific to {{site.data.keyword.wos4d_full}} only) |  Has complete access to IBM Cloud Private platform | Has complete access to the specified instances in the resource group | The following actions can be completed by the cluster administrator only: Connect to an LDAP directory, add users and assign them the IAM roles, manage workloads, infrastructure, and applications across all namespaces, create namespaces, assign quotas, add pod security policies, add an internal Helm repository, delete an internal Helm repository, add Helm charts to the internal Helm repository, remove Helm charts from the internal Helm repository, and synchronize internal and external Helm repositories |
{: row-headers}
{: class="comparison-table"}
{: caption="Table 1. Example platform management roles and actions for services in an account" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


For service access roles, which enable users access to {{site.data.keyword.aios_short}} as well as the ability to call the REST API, {{site.data.keyword.aios_short}} defers to the platform management roles that are listed in the preceding table. For information about assigning user roles in the UI, see [Managing access to resources](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

 