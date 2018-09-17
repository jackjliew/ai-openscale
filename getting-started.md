---

copyright:
  years: 2015, 2018
lastupdated: "2018-9-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Getting started
{: #gettingstarted}

This topic provides reference material and first steps to help you get started using {{site.data.keyword.aios_full}}.
{: shortdesc}

## Complete the tutorial (recommended)
{: #gs-tutorial}

A full list of prerequisites, along with step-by-step instructions for provisioning {{site.data.keyword.Bluemix_notm}} machine learning and data services, creating and deploying machine learning models, and configuring the new {{site.data.keyword.aios_full}} service to monitor your models for trust and transparency, can be [found in the tutorial](tutorial.html).

## Manual configuration
{: #gs-prereqs}

The following steps outline the process required to configure {{site.data.keyword.aios_short}} using your own data and models. It is recommended that you [complete the tutorial[(tutorial.html) to become familiar with the process. ***At a minimum***, you will need:

1.  An {{site.data.keyword.aios_short}} service instance.

    - Go to the [{{site.data.keyword.aios_short}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/ai-openscale) page in the {{site.data.keyword.Bluemix_notm}} Catalog.

    - Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in with an existing account.

    - Click **Create**.

1.  A PostgreSQL database connected to your {{site.data.keyword.Bluemix_notm}} account.

    **Note**: For the current release, only a PostgreSQL database is supported.

    **Note**: The PostgreSQL database must be present in the same {{site.data.keyword.Bluemix_notm}} account as the {{site.data.keyword.aios_short}} instance.

    - To provision a new PostgreSQL database instance, access the [**Compose for PostgreSQL** landing page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/compose-for-postgresql) in {{site.data.keyword.Bluemix_notm}}.

1.  A Watson Machine Learning (WML) service instance connected to your {{site.data.keyword.Bluemix_notm}} account.

    **Note**: For the current release, only the Watson Machine Learning framework is supported.

    **Note**: The WML service instance must be present in the same {{site.data.keyword.Bluemix_notm}} account as the {{site.data.keyword.aios_short}} instance.

    - To provision a new Watson Machine Learning service instance, access the [**Machine Learning** landing page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/machine-learning) in {{site.data.keyword.Bluemix_notm}}.

1.  An AI model, deployed in the WML service instance, in production.

    - The model can be any type (Spark ML, Deep learning, etc.), and should have an output schema defined.

    - The model training data must be available in either Cloud Object Storage, or in Db2. Access to the training data is not mandatory, but without it you will not be able to configure bias checking. See [Configuring the Fairness monitor](monitor-fairness.html#config-fair) for more details.

    - If the model is accepting structured data as input, the model training data must be available in either Cloud Object Storage, or in Db2 for explainability to work. See [Configuring the Explainability monitor](monitor-explain.html#config-explain)

    - If your model is deployed in any serve environment other than WML, you must wrap the scoring endpoint of the model in a Python function, and deploy this Python function in WML. You will also need to have the training data of your model available in Db2 or Cloud Object Storage to monitor bias for your model. Explainability and accuracy is not supported for Python functions. See more information in the [AI OpenScale Python client documentation](http://ai-openscale-python-client.mybluemix.net/).

## Step 1: Specify your database
{: #gs-config-db}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify a database. This is the database that {{site.data.keyword.aios_short}} uses to store payload, feedback, and measurement data.

You will also select a schema for your database. A schema is a named collection of tables in the database.

1.  From the home page of the {{site.data.keyword.aios_short}} tool, click **Begin**.

    ![Home page](images/gs-config-start.png)

1.  Select a database from the **Database** drop-down menu.

    ![Select database](images/gs-config-database.png)

1.  Select a **Schema** for that database.

    ![Select schema](images/gs-config-schema.png)

1.  Click **Next**.

## Step 2: Specify your Watson Machine Learning service instance
{: #gs-config-ml}

Now, specify your Watson Machine Learning instance. This is where you store your AI models and deployments.

1.  Select an instance from the **Watson Machine Learning service** drop-down menu.

    ![Select ML service](images/gs-config-ml.png)

1.  Click **Next**.

## Step 3: Select which deployments to monitor
{: #gs-config-deploys}

1.  From the list of model deployments stored in your WML instance, select which deployments you will monitor.

    ![Select deployments](images/gs-config-deploy.png)

1.  Click **Next**.
1.  Click **Save**.

You have successfully configured {{site.data.keyword.aios_short}}.

## Next steps
{: #gs-next-steps}

- [Configure monitors](monitor-overview.html) for each deployment you selected.
- [View monitored data](insight-overview) in the {{site.data.keyword.aios_short}} dashboard.
