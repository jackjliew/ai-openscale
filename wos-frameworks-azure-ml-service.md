---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Microsoft Azure ML Service frameworks
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} fully supports the following Microsoft Azure Machine Learning Service frameworks:
{: shortdesc}

Table 1. Framework support details

| Framework | Problem type | Data type |
|:---|:---:|:---:|
| Native | Classification | Structured |
| scikit-learn | Classification | Structured |
| scikit-learn | Regression | Structured |
{: caption="Framework support details" caption-side="top"}

## Adding Microsoft Azure ML Service to {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

You can configure {{site.data.keyword.aios_short}} to work with Microsoft Azure ML Service by using one of the following methods:

- If this is the first time that you are adding a machine learning provider to {{site.data.keyword.aios_short}}, you can use the configuration interface. For more information, see [Specifying a Microsoft Azure ML Service instance](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice).
- You can also add your machine learning provider by using the Python SDK. You must use this method if you want to have more than one provider. For more information on performing this programmatically, see [Bind your Microsoft Azure machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).


{{site.data.keyword.aios_short}} calls various REST endpoints that are needed to interact with the Azure ML Service. To do this, you must bind the Azure Machine Learning Service {{site.data.keyword.aios_short}}.

1. Create an Azure Active Directory Service Principal.
2. Specify the credential details when adding the Azure ML Service service binding, either through the UI or the {{site.data.keyword.aios_short}} Python SDK.

## Requirements for JSON request and response files
{: #frmwrks-azureservice-JSON}

For {{site.data.keyword.aios_short}} to work with Azure ML Service, the web service deployments you create must meet certain requirements. The web service deployments you create must accept JSON requests and return JSON responses, according to the requirements described below.

### Required web service JSON request format
{: #frmwrks-azureservice-JSON-sample-request}

- The REST API request body must be a JSON document that contains one JSON array of JSON objects
- The JSON array must be named `"input"`.
- Each JSON object can only include simple key-value pairs, where the values can only be a string, a number, `true`, `false`, or `null`
- The values cannot be a JSON object or array
- Each JSON object in the array must have all have the same keys (and hence number of keys) specified, regardless of whether or not there is a non-`null` value available


The following sample JSON file meets the preceding requirements and can be used as a template for creating your own JSON request files:


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### Required web service JSON response format
{: #frmwrks-azureservice-JSON-sample-response}

Make note of the following items when you create a JSON response file:

- The REST API response body must be a JSON document that contains one JSON array of JSON objects
- The JSON array must be named `"output"`.
- Each JSON object can only include key-value pairs, where the values can only be a string, a number, `true`, `false`, `null`, or an array that does not contain any other JSON objects or arrays
- The values cannot be a JSON object
- Each JSON object in the array must have all have the same keys (and number of keys) specified, regardless of whether or not there is a non-`null` value available
- For classification models: the web service must return an array of probabilities for each class and the ordering of the probabilities must be consistent for each JSON object in the array
  - Example: suppose you have a binary classification model that predicts credit risk, where the classes are `Risk` or `No Risk`
  - For every result returned back in the "output" array, the objects must contain a key-value pair that includes the probabilities in fixed order, in the form:
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

To be consistent with Azure ML visual tools used in both Azure ML Studio and Service, it is recommended, though not required to use the following key names:

- the key name `"Scored Labels"` for the output key that denotes the predicted value of the model
- the key name `"Scored Probabilities"` for the output key that denotes an array of probabilities for each class

The following sample JSON file meets the preceding requirements and can be used as a template for creating your own JSON response files:


```JSON
{
  "output": [
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## Sample notebooks
{: #frmwrks-azureservice-smpl-ntbks}

The following notebooks show how to work with Microsoft Azure ML Service:

- [Data mart creation, model deployment monitoring and data analysis](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure Service model scoring examples](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Explore further
{: #frmwrks-azureservice-mediumblogs}

- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
