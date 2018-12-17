---

copyright:
  years: 2018
lastupdated: "2018-12-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Specify your Azure ML service
{: #connect-azure}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify a Microsoft Azure ML service instance. Your Azure ML service instance is where you store your AI models and deployments.
{: shortdesc}

## Connect your Azure ML service instance
{: #config-azure}

{{site.data.keyword.aios_short}} connects to AI models and deployments in a Azure ML service instance.

1.  From the home page of the {{site.data.keyword.aios_short}} tool, click **Begin**.

    ![Home page](images/gs-config-start.png)

1.  Select the **Microsoft Azure** tile and click **Next**.

    ![Select Azure ML service](images/connect-azure.png)

1.  Enter your credentials:

    See [How to: Use the portal to create an Azure AD application and service principal that can access resources ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal) for instructions about how to get your Microsoft Azure credentials.
    {: note}

    ![Enter Azure ML service credentials](images/connect-azure-cred.png)

1.  Click **Next**.

1.  {{site.data.keyword.aios_short}} will list your deployed models; select the ones you want to monitor

    ![Select MS Azure deployed models](images/connect-azure-deploys.png)

1.  Click **Next**.

### Next steps
{: #payload-logging}

{{site.data.keyword.aios_short}} is now ready for you to [specify your database](connect-db.html).
