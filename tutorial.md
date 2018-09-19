---

title: Trust and transparency for your machine learning models with AI OpenScale
description: Monitor your machine learning deployments for bias and explainability
duration: 180
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, deploy a sample web app tand finally configure the new IBM AI OpenScale product to monitor your models for trust and transparency.
takeaways:
- See how AI OpenScale provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018
lastupdated: "2018-9-17"

---

# Tutorial

## Prerequisites

To complete this tutorial, you will need:

- A [Watson Studio](https://dataplatform.ibm.com/) account.
- An [IBM Cloud](https://console.bluemix.net/) account

During the tutorial, you will provision the following Lite (free) IBM Cloud Services:

- Machine Learning
- Apache Spark
- Object Storage
- You will also provision the following **paid** IBM Cloud Services:
    - Db2 Warehouse
    - PostgreSQL

## Introduction

In this tutorial, you will:

- Provision IBM Cloud machine learning and storage services and upload sample data
- Set up a Watson Studio project, and run Python notebooks to create, train and deploy machine learning models
- Configure and explore trust, transparency and explainability monitoring for your models

## Provision IBM Cloud Services

Login to your [IBM Cloud account](https://console.bluemix.net) with your IBM ID.

### Provision a Machine Learning service

- If you do not already have a Machine Learning service associated with your account, click the **Create Resource** button or the **Catalog** menu item, then filter on "Machine Learning" and click the **Machine Learning** tile:

  ![Machine Learning](images/machine_learning.png)
  
- Give your service a name, choose the Lite (free) plan, and click the **Create** button.

### Make note of the Machine Learning service credentials

In your machine learning instance, click on the **Service credentials** link on the left-hand side of the page. Name the credential and click **Add**. Then, from the list of credentials, click **View credential** and copy the JSON object for later use.

### Provision a Spark service

If you do not already have a Spark service associated with your account, click the **Catalog** button from the top menu, filter on "Spark", and click the **Apache Spark** tile:

  ![Apache Spark](images/spark.png)
  
Assign your service a name, choose the Lite (free) plan, and click the **Create** button.

### Make note of the service credentials for your Spark instance

Open your Spark instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy this JSON object for later use.

### Provision an Object Storage service

If you do not already have an Object Storage service associated with your account, click the **Catalog** button from the top menu, filter on "object storage", and click the **Object Storage** tile:

  ![Object Storage](images/object_storage.png)
  
Give your service a name, choose the Lite (free) plan, and click the **Create** button.

### Provision a paid PostgreSQL service

If you do not already have a PostgreSQL service associated with your account, click the **Catalog** button from the top menu, filter on "postgres", and click the **Compose for PostgreSQL** tile:

  ![Compose for PostgreSQL](images/postgres.png)
  
Give your service a name, choose the Standard plan, and click the **Create** button.

### Make note of the service credentials for your PostgreSQL instance

Open your existing (or newly-created) PostgreSQL instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy this JSON object for later use.

### Provision a paid Db2 Warehouse service

If you do not already have a Db2 Warehouse service associated with your account, click the **Catalog** button from the top menu, filter on "db2", and click the **Db2 Warehouse** tile:

  ![Db2 Warehouse](images/db2_warehouse.png)
  
Give your service a name, choose the Entry plan, and click the **Create** button.

### Make note of the service credentials for your Db2 Warehouse instance

Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy this JSON object for later use.

### Upload training and feedback data to Db2 Warehouse

Download the [car_rental_feedback_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/ai-openscale) and [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/ai-openscale) files.

Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console](https://console.bluemix.net), click **Manage** from the left side panel, and the click the green **Open** button.

Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)
  
Browse to the feedback data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets, and then click **New Table** on the right:

  ![New Table](images/new_table.png)
  
Name your table CAR\_RENTAL\_FEEDBACK, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)
  
Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)
  
The feedback data should now be displaying correctly in columns. Click **Next** to continue, and then click **Begin Load** to load the data.

When the data has finished loading, repeat the same steps to load the training data file, naming it CAR\_RENTAL\_TRAINING.

### Provision AI OpenScale

Click the **Catalog** link and filter on "OpenScale". Select the tile for AI OpenScale:

  ![AI OpenScale](images/openscale.png)
  
Give your service a name, select the Lite plan, and click **Create**. You will configure AI OpenScale after setting up models for it to monitor.

## Set up a Watson Studio project

Login to your [Watson Studio account](https://dataplatform.ibm.com/). Click the account avatar icon in the upper right and verify that the account you are using is the same account you used to create your IBM Cloud services:

  ![Same Account](images/same_account.png)

In Watson Studio, begin by creating a new project. Select the **Complete** tile and click **Create**:

  ![Watson Studio complete](images/ws_complete.png)
  
Give your project a name and description, make sure the Object Storage service you created in the previous step is selected in the **Storage** dropdown, and click **Create**.

### Associate your IBM Cloud Services with your Watson project

Open your Watson Studio project and select the **Settings** tab. In the **Associated Services** section, click the **Add service** dropdown and select **Watson**:

  ![Add Watson Service](images/add_watson_service.png)
  
Click the **Add** link on the **Machine Learning** tile and select the **Existing** tab. Choose the service you created in the previous section from the **Existing Service Instance** dropdown and click **Select**.

From the project settings tab, select **Add service** again and choose **Spark** from the dropdown. From the **Existing** tab, choose the Spark service you created and click **Select**.

### Add the Spark notebooks to your Watson Studio project

Download the following files:

- [CARS4U-Action-Recommendation-Spark.ipynb](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/ai-openscale/CARS4U-Action-Recommendation-Spark.ipynb)
- [CARS4U-Business-Area-Prediction-Spark.ipynb](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/ai-openscale/CARS4U-Business-Area-Prediction-Spark.ipynb)

In Watson Studio, select the **Assets** tab of your project, scroll down to the **Notebooks** section, and click the **New Notebook** button:

  ![New Notebook](images/new_notebook.png)
  
Select the **From file** tab of the menu, and give your notebooks a name:

  ![New Notebook Form](images/new_notebook_name.png)
  
In the **Select runtime** section, choose the Spark instance you created earlier from the dropdown list:

  ![Spark Runtime](images/spark_runtime.png)
  
Click **Create Notebook**. Now repeat these steps for the other Spark notebook, making sure to set your Spark instance as the runtime.

### Add the Python notebooks to your Watson Studio project

Download the following files:

- [CARS4U-Business-Area-and-Action-AI-function.ipynb](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/ai-openscale/CARS4U-Business-Area-and-Action-AI-function.ipynb)
- [CARS4U-Satisfaction-Prediction-Keras-AI-function.ipynb](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/ai-openscale/CARS4U-Satisfaction-Prediction-Keras-AI-function.ipynb)

Follow the same steps as above to add these notebooks to your project. However, use the default Python 3.5 XS runtime for them instead of your Spark instance:

  ![Python Runtime](images/python_runtime.png)
  
## Edit and run the notebooks

### Edit and run the Action Recommendation Spark Notebook

From the **Assets** tab in your Watson Studio project, click the **Edit** icon next to the CARS4U-Action-Recommendation-Spark notebook to edit it. In section 2 and section 4.2, replace the Db2 Warehouse credentials with the ones you created in the previous section, and ensure that the table name for the training data matches the one you created when loading the CSV files.

In section 4, replace the Watson Machine Learning credentials with the ones you created in the previous section.

In section 6.1, replace the Spark credentials with the ones you created in the previous section.

Once you have entered your credentials, your notebook is ready to run. Click the **Kernel** menu item, and select **Restart and Run All** from the menu:

  ![Restart and Run](images/restart_and_run.png)
  
This will create, train and deploy the **CARS4U - Action Recommendation Model** in your project.

### Edit and run the Business Area Prediction Spark Notebook

From the **Assets** tab in your Watson Studio project, click the **Edit** icon next to the CARS4U-Business-Area-Prediction-Spark notebook to edit it. In section 2, replace the Db2 Warehouse credentials with the ones you created in the previous section.

In section 4, replace the Watson Machine Learning credentials with the ones you created in the previous section.

Your notebook is ready to run. Click the **Kernel** menu item, and select **Restart and Run All** from the menu. This will create, train and deploy the **CARS4U - Business Area Prediction Model** in your project.

### Edit and run the Business Area and Action AI Function Notebook

From the **Assets** tab in your Watson Studio project, click the **Edit** icon next to the CARS4U-Business-Area-and-Action-AI-function notebook to edit it.

In section 2, replace the Watson Machine Learning credentials with the ones you created in the previous section.

Your notebook is ready to run. Click the **Kernel** menu item, and select **Restart and Run All** from the menu. This will create, train and deploy the **CARS4U - Business area and Action Prediction - AI Function** in your project.

### Edit and run the Satisfaction Prediction Keras AI Function Notebook

From the **Assets** tab in your Watson Studio project, click the **Edit** icon next to the CARS4U-Satisfaction-Prediction-Keras-AI-function notebook to edit it.

In section 0, replace the Watson Machine Learning and Postgres credentials with the ones you created in the previous section.

In section 2, replace the "dsn" and "username" Db2 Warehouse credentials with the ones you created previously.

Your notebook is ready to run. Click the **Kernel** menu item, and select **Restart and Run All** from the menu. This will create and deploy the **CARS4U - Business area and Action Prediction AI Function** in your project.

## Configure AI OpenScale

### Connect AI OpenScale to your machine learning models

Now that the machine learning models have been deployed, you can configure AI OpenScale to ensure trust and transparency with your models.

From the [IBM Cloud Dashboard](https://console.bluemix.net/dashboard/apps), scroll down to the **Services** section and click on the instance of AI OpenScale you provisioned. Select the **Manage** tab and click the **Get Started** button. The IBM AI OpenScale Getting Started page opens; click **Begin**.

AI OpenScale will ask for a connection to a PostgreSQL deployment. Select the one you created earlier from the **Database** dropdown, and choose the **public** schema:

  ![AI OpenScale PostgreSQL](images/aios_postgres.png)
  
Click **Next**. You will now select your instance of Watson Machine Learning from the dropdown, and click **Next** again.

You are now able to select which deployed models will be monitored by AI OpenScale. All five models and functions created and deployed can be checked by default; click **Next** to accept this:

  ![Models monitored](images/models_monitored.png)
  
Save the configuration and, when prompted, click the **Continue with Configuration** button.

### Configure fairness monitoring

Begin by configuring the Action model. Select its tile and click **Begin**:

  ![Business area and Action Prediction Model](images/bus_area_model.png)
  
There are three areas to configure. Begin by selecting **Fairness** and clicking **Begin**. You can read a description of Fairness before clicking **Next** to continue.

Specify the location of the model training data by selecting **Db2** from the **Location** dropdown and filling out the remaining fields with the Db2 credentials we created earlier before clicking **Next**.

Once the database is connected, select your schema and the training data table in the dropdowns, then click **Next**:

  ![Schema Selection](images/schema_select.png)
  
Next, you must specify which column from the table contains prediction values. In this case, it's the **Action** column, so select that one and click **Next**.

You may now choose which features to monitor. In this example, we'll monitor the **Gender** feature for bias. Click on the **Gender** tile and click **Next**.

AI OpenScale works to detect bias against a protected group in comparison to a reference group. For our example, add the value "Male" to the **Reference group**, and the value "Female" to the **Protected group**, and click **Next**:

  ![Gender Groups](images/gender_groups.png)
  
You may now assign a fairness threshold. You will see an alert on your operations dashboard if the fairness rating falls below this threshold. Click **Next** to leave it set at the default of 80%.

You will now select favorable and unfavorable prediction values from the payload logging database. AI OpenScale has automatically detected which column in our payload logging data contains the prediction values; those values are 0 (for no customer service action taken) or 1 - 3 (corresponding to follow-up actions, vouchers or discounts). Add these values to the form and click **Next**:

  ![Positive and negative values](images/pos_and_neg.png)
  
Use the slider to adjust the minimum sample size to 400, then click  **Next**. Review your choices, and then click **Save**.

### Configure accuracy monitoring

Continue to **Accuracy** and click **Begin**. You can read a description of Accuracy before clicking **Next** to continue.

Select the Spark instance that you configured in a previous step from the dropdown list and click **Next**.

Next, select the model type. There are four possible outcomes from the model, so select **Multiclass Classification** from the dropdown and click **Next**:

  ![Multiclass](images/multiclass.png)
  
Next, set the accuracy threshold. Click **Next** to leave it at the default 80%. Use the slider to adjust the minimum sample size to 400, then click  **Next**.

You can review your choices before clicking **Save** to finalize them.

### Configure explainability monitoring

Continue to **Explainability** and click **Begin**. You can read a description of Accuracy before clicking **Next** to continue.

First, select the type of data the deployment analyzes. Our models receive numeric/categorical data, so select that option from the dropdown and click **Next**.

The training data is located in the Db2 Warehouse instance we created earlier. Add the credentials in the form, **Test** the connection, and then click **Next**.

To identify the location of the training table, set the schema to your Db2 Warehouse username, set the table to **CAR\_RENTAL\_TRAINING**, and click **Next**:

  ![Explainability Schema](images/explain_schema.png)
  
Next, select the **Action** column, as it contains the prediction values from the machine learning service, and click **Next**.

All of the data columns are inputs to the model. Select all inputs and click **Next**:

  ![Explainability Inputs](images/explain_inputs.png)
  
For categorical features, neither **ID**, **Children** nor **Satisfaction** contained text, so click **Next** without selecting any. Review your input and click **Save**.

You have finished configuring AI OpenScale. It will now monitor your models and provide real-time bias detection and explainability. In the next steps, you will provide sample data for it to analyze.

## Connect your databases to Watson Studio

From the **Assets** tab in your Watson Studio project, click the **Add to project** button and select **Connection** from the dropdown:

  ![Add Connection](images/add_connection.png)
  
A list of your Cloud Services will appear. Select the Db2 instance you created earlier, and the click **Create**. You can now add the data from this database to your project. Click **Add to project** again, and selected **Connected assets**:

  ![Add Connected Asset](images/add_connected_assets.png)
  
Click the **Select source** link and choose your Db2 Warehouse instance, schema, and the CAR\_RENTAL\_FEEDBACK table, then click **Select**.
  
  ![Connection Source](images/connection_source.png)

Give your asset a name, then click **Create**. Repeat the same steps to add the CAR\_RENTAL\_TRAINING table as well.

Now add the PostgreSQL database. In your Watson Studio project, click **Add to project** and select **Connection**.

Select your PostgreSQL instance from the list of Cloud Services. If Watson Studio is unable to connect to the existing service in this way, instead connect it to the **Compose for PostgreSQL** service in the section below, and provide the credentials to your service:

  ![Compose Service](images/compose_service.png)
  
Now add the payload logging tables from PostgreSQL to Watson Studio.  First, find the deployment ID for your Action model. From the **Deployments** tab of your Watson Studio project, click the **CARS4U - Action Model Deployment** link. On the **Overview** tab, scroll down and make note of the model ID:

  ![Model ID](images/model_id.png)

From the **Assets** tab of your Watson Studio project, click **Add to project** and select **Connected assets** from the dropdown. Click the **Select source** button and choose your PostgreSQL instance and the **public** schema.

The payload logs are named _Payload\_\<model id\>_. Locate the one that matches the Action Model Deployment. Click **Select**, give the table a memorable name like "Action Model Payload", and click **Create**:

  ![Named Asset Connection](images/named_asset_connection.png)
  
With the action model payload added as a data asset within Watson Studio, it's now easy to share, visualize and analyze. The payload table is currently empty. Next, you will provide some data for your models to analyze.

## Provide a set of sample data to your models

When configuring AI OpenScale, you set the threshold for fairness and accuracy monitoring to 400 requests. No data will appear in the dashboard until this threshold is met. You can generate these requests using the web application, or you can do it all at once by feeding the training data back to the model for scoring.

To do this, you will need the scoring endpoint URL for your Action Model. From the **Deployments** tab of your Watson Studio project, click the **CARS4U - Action Model Deployment** link, click the **Implementation** tab, and then copy the Scoring End-point for your model:

  ![Endpoint URL](images/endpoint_url.png)

Next, download [this iPython notebook](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/ai-openscale/CARS4U-Sample-Data-Generation.ipynb) to your machine, and then add it to your Watson Studio project by clicking the **New notebook** link from the **Notebook** section of the  **Assets** tab.

Select **From file**, choose the "CARS4U-Sample-Data-Generation.ipynb" file, and select the **Default Python 3.5 Free** runtime from the dropdown. Click **Create Notebook**.

Once the notebook has opened, update the first code cell with your Db2 Warehouse **dsn** and **username** credentials. Then update the second code cell with your WML credentials, and the scoring end-point URL for the Action Model deployment.

Run both code cells of the notebook. Each time you run the second code cell, nearly 500 payloads will be sent to your model for scoring. Run this cell enough to exceed the threshold you set for monitoring.

## View the explainability for a model transaction

From the **Assets** tab of your Watson Studio project, click on the **Action Model Payload** link in the **Data Assets** section. There should now be at least 482 rows of payload data. Expand the _scoring\_id_ column horizontally, and copy one of the identifiers to your clipboard:

  ![scoring_id](images/scoring_id.png)
  
Using the [AI OpenScale dashboard](https://aiopenscale.cloud.ibm.com/aiopenscale/), click on the **Explainability** button:
  
  ![Explainability](images/explainability.png)
  
Paste the value you copied from the _scoring\_id_ column into the search box and press **Return** on your keyboard:

  ![Paste Transation](images/paste_transaction.png)
  
You will now see an explanation of how the model arrived at its conclusion, including how confident the model was, the factors that contributed to the confidence level, and the attributes fed to the model.
