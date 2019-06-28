---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure, ml, machine learning, services

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

# Specifying a Microsoft Azure ML Studio instance
{: #connect-azure}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify a Microsoft Azure ML Studio instance. Your Azure ML Studio instance is where you store your AI models and deployments.
{: shortdesc}

You can also add your machine learning provider by using the Python SDK. For more information on performing this programmatically, see [Bind your Microsoft Azure machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

## Connect your Azure ML Studio instance
{: #ca-connect}

{{site.data.keyword.aios_short}} connects to AI models and deployments in a Azure ML Studio instance.

1.  From the home page of the {{site.data.keyword.aios_short}} tool, click **Begin**.

    ![Home page](images/gs-config-start.png)

1.  Select the **Microsoft Azure ML Studio** tile and click **Next**.

    ![Select Azure ML Studio](images/connect-azure.png)

1.  Enter your credentials:

    - Client ID: The actual string value of your client ID, which verifies who you are and authenticates and authorizes calls that you make to Azure Studio.
    - Client Secret: The actual string value of the secret, which verifies who you are and authenticates and authorizes calls that you make to Azure Studio.
    - Tenant: Your tenant ID corresponds to your organization and is a dedicated instance of Azure AD. To find the tenant ID, hover over your account name to get the directory / tenant ID, or select Azure Active Directory > Properties > Directory ID in the Azure portal.
    - Subscription ID: Subscription credentials which uniquely identify your Microsoft Azure subscription. The subscription ID forms part of the URI for every service call.

    See [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} for instructions about how to get your Microsoft Azure credentials.
    {: note}

    ![Enter Azure ML Studio credentials](images/connect-azure-cred.png)

1.  Click **Next**.

1.  {{site.data.keyword.aios_short}} will list your deployed models; select the ones you want to monitor

    ![Select MS Azure deployed models](images/connect-azure-deploys.png)

1.  Click **Next**.

### Next steps
{: #ca-next}

{{site.data.keyword.aios_short}} is now ready for you to [specify your database](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db).
