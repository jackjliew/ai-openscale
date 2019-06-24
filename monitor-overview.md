---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: deployment, monitors, data

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

# Preparing monitors for a deployment
{: #mo-config}

Set up and enable monitors for each deployment that you are tracking with {{site.data.keyword.aios_short}}.
{: shortdesc}

## Configuration
{: #io-conf}

The **Configure** tab ( ![Config tab](images/insight-config-tab.png) ) opens a Configuration Summary for the selected deployment.

  ![Config summary](images/insight-config-summary.png)

From here, you can directly edit the configuration settings for your deployment monitor.

## Selecting a deployment
{: #mo-select-deploy}

1.  First, you must select a deployment.

    1. Click the **Add deployments** button. A list of available model deployments appears.
    2. Click a model deployment and then click **Configure**.

    If there are multiple deployments for a given model, then when you configure one deployment, all other deployments for the same model also get configured.
    {: note}

    ![Select deployment page](images/config-select-deploy.png)

1.  Click the **Configure monitors** button.

    ![Prepare for monitoring](images/config-prep-monitor.png)

## Provide payload logging details
{: #mo-work-data}

You must provide information about your model and training data. For more information about training data, see [Why does {{site.data.keyword.aios_short}} need access to my training data?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Prepare explanation](images/config-what-monitor.png)

- If you use an {{site.data.keyword.pm_full}} instance that is in the same region as your {{site.data.keyword.aios_short}} instance, your payload logging information is configured automatically for you.
- Otherwise from the **Payload logging** tab and windows, you must enter information about your data and algorithm types and your payload logging. 

   There are specific requirements depending on your selections. For more information, see [Numeric/categorical data](https://test.cloud.ibm.com/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan).

   Before you can configure your monitors, you need to copy one of the code snippets to run. Run the cURL command in your client application or the Python command in your data science notebook. This provides a way to log model deployment requests and write response data into the payload database.

## Provide model details
{: #mo-work-model-dets}

Provide information about your model so that {{site.data.keyword.aios_short}} can access the database and understand how the model is set up.

Specifically to configure monitors, you must perform the following tasks:

1. Specify the location of the training data. You do this by entering the location, hostname or IP address, the database name, and the authentication information.
2. Within the database, you must select the training table by selecting the schema and table.
3. Select the label column from the training table.
4. Select the features that were used to train the AI deployment.
5. Select the text and categorical features.
6. Select the deployment prediction column.
7. Finally, you can review your model details before you save it.

The following sections give some specific information that you encounter depending on the type of model, either [Numeric/categorical data](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan) or [Images and Unstructured text](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datai).


### Numeric/categorical data
{: #mo-nuca}

For numeric or categorical data, you need to provide information about the training data for your model, in order to configure the monitors.

- **Manually configure monitors** - Requires you to provide connection information to your training data.

    - Select the [algorithm type](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand), and click **Next**:

      The format of the training data must match the model. For example, if the model expects `M` and `F` for the feature `Gender`, then the training data should have `M` and `F`, not `Male` and `Female`.  The current release of {{site.data.keyword.aios_short}} supports only Db2 database or Cloud Object Storage locations.
        {: important}

    - Specify the Location (either `Db2` or `Cloud Object Storage`), then:

        - For a Db2 database, enter the following information:

            - Host name or IP address
            - Port
            - Database (name)
            - Username
            - Password

        - For Cloud Object Storage, enter the following information:

            - Login URL: The Login URL must match the region setting of the bucket where your training data is located. You will specify the training data bucket in the next step.
            - Resource instance (ID)
            - API key

    - To ensure a valid connection, click the **Test** button to connect to the training data.
    - Specify the exact location in the Db2 database or Cloud Object Storage where the training data is located.

        - For a Db2 database, select both a schema and a training table that includes columns expected by your model.
        - For Cloud Object Storage, select a Bucket and a Data Set.

- **Upload a configuration file** - Choose this option if you prefer to keep your training data private. You can use a custom Python notebook to provide {{site.data.keyword.aios_short}} with information to analyze your training data without providing access to the training data itself.

  Running the Python notebook lets you capture distinct values in the schema columns, as well as the column names. In addition, you can use the notebook to pre-configure the Fairness monitor.

   - Download the [custom notebook](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external}, and replace any credentials with your own credentials.
   - Review the notebook carefully, specifying data for your model where appropriate. Save the notebook.
   - Run the notebook to generate a JSON-formatted configuration file.
   - Upload the JSON configuration file.

     ![Upload config JSON](images/config-json-monitor.png)

- {{site.data.keyword.aios_short}} locates your training data from the metadata stored with the model in {{site.data.keyword.pm_full}}. Choose the label column in the training data that contains your prediction values.
- Select the columns used to train the model - these are the features that your model deployment expects in a request.
- Finally, select the columns that contained text, and have been converted to integers. For example, if the original training data contained `Male` and `Female` for `Gender`, and they have now been mapped to `0` and `1` respectively, the training data now contains `0` and `1` values for the `Gender` column. Identify such columns which now contain integers, but originally contained text values.

### Images and Unstructured text
{: #mo-imun}

- **Images**

  For models that accept images as input, the image needs to be represented as a (height) x (width) x (# channels) format, where each point represents either monochrome or RGB values for each pixel.

- **Unstructured text**

   For models that accept text as input, it is expected that the model accepts the entire text, and not a vectorized representation of the text.

## Review and save configuration
{: #mo-save}

Review your selection summary and click **Save** to continue.

  ![Select data table](images/config-summary-monitor.png)

### Next steps
{: #mo-next}

To begin configuring monitors, click the **Accuracy** tab and click **Begin**.
