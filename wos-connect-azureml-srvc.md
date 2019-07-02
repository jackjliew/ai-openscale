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

# Specifying a Microsoft Azure ML Service instance
{: #connect-azureservice}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify a Microsoft Azure ML Service instance. Your Azure ML Service instance is where you store your AI models and deployments.
{: shortdesc}

You can also add your machine learning provider by using the Python SDK. For more information on performing this programmatically, see [Bind your Microsoft Azure Service machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Connect your Azure ML Service instance
{: #ca-connect}

{{site.data.keyword.aios_short}} connects to AI models and deployments in a Azure ML Service instance.

1.  From the **Configure** tab, click **Machine learning provider**.
1.  Click the **Microsoft Azure ML Service** tile.
1.  Enter and save your credentials:

    - Client ID: The actual string value of your client ID, which verifies who you are and authenticates and authorizes calls that you make to Azure Service.
    - Client Secret: The actual string value of the secret, which verifies who you are and authenticates and authorizes calls that you make to Azure Service.
    - Tenant: Your tenant ID corresponds to your organization and is a dedicated instance of Azure AD. To find the tenant ID, hover over your account name to get the directory / tenant ID, or select Azure Active Directory > Properties > Directory ID in the Azure portal.
    - Subscription ID: Subscription credentials which uniquely identify your Microsoft Azure subscription. The subscription ID forms part of the URI for every service call.

    See [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} for instructions about how to get your Microsoft Azure credentials.
    {: note}

1.  {{site.data.keyword.aios_short}} lists your deployed models; select the ones you want to monitor and click **Configure**.

You have successfully selected deployments.

### Next steps
{: #ca-next}

{{site.data.keyword.aios_short}} is now ready for you to [configure monitors](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
