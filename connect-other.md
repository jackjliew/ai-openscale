---

copyright:
  years: 2018
lastupdated: "2018-12-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Specify your Custom service
{: #connect-other}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify a service instance. Your service instance is where you store your AI models and deployments.
{: shortdesc}

## Connect your Custom service instance
{: #config-other}

{{site.data.keyword.aios_short}} connects to AI models and deployments in a service instance.

1.  From the home page of the {{site.data.keyword.aios_short}} tool, click **Begin**.

    ![Home page](images/gs-config-start.png)

1.  Select the **Custom** tile and click **Next**.

    ![Select custom](images/connect-custom.png)

1.  Connect to deployments by selecting one of the options:

    ![Select custom](images/connect-custom-deploy.png)

1.  Enter your credentials:

    ![Enter service credentials](images/connect-custom-cred.png)

1.  Click **Next**.

    - If you selected the "Enter individual scoring endpoints" tile, you must provide a deployment name and endpoint:

      ![Enter service credentials](images/connect-custom-endpoint.png)

      Click **Next**.

    - If you selected the "Request a list of deployments" tile, you must provide a hostname or IP address, and port number:

      ![Enter service credentials](images/connect-custom-apiendpoint.png)

      Click **Next**.

1.  Review your selected deployments.

    ![Enter service credentials](images/connect-custom-deploy2.png)

1.  Click **Next**.

### Next steps
{: #payload-logging}

{{site.data.keyword.aios_short}} is now ready for you to [specify your database](connect-db.html).
