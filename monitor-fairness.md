---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Configuring the fairness monitor
{: #mf-monitor}

In {{site.data.keyword.aios_full}}, the fairness monitor scans your deployment for biases, to ensure fair outcomes across different populations.
{: shortdesc}

## Understanding Fairness
{: #mf-understand}

{{site.data.keyword.aios_short}} checks your deployed model for bias at runtime. To detect bias for a deployed model, you must define fairness attributes, such as Age or Gender, as detailed in the following [Configuring the Fairness monitor](#mf-config) section.

It is mandatory to specify the output schema for a model or function in Watson {{site.data.keyword.pm_short}}, for bias checking to be enabled in {{site.data.keyword.aios_short}}. The output schema can be specified using the `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` property in the metadata part of the `store_model` API. For more information, see the [{{site.data.keyword.pm_full}} client documentation](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}.

### How it works
{: #mf-works}

Before configuring the Fairness monitor, there a few key concepts that are critical to understand:

- Fairness attributes are the model attributes for which the model is likely to exhibit bias. As an example, for the fairness attribute **`Gender`**, the model could be biased against specific gender values (`Female`, `Transgender`, etc.) Another example of a fairness attribute is **`Age`**, where the model could exhibit bias against people in an age group, like `18 to 25`.

- Reference and monitored values: The values of fairness attributes are split into two distinct categories: Reference and Monitored. The Monitored values are those which are likely to be discriminated against. In the case of a fairness attribute like **`Gender`**, the Monitored values could be `Female` and `Transgender`. For a numeric fairness attribute, such as **`Age`**, the Monitored values could be `[18-25]`. All other values for a given fairness attribute are then considered as Reference values, for example `Gender=Male` or `Age=[26,100]`.

- Favorable and unfavorable outcomes: The output of the model is categorized as either Favorable or Unfavorable. As an example, if the model is predicting whether a person should get a loan or not, then the Favorable outcome could be `Loan Granted` or `Loan Partially Granted`, whereas the Unfavorable outcome might be `Loan Denied`. Thus, the Favorable outcome is one that is deemed as a positive outcome, while the Unfavorable outcome is deemed as being negative.

The {{site.data.keyword.aios_short}} algorithm computes bias on an hourly basis, using the last `N` records present in the payload logging table; the value of `N` is specified when configuring Fairness. The algorithm perturbs these last `N` records to generate additional data.

The perturbation is done by changing the value of the fairness attribute from Reference to Monitored, or vice-versa. The perturbed data is then sent to the model to evaluate its behavior. The algorithm looks at the last `N` records in the payload table, and the behavior of the model on the perturbed data, to decide if the model is acting in a biased manner.

A model is deemed to be biased if, across this combined dataset, the percentage of Favorable outcomes for the Monitored class is less than the percentage of Favorable outcomes for the Reference class, by some threshold value. This threshold value is to be specified when configuring Fairness.

Fairness values can be more than 100%. This means that the Monitored group received more favorable outcomes than the Reference group. In addition, if no new scoring requests are sent, then the Fairness value will remain constant.
{: note}

### Do the math
{: #mf-bias-math}

The fairness metric used in {{site.data.keyword.aios_short}} is disparate impact, which is a measure of how the rate at which an unprivileged group receives a certain outcome or result compares with the rate at which a privileged group receives that same outcome or result.

The following mathematical formula is used for calculating disparate impact:

```
                     (num_positives(privileged=False) / num_instances(privileged=False))
Disparate impact =   ______________________________________________________________________

                     (num_positives(privileged=True) / num_instances(privileged=True))
```

where `num_positives` is the number of individuals in the group (either privileged=False, i.e. unprivileged, or privileged=True, i.e. privileged) who received a positive outcome, and num_instances is the total number of individuals in the group.

The resulting number will be a percentage—i.e. the percentage that the rate at which unprivileged group receives the positive outcome is of the rate at which the privileged group receives the positive outcome. For instance, if a credit risk model assigns the “no risk” prediction to 80% of unprivileged applicants and to 100% of privileged applicants, that model would have a disparate impact (presented as the fairness score in {{site.data.keyword.aios_short}}) of 80%.

In {{site.data.keyword.aios_short}}, the positive outcomes are designated as the favorable outcomes, and the negative outcomes are designated as the unfavorable outcomes. The privileged group is designated as the reference group, and the unprivileged group is designated as the monitored group.


### Bias visualization ![beta tag](images/beta.png)
{: #mf-monitor-bias-viz}

When potential bias is detected, {{site.data.keyword.aios_short}} performs several functions to confirm whether the bias is real. {{site.data.keyword.aios_short}} perturbs the data by flipping the monitored value to the reference value and then running this new record through the model. It then surfaces the resulting output as the de-biased output. {{site.data.keyword.aios_short}} also trains a shadow de-biased model that it then uses to detect when a model is going to make a biased prediction. 

Two different datasets are used for computing fairness and accuracy. Fairness is computed by using the payload + perturbed data. Accuracy is computed by using the feedback data. To compute accuracy, {{site.data.keyword.aios_short}} needs manually labelled data, which is only present in feedback table.

The results of these determinations are available in the bias visualization, which includes the following views: 

- **Payload + Perturbed**: Includes the scoring request received for the selected hour plus additional records from previous hours if the minimum number of records required for evaluation was not met. Includes additional perturbed/synthesized records used to test the model's response when the value of the monitored feature changes.

   Take note of the following payload and perturbed details:

   - Number of records that are read in this hour from payload table
   - Additional records that are read from previous hours (For example, if the `min_records` value in the fairness configuration is set to 1000, and between 2pm to 3pm only 10 records are added, to meet the minimum requirement, the system would read an additional 990 records from previous hours.)
   - Perturbed records per fairness attribute
   - Oldest record timestamp in the data frame for which bias has to be computed
   - Newest/latest record timestamp in the data frame for which bias has to be computed

  ![example of payload plus perturbed](images/payload&perturbed.png)



- **Payload**: The actual scoring requests received by the model for the selected hour.

   Take note of the following payload details:
   
   - Number of records that are read/on which debiased operation is performed from payload table
   - Oldest record timestamp in the data frame for which bias has to be computed
   - Newest/latest record timestamp in the data frame for which bias has to be computed


  ![example of payload data](images/payload.png)

- **Training**: The training data records used to train the model.

   Take note of the following training details:
   
   - Number of training data records. Training data is read one time, and distribution is stored in the `subscription/fairness_configuration` variable. While computing distribution we should also find the number of training data records and store it in the same distribution. Also when training data is changed, meaning if the `POST /data_distribution` command is run again, this value is updated in the `fairness_configuration/training_data_distribution` variable. While sending the metric, we should also send this value as well.
   - The time at which training data is last processed (first time and subsequent updates)

  ![example of training data](images/training.png)
   

   
- **Debiased**: The output of the debiasing algorithm after processing the runtime and perturbed data.

   Take note of the following debiased details:
   
   - Number of records that are read/on which the debiased operation is performed from payload table
   - Additional records that are read to perform bias, and thereby de-biased as well. Same number as in the `Payload + Perturbed` selection
   - Perturbed records per fairness attribute
   - Oldest record timestamp in the data frame for which bias has to be computed
   - Newest/latest record timestamp in the data frame for which bias has to be computed
   - Before and after fairness values display in the header portion of the Debiased view. 
      - The **after** accuracy is computed by taking the feedback data and sending it to the active debiasing API. This API returns the de-biased prediction. The feedback data also contains the manual label. The manual label is compared with the debiased prediction to compute the accuracy. This API returns the de-biased prediction. The feedback table also contains the manual label. The manual label is compared with the debiased prediction to compute the accuracy. 
      - The **before** accuracy is computed by using the same feedback data. For before accuracy computation, the feedback data is sent to the model to get its prediction and the predicted value is compared with the manual label to get the accuracy.

  ![example of debiased data](images/debiased.png)
  
### Example
{: #mf-ex1}

Consider a data point where, for `Gender=Male` (Reference value), the model predicts an Favorable outcome, but when the record is perturbed by changing `Gender` to `Female` (Monitored value), while keeping all other feature values the same, the model predicts an Unfavorable outcome. A model overall is said to exhibit bias if there are sufficient data points (across the last `N` records in the payload table, plus the perturbed data) where the model was acting in a biased manner.

### Supported models
{: #mf-supmo}

 {{site.data.keyword.aios_short}} supports bias detection only for those models and Python functions which expect some kind of structured data in its feature vector.

## Configuring the Fairness monitor
{: #mf-config}

From the **Fairness** tab, on the **What is Fairness?** page, click **Begin** to start the configuration process.

![What is fairness? page](images/fair-what-is.png)

Throughout this process, {{site.data.keyword.aios_full}} analyzes your model and makes recommendations based on the most logical outcome. On the successive pages of the **Fairness** tab, you must perform the following tasks:

1. Select the features to monitor. Only features which are of categorical, numeric (integer), float, or double fairness data type are supported. Features with other data types are not supported.

1. Specify reference and monitored groups.

   Each feature has specific requirements to configure. For example, if you choose `age` as one of your monitored features, you must define the age ranges for a **Reference Group** and a **Monitored Group** by entering values directly in each group.

1.  Set the fairness alert threshold for the feature.

    A Fairness threshold is used to specify an acceptable difference between the percentage of Favorable outcomes for the Monitored group as compared to the percentage of Favorable outcomes for the Reference group.

    Consider a model that predicts who should get a loan (`favorable outcome=loan granted`) and who shouldn’t (`unfavorable outcome=loan denied`). Further, the Monitored value for age is `[18,25]`, and the Reference value is `[26,100]`. When the bias detection algorithm runs, if it finds that the percentage of Favorable outcomes for people in the age group `[18,25]` in the last `N` records plus perturbed data is `50%`, while the percentage of Favorable outcomes for people in the age group `[26,100]` is `70%`, then Fairness is computed as 50*100/70 = 71.42.

    If the Fairness threshold is set to 80%, then the algorithm will flag the model as being biased, because the computed Fairness exceeds the threshold. However, if the threshold is set to 70% then it will not report the model as being biased.

     The values that you enter in these screens should be those that are sent to the model scoring endpoint (and consequently will be added to the payload table). If the data is being manipulated before sending to the scoring endpoint, then enter the manipulated values. For example, if the original data had values of `Male` and `Female` for *Gender* and it was manipulated so that the data sent to the scoring endpoint was `M` and `F`, then enter `M` and `F` on this screen.

1.  Specify values that represent a favorable outcome for the model. Values are derived from the `label` column in the [training data](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata), if the model output schema contains a mapping column. In {{site.data.keyword.pm_full}}, the `prediction` column always has a double value. The mapping column is used to specify the mapping of this `prediction` value to the class label.

    For example, if the `prediction` value is `1.0`, the mapping column could have a value of `Loan denied`; this implies that the prediction of the model is `Loan denied`. So, if the model output schema contains a mapping column, then specify Favorable and Unfavorable values using those present in the mapping column.

    If, however, the mapping column is not present in the model output schema, then the Favorable and Unfavorable values need to be specified using the value of the `prediction` column (`0.0`, `1.0`, etc.)

1.  Finally, set a minimum sample size, to prevent measuring Fairness until a minimum number of records are available in the evaluation dataset. This ensures the sample size is not too small to skew results. Every time bias checking runs, it will use the minimum sample size to decide the number of records on which it will do the bias computation.

    A summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section, otherwise, click **Save**.

    You can also click **Add another feature** to return to the feature selection screen and add more features, such as `City`, `Zip Code` or `Account Balance` to the Fairness monitor.

### Understanding how de-biasing works
{: #mf-debias}

To check the debias endpoint, click the **Debias Endpoint** button. You can then view and copy the enpoint in different formats, such as cURL, Java, or Python. 

The de-biased scoring endpoint can be used exactly as the normal scoring endpoint of your deployed model. In addition to returning the response of your deployed model, it also returns the `debiased_prediction` and `debiased_probability` columns.

- The `debiased_prediction` column contains the debiased prediction value. In the case of {{site.data.keyword.pm_full}}, this is an encoded representation of the prediction. For example, if the model prediction is either "Loan Granted" or "Loan Denied", {{site.data.keyword.pm_full}} can encode these two values to "0.0" and "1.0", respectively. The `debiased_prediction` column contains such an encoded representation of the debiased prediction.

- The `debiased_probability` column, on the other hand, represents the probability of the debiased prediction. This is an array of double value, where each value represents the probability of the de-biased prediction belonging to one of the prediction classes.

One another column, `debiased_decoded_target`, is also returned, in case you have a column in your output schema that contains a column with `modeling-role` as `decoded-target`.

- The `debiased_decoded_target` column contains the string representation of the debiased prediction. In the previous example, where the prediction value was either "0.0" or "1.0", the `debiased_decoded_target` will contain either "Loan Granted" or "Loan Denied".

Ideally, you would directly call this endpoint from your production application, instead of directly calling the scoring endpoint of your model deployed in your model serve engine ({{site.data.keyword.pm_full}}, Amazon Sagemaker, Microsoft Azure ML Studio, etc.) This way, {{site.data.keyword.aios_short}} will also store the `debiased` values in the payload logging table of your model deployment. Then, all scoring done via this endpoint would be automatically de-biased.

Because this endpoint deals with runtime bias, it will continue to run background checks for the latest scoring data from the payload logging table, and keep updating the bias mitigation model which is used to de-bias the scoring requests sent. In this way, {{site.data.keyword.aios_short}} is always up-to-date with the latest incoming data, and with its behavior to detect and mitigate bias.

Finally, {{site.data.keyword.aios_short}} uses a threshold to decide that data is now acceptable and is deemed to be unbiased. That threshold is taken as the least value from the thresholds set in the Fairness monitor for all the fairness attributes configured.

## Next steps
{: #mf-next}

From the **Configure monitors** page, you can select another monitoring category.
