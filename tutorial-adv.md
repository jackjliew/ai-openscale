---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Python SDK Tutorial (Advanced)
{: #crt-ov}

## Scenario
{: #crt-scenario}

Traditional lenders are under pressure to expand their digital portfolio of financial services to a larger and more diverse audience, which requires a new approach to credit risk modeling. Their data science teams currently rely on standard modeling techniques - like decision trees and logistic regression - which work well for moderate datasets, and make recommendations that can be easily explained. This satisfies regulatory requirements that credit lending decisions must be transparent and explainable.

To provide credit access to a wider and riskier population, applicant credit histories must expand beyond traditional credit, like mortgages and car loans, to alternate credit sources like utility and mobile phone plan payment histories, plus education and job titles. These new data sources offer promise, but also introduce risk by increasing the likelihood of unexpected correlations which introduce bias based on an applicant’s age, gender, or other personal traits.

The data science techniques most suited to these diverse datasets, such as gradient boosted trees and neural networks, can generate highly accurate risk models, but at a cost. Such "black box" models generate opaque predictions that must somehow become transparent, to ensure regulatory approval such as Article 22 of the General Data Protection Regulation (GDPR), or the federal Fair Credit Reporting Act (FCRA) managed by the Consumer Financial Protection Bureau.

The credit risk model provided in this tutorial uses a training dataset that contains 20 attributes about each loan applicant. Two of those attributes - age and sex - can be tested for bias. For this tutorial, the focus will be on bias against sex and age. For more information about training data, see [Why does {{site.data.keyword.aios_short}} need access to my training data?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

{{site.data.keyword.aios_short}} will monitor the deployed model's propensity for a favorable outcome ("No Risk") for one group (the Reference Group) over another (the Monitored Group). In this tutorial, the Monitored Group for sex is `female`, while the Monitored Group for age is `18 to 25`.

## Prerequisites
{: #crt-prereqs}

This tutorial uses a Jupyter notebook that should be run in a Watson Studio project, using a "Python 3.5 with Spark" runtime environment. It requires service credentials for the following {{site.data.keyword.cloud_notm}} services:

- Cloud Object Storage (to store your {{site.data.keyword.DSX}} project)
- {{site.data.keyword.aios_short}}
- {{site.data.keyword.pm_full}}
- (Optional) Databases for PostgreSQL or Db2 Warehouse

The Jupyter notebook will train, create and deploy a German Credit Risk model, configure {{site.data.keyword.aios_short}} to monitor that deployment, and provide seven days' worth of historical records and measurements for viewing in the {{site.data.keyword.aios_short}} Insights dashboard. You can also optionally configure the model for continuous learning with Watson Studio and Spark.

## Introduction
{: #crt-intro}

In this tutorial, you will perform the following tasks:

- [Provision {{site.data.keyword.cloud_notm}} machine learning and storage services](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-services).
- [Set up a Watson Studio project, and run a Python notebook to create, train and deploy a machine learning model](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-set-wstudio).
- [Provision {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-wos-adv).
- [Run a Python notebook to create a data mart, configure performance, accuracy, and fairness monitors, and create data to monitor](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-edit-notebook).
- [View results in the {{site.data.keyword.aios_short}} Insights tab](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-view-results).

## Provision {{site.data.keyword.cloud_notm}} Services
{: #crt-services}

Log in to your [{{site.data.keyword.cloud_notm}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window} with your {{site.data.keyword.ibmid}}. When provisioning services, particularly if you use Db2 Warehouse, verify that your selected organization and space are the same for all services.

### Create a {{site.data.keyword.DSX}} account
{: #crt-wstudio}

- [Create a {{site.data.keyword.DSX}} instance ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/watson-studio){: new_window} if you do not already have one associated with your account:

  ![Watson Studio](images/watson_studio.png)

- Give your service a name, choose the Lite (free) plan, and click the **Create** button.

### Provision an {{site.data.keyword.cos_full_notm}} service
{: #crt-cos}

- [Provision an {{site.data.keyword.cos_short}} service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} if you do not already one associated with your account:

  ![Object Storage](images/object_storage.png)

- Give your service a name, choose the Lite (free) plan, and click the **Create** button.

### Provision an {{site.data.keyword.pm_full}} service
{: #crt-wml}

- [Provision a {{site.data.keyword.pm_short}} instance ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/machine-learning){: new_window} if you do not already have one associated with your account:

  ![Machine Learning](images/machine_learning.png)

- Give your service a name, choose the Lite (free) plan, and click the **Create** button.

### Provision an {{site.data.keyword.aios_full}} service
{: #crt-wos-adv}

If you haven't already, ensure that you provision {{site.data.keyword.aios_full}}. 

- [Provision a {{site.data.keyword.aios_short}} instance ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/watson-openscale){: new_window} if you do not already have one associated with your account:

  ![{{site.data.keyword.aios_short}} tile](images/wos-cloud-tile.png)

1. Click **Catalog** > **AI** > **{{site.data.keyword.aios_short}}**.
2. Give your service a name, choose a plan, and click the **Create** button.
3. To start {{site.data.keyword.aios_short}}, click the **Get Started** button.

### (Optional) Provision a Databases for PostgreSQL or DB2 Warehouse service
{: #crt-db2}

If you have a paid {{site.data.keyword.cloud_notm}} account, you may provision a `Databases for PostgreSQL` or `Db2 Warehouse` service to take full advantage of integration with {{site.data.keyword.DSX}} and continuous learning services. If you choose not to provision a paid service, you can use the free internal PostgreSQL storage with {{site.data.keyword.aios_short}}, but you will not be able to configure continuous learning for your model.

- [Provision a Databases for PostgreSQL service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/databases-for-postgresql) or [a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse) if you do not already have one associated with your account:

  ![DB for Postgres](images/dbpostgres.png)

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Standard plan (Databases for PostgreSQL) or Entry plan (Db2 Warehouse), and click the **Create** button.

## Set up a {{site.data.keyword.DSX}} project
{: #crt-set-wstudio}

- Log in to your [{{site.data.keyword.DSX}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.ibm.com/){: new_window}. Click the {{site.data.keyword.avatar}} and verify that the account you are using is the same account you used to create your {{site.data.keyword.cloud_notm}} services:

  ![Same Account](images/same_account.png)

- In {{site.data.keyword.DSX}}, begin by creating a new project. Select "Create a project":

  ![Watson Studio create project](images/studio_create_proj.png)

- Select the **Standard** tile, to create the project:

  ![Watson Studio select Standard project](images/studio_create_standard.png)

- Give your project a name and description, make sure the Cloud Object Storage service you created is selected in the **Storage** dropdown, and click **Create**.

## Create and deploy a {{site.data.keyword.pm_short}} model
{: #crt-make-model}

### Add the `Working with Watson Machine Learning` notebook to your {{site.data.keyword.DSX}} project
{: #crt-add-notebook}

- Download the following file:

    - [Working with Watson Machine Learning ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- From the **Assets** tab in your {{site.data.keyword.DSX}} project, click the **Add to project** button and select **Notebook** from the dropdown:

  ![Add Connection](images/add_notebook.png)

- Select **From file**:

  ![New Notebook Form](images/new_notebook_name.png)

- Then click the **Choose file** button, and select the "german_credit_lab.ipynb" notebook file that you downloaded:

  ![New Notebook Form](images/new_notebook_name2a.png)

- In the **Select runtime** section, choose a Python 3.5 with Spark option:

- Click **Create Notebook**.

### Edit and run the `Working with Watson Machine Learning` notebook
{: #crt-edit-notebook}

The `Working with Watson Machine Learning` notebook contains detailed instructions for each step in the Python code you will run. As you work through the notebook, take some time to understand what each command is doing.
{: tip}

- From the **Assets** tab in your Watson Studio project, click the **Edit** icon next to the `Working with Watson Machine Learning` notebook to edit it.

- In the "Provision services and configure credentials" section, make the following changes:

    - Follow the instructions to create, copy, and paste an {{site.data.keyword.cloud_notm}} API key.

    - Replace the {{site.data.keyword.pm_full}} service credentials with the ones you created previously.

    - Replace the DB credentials with the ones you created for Databases for PostgreSQL.

    - If you previously configured {{site.data.keyword.aios_short}} to use a free internal PostgreSQL database as your data mart, you can switch to a new data mart that uses your Databases for PostgreSQL service. To delete your old PostgreSQL configuration and create a new one, set the KEEP_MY_INTERNAL_POSTGRES variable to `False`.

        The notebook will remove your existing internal PostgreSQL data mart and create a new data mart with the supplied DB credentials. **No data migration will occur**.
        {: important}

- Once you have provisioned your services and entered your credentials, your notebook is ready to run. Click the **Kernel** menu item, and select **Restart & Clear Output** from the menu:

  ![Restart and Clear](images/restart_and_clear.png)

- Now, run each step of the notebook in sequence. Notice what is happening at each step, as described. Complete all the steps, up through and including the steps in the "Additional data to help debugging" section.

The net result is that you will have created, trained, and deployed the **Spark German Risk Deployment** model to your {{site.data.keyword.aios_short}} service instance. {{site.data.keyword.aios_short}} will be configured to check the model for bias against sex (in this case, Female) or age (in this case, 18-25 years old).

## Viewing results
{: #crt-view-results}

### View insights for your deployment
{: #crt-view-insights}

Using the [{{site.data.keyword.aios_short}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, click on the **Insights** tab:

  ![Insights](images/insight-dash-tab.png)

The Insights page provides an overview of metrics for your deployed models. You can easily see alerts for Fairness or Accuracy metrics that exceed the threshold set when running the notebook. The data and settings used in this tutorial will have created Accuracy and Fairness metrics similar to the ones shown here.

  ![Insight overview](images/insight-overview-adv-tutorial-2.png)

### View monitoring data for your deployment
{: #crt-view-mon-data}

1. To view monitoring details, from the **Insights** page, click the tile that corresponds to the deployment. The monitoring data for that deployment appears. 
2. Slide the marker across the chart to select data for a specific one-hour window. 
3. Click the **View details** link.

  ![Monitor data](images/insight-monitor-data2.png)

Now, you can review the charts for the data you monitored. For this example, you can see that for the "Sex" feature, the group `female` received the favorable outcome "No Risk" less (68%) than the group `male` (78%).

  ![Insight overview](images/insight-review-charts2.png)

### View explainability for a model transaction
{: #crt-view-explain}

For each deployment, you can see explainability data for specific transactions.

If you already know which transaction you want to view, there's a quick way to look it up with the transaction ID. After you click the deployment tile, from the navigator, click the **Explain a transaction** ![Explain a transaction tab](images/insight-transact-tab.png) icon, type the transaction ID, and press **Enter**.
{: tip}

If you use the internal lite version of PostgreSQL, you might not be able to retrieve your database credentials. This might prevent you from seeing transactions.
{: note}

1. From the charts for the latest biased data, click the **View transactions** button.

  ![View transactions](images/view_transactions.png)

  A list of transactions where the deployment has acted in a biased manner appears. 
  
2. Select one of the transactions and, from the **ACTION** column, click the **Explain** link.

  ![Transaction list](images/transaction_list_cr.png)

You will now see an explanation of how the model arrived at its conclusion, including how confident the model was, the factors that contributed to the confidence level, and the attributes fed to the model.

  ![View Transaction](images/view_transaction_cr.png)
  
## Next steps
{: #crt-next-steps}

- Learn more about [viewing and interpreting the data](/docs/services/ai-openscale?topic=ai-openscale-it-ov) and [monitoring explainability](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
