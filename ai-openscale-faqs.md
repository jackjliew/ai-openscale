---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: FAQs, frequently asked questions, questions

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

# FAQs
{: #wos-faqs}

Here you'll find some of the most frequently-asked questions from users of {{site.data.keyword.aios_full}}.
{: shortdesc}

## Questions
{: #wos-faqs-questions}

- [How do I convert a prediction column from an integer data type to a categorical data type?](#wos-faqs-convert-data-types)
- [Why does {{site.data.keyword.aios_short}} need access to my training data?](#trainingdata)

### How do I convert a prediction column from an integer data type to a categorical data type?
{: #wos-faqs-convert-data-types}

When configuring fairness monitoring for a model, the prediction column only allows for integer numerical value even though the prediction label is categorical How do I configure this for categorical feature (that is not integer)? is a manual conversion required? 

The training data could have class labels such as “Loan Denied”, “Loan Granted”. The prediction value returned by WML scoring end point has values such as “0.0”, “1.0", etc. The scoring end point also has an optional column which contains the text representation of prediction. E.g., if prediction=1.0, the predictionLabel column could have a value “Loan Granted”. If such a column is available, then while configuring the favourable and unfavourable outcome for the model, you can specify the string values “Loan Granted” and “Loan Denied”. If such a column is not available then you need to specify the integer/double values of 1.0, 0.0 for the favourable/unfavourable class.

WML has a concept of output schema which defines the schema of the output of WML scoring end point and the role for the different columns. The roles are used to identify which column contains the prediction value, which column contains the prediction probability, and the class label value, etc. The output schema is automatically set for models created using model builder. It can also be set using the WML python client. Users can use the output schema to define a column which contains the string representation of the prediction. This is done by setting the modeling_role for the column to ‘decoded-target’. The documentation for the WML python client is available at: http://wml-api-pyclient-dev.mybluemix.net/#repository. Search for “OUTPUT_DATA_SCHEMA” to understand the output schema and the API to use is to store_model API which accepts the OUTPUT_DATA_SCHEMA as a parameter.

### Why does {{site.data.keyword.aios_short}} need access to my training data?
{: #trainingdata}

You must either provide {{site.data.keyword.aios_short}} access to training data that is stored in Db2 or {{site.data.keyword.cos_full_notm}}, or you must run a notebook that can access the training data. {{site.data.keyword.aios_short}} needs access to your training data for the following reasons:

- To generate contrastive explanations: To create explanations, access to statistics, such as median value, standard deviation, and distinct values from the training data is required.
- To display training data statistics: To populate the bias details page, {{site.data.keyword.aios_short}} must have training data from which to generate statistics.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

In the notebook-based approach, you are expected to upload the statistics and other information when configuring a deployment in {{site.data.keyword.aios_short}}. This implies that {{site.data.keyword.aios_short}} no longer has access to the training data outside the notebook, which is run in your environment. It only has access to the information uploaded during the configuration.


