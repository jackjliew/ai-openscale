---

copyright:
  years: 2015, 2018
lastupdated: "2018-9-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Fairness
{: #monitor-fair}

Fairness monitors your deployment for biases, to help ensure fair outcomes across different populations.
{: shortdesc}

## Understanding Fairness
{: #understand-fair}

{{site.data.keyword.aios_short}} checks your deployed model for bias at runtime. To detect bias for a deployed model, you must define feature requirements, such as Age or Gender, as detailed in [Configuring the Fairness monitor](monitor-fairness.html#config-fair) below.

It is mandatory to specify the output schema for a model or function in Watson Machine Learning (WML), for bias checking to be enabled in {{site.data.keyword.aios_short}}. The output schema can be specified using the `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` property in the metadata part of the `store_model` API. For more information, see the [WML client documentation](http://wml-api-pyclient-dev.mybluemix.net/#repository)

### How it works

Before configuring the Fairness monitor, there a few key concepts that are critical to understand:

- *Fairness attributes*: These are the model attributes for which the model is likely to exhibit bias. As an example, for the fairness attribute **`Gender`**, the model could be biased against specific gender values (`Female`, `Transgender`, etc.) Another example of a fairness attribute is **`Age`**, where the model could exhibit bias against people in an age group, like `18 to 25`.
  
- *Majority / Minority value*: The values of fairness attributes are split into two distinct categories: Majority and Minority. The Minority values are those which are likely to be discriminated against. In the case of a fairness attribute like **`Gender`**, the Minority values could be `Female` and `Transgender`. For a numeric fairness attribute, such as **`Age`**, the Minority values could be `[18-25]`. All other values for a given fairness attribute are then considered as Majority value, for example `Gender=Male` or `Age=[26,100]`.
  
- Favorable / Unfavorable outcome: The output of the model is categorized as either Favorable or Unfavorable. As an example, if the model is predicting whether a person should get a loan or not, then the Favorable outcome could be `Loan Granted` or `Loan Partially Granted`, whereas the Unfavorable outcome might be `Loan Denied`. Thus, the Favorable outcome is one that is deemed as a positive outcome, while the Unfavourable outcome is deemed as being negative.

The {{site.data.keyword.aios_short}} algorithm computes bias on an hourly basis, using the last `N` records present in the payload logging table; the value of `N` is specified when configuring Fairness. The algorithm perturbs these last `N` records to generate additional data.

The perturbation is done by changing the value of the fairness attribute from Majority to Minority, or vice-versa. The perturbed data is then sent to the model to evaluate its behavior. The algorithm looks at the last `N` records in the payload table, and the behavior of the model on the perturbed data, to decide if the model is acting in a biased manner.

A model is deemed to be biased if, across this combined dataset, the percentage of Favorable outcomes for the Minority class is less than the percentage of Favorable outcomes for the Majority class, by some threshold value. This threshold value is to be specified when configuring Fairness.

### Example

Consider a data point where, for `Gender=Male` (Majority value), the model predicts a Favorable outcome, but when the record is perturbed by changing `Gender` to `Female` (Minority value), while keeping all other feature values the same, the model predicts an Unfavorable outcome. A model overall is said to exhibit bias if there are sufficient data points (across the last `N` records in the payload table, plus the perturbed data) where the model was acting in a biased manner.

### Supported models

 {{site.data.keyword.aios_short}} supports bias detection only for those models and Python functions which expect some kind of structured data in its feature vector. In the current release, bias detection is supported only for classification models (models which predict a categorical value); {{site.data.keyword.aios_short}} does not support bias detection for regression models (models which predict a continuous value).

## Configuring the Fairness monitor
{: #config-fair}

1.  From the *What is Fairness?* page, click **Next** to start the configuration process.

    ![What is fairness? page](images/fair-what-is.png)

1.  {{site.data.keyword.aios_short}} will attempt to locate your training data from themetadata stored with the model in WML. If {{site.data.keyword.aios_short}} is unable to locate training data, enter the following connection information on the *Specify the location of the training data* page. First, specify the Location (either `Db2` or `Cloud Object Storage`), then:

    - For a Db2 database, complete the following:

      - Host name or IP address
      - Port
      - Database (name)
      - Username
      - Password

      ![Specify Db2 location of training data page](images/fair-config-data-db2.png)

    - For Cloud Object Storage, complete the following:

      - Log-in URL
      - Resource instance (ID)
      - Access key
      - Secret key
      - API key

      ![Specify Cloud Object Storage location of training data page](images/fair-config-data-cos.png)

    Ensure a valid connection by clicking the **Test** button to connect to the training data. Click **Next**.

1.  Now, you need to specify the exact location of the training data in Db2 or Cloud Object Storage.

    - For a Db2 database, select your schema and a training table that includes columns expected by the model schema:

      ![Specify Db2 location of training table](images/fair-config-table-db2.png)

    - For Cloud Object Storage, select a `Bucket` and a `Data Set`:

      ![Specify Cloud Object Storage location of data set](images/fair-config-dset-cos.png)

    Click **Next**.

1.  Choose the label column in the training data that contains your prediction values and click **Next**.

    ![Select column label](images/fair-config-column.png)

1.  On the *Select the deployment prediction column* page, select the prediction column from the payload logging table. The payload logging table contains the model deployment output.

    ![Select deployment prediction](images/fair-select-deploy.png)

    **Note**: Unless you have manually defined the schema, the default name of the model deployment prediction column will be `prediction`.

    If your payload logging table has no schema, a link directs you to the WML API (Swagger) document.

    ![No schema for deployment](images/fair-select-deploy-no.png)

    The page displays key information needed to make the request. **Note**: You must be familiar enough with the model to correctly structure `online_prediction_input` in the API call.

    Click **Next** to continue.

1.  On the *Select the features to monitor* page, find and select fairness attributes that you want to use and click **Next**.

    **Note**: Only features which are of categorical or numeric (integer) data type are supported. Features with other data types, such as float, double, etc., are not supported.

    In this example, the `Age`, `Gender`, and `Ethnicity` features have been selected.

    ![Select features to monitor page with selections](images/fair-select-feature.png)

    Click **Next** to continue.

1.  Each feature has specific requirements to configure. In this example, you define the **`Age`** ranges for a Reference (Majority) Group and a Protected (Minority) Group by manually entering values directly in each group.

    In this example, for the **`Age`** fairness attribute, if you feel that your model is likely to be biased against people with ages between 18 and 25, then the Protected Group value will be `[18,25]` and the Reference Group value will be `[26,100]`. In case of the **`Gender`** fairness attribute, the Reference Group value might be `Male`, while the Protected Group values could be `Female` and `Transgender`.

    ![Configure age settings](images/fair-config-age.png)

    Click **Next** to continue

1.  Set the threshhold limit for Fairness, for **`Age`**.

    A Fairness threshhold is used to specify an acceptable difference between the percentage of Favorable outcomes for the Minority group as compared to the percentage of Favorable outcomes for the Majority group.

    Consider a model that predicts who should get a loan (`favorable outcome=loan granted`) and who shouldn’t (`unfavorable outcome=loan denied`). Further, the Minority value for age is `[18,25]`, and the Majority value is `[26,100]`. When the bias detection algorithm runs, if it finds that the percentage of Favorable outcomes for people in the age group `[18,25]` in the last `N` records plus perturbed data is `50%`, while the percentage of Favorable outcomes for people in the age group `[26,100]` is `70%`, then Fairness is computed as 50*100/70 = 71.42.

    If the Fairness threshold is set to 80%, then the algorithm will flag the model as being biased, because the computed Fairness is lower than the threshhold. However, if the threshold is set to 70% then it will not report the model as being biased.

    ![Configure age settings](images/fair-config-age-limit.png)

    Click **Next** once you have selected a Fairness threshhold.

1.  Configure the `Gender` and `Ethnicity` features in the same manner:

     ![Configure gender settings](images/fair-config-gender.png)

     ![Configure ethnicity settings](images/fair-config-ethnic.png)

     **Note**: The values that you enter in this screen should be those that are sent to the model scoring endpoint (and consequently will be added to the payload table). If the data is being manipulated before sending to the scoring endpoint, then enter the manipulated values. For example, if the original data had values of `Male` and `Female` for *Gender* and it was manipulated so that the data sent to the scoring endpoint was `M` and `F`, then enter `M` and `F` on this screen.

     Click **Next** when you are done with each feature.

1.  Now, specify values that represent a favorable outcome for the model. Values are derived from the `label` column in the training data, if the model output schema contains a mapping column. In WML, the `prediction` column always has a double value. The mapping column is used to specify the mapping of this `prediction` value to the class label.

    For example, if the `prediction` value is `1.0`, the mapping column could have a value of `Loan denied`; this implies that the prediction of the model is `Loan denied`. So, if the model output schema contains a mapping column, then specify Favorable and Unfavorable values using those present in the mapping column.

    If, however, the mapping column is not present in the model output schema, then the Favorable and Unfavorable values need to be specified using the value of the `prediction` column (`0.0`, `1.0`, etc.)

     ![Configure outcome](images/fair-config-outcome.png)

     Click **Next**.

1.  Finally, set a minimum sample size, to prevent measuring Fairness until a minimum number of records are available in the evaluation dataset. This ensures the sample size is not too small to skew results. Every time bias checking runs, it will use the minimum sample size to decide the number of records on which it will do the bias computation.

     ![Configure sample size](images/fair-config-sample.png)

1.  Click the **Next** button.

    A summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section.

    You can also select the **Add another feature** link to return to the feature selection screen and add more features to the Fairness monitor, for example: `City`, `Zip Code` or `Account Balance`.

1.  Click **Save** to complete your configuration.

### Next steps
{: #fair-next}

From the *Configure monitors* page, you can select another monitoring category.
