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

You can use Microsoft Azure ML Service to perform payload logging, feedback logging, and to measure performance accuracy, run-time bias detection, explainability, and auto-debias function in {{site.data.keyword.aios_full}}.

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

- [MS Azure Service model scoring examples](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## Specifying a Microsoft Azure ML Service instance
{: #connect-azureservice}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify a Microsoft Azure ML Service instance. Your Azure ML Service instance is where you store your AI models and deployments.
{: shortdesc}

You can also add your machine learning provider by using the Python SDK. For more information on performing this programmatically, see [Bind your Microsoft Azure Service machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

### Requirements 
{: #connect-azureservice-reqs}

To connect your Microsoft Azure instance to {{site.data.keyword.aios_short}}, you must provide the following credentials:

#### Client ID

The actual string value of your client ID, which verifies who you are and authenticates and authorizes calls that you make to Azure Service.

#### Client Secret

The actual string value of the secret, which verifies who you are and authenticates and authorizes calls that you make to Azure Service.

#### Tenant

Your tenant ID corresponds to your organization and is a dedicated instance of Azure AD. To find the tenant ID, hover over your account name to get the directory / tenant ID, or select **Azure Active Directory** > **Properties** > **Directory ID** in the Azure portal.

#### Subscription ID

Subscription credentials that uniquely identify your Microsoft Azure subscription. The subscription ID forms part of the URI for every service call.

For instructions about how to get your Microsoft Azure credentials, see [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.

### Steps to connect your Azure ML Service instance
{: #ca-connect}

{{site.data.keyword.aios_short}} connects to AI models and deployments in a Azure ML Service instance.

1.  From the **Configure** ![configuration icon is shown](images/insight-config-tab.png) tab, in the navigation pane, click **Machine learning providers**.
1.  Click the **Add machine learning provider** button, and then click the **Microsoft Azure ML Service** tile.

       ![the select your machine learning service provider screen is shown with tiles for the supported machine learning engines](images/wos-machine-learning-providers-selection-azr-srvc.png)


1.  Enter and save your credentials:

    ![Enter Azure ML Studio credentials](images/wos-connect-azure—srvc-cred.png)


## Payload logging with the Microsoft Azure ML Service engine
{: #cml-azsrvconfig}

### Bind your Microsoft Azure ML Service engine
{: #cml-azsrvbind}

A non-{{site.data.keyword.pm_full}} engine is bound as Custom, meaning that this is just metadata; there is no direct integration with the non-{{site.data.keyword.pm_full}} service.
   
```
AZURE_ENGINE_CREDENTIALS = {
"client_id": "***",
"client_secret": "***",
"subscription_id": "***",
"tenant": "***"
}

binding_uid = client.data_mart.bindings.add('My Azure ML Service engine', AzureMachineLearningServiceInstance(AZURE_ENGINE_CREDENTIALS))


bindings_details = client.data_mart.bindings.get_details()
```
{: codeblock}

You can see your service binding with the following command:

```
client.data_mart.bindings.list()
```
{: codeblock}

The sample output:

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### Add Microsoft Azure ML Service subscription
{: #cml-azsrvsub}

Add subscription

```
client.data_mart.subscriptions.add(
   AzureMachineLearningAsset(source_uid=source_uid,
                                binding_uid=binding_uid,
                                input_data_type=InputDataType.STRUCTURED,
                                problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                label_column='<my_label_column_name>',
                                prediction_column='Scored Labels'))
```
{: codeblock}

Get subscription list

```
subscriptions = client.data_mart.subscriptions.get_details()

subscriptions_uids = client.data_mart.subscriptions.get_uids()
print(subscriptions_uids)
```
{: codeblock}

### Enable payload logging
{: #cml-azsrvenlog}

Enable payload logging in subscription

```
subscription.payload_logging.enable()
```
{: codeblock}

Get logging details

```
subscription.payload_logging.get_details()
```
{: codeblock}

### Scoring and payload logging
{: #cml-azsrvscore}

Score your model. For a full example, see the [Working with Azure Machine Learning Service Engine notebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

Store the request and response in the payload logging table:

```
records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                     PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

for i in range(1, 10):
   records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

subscription.payload_logging.store(records=records_list)
```
{: codeblock}
{: python}
   
For languages other than Python, you can also perform payload logging directly, using a REST API.
   
```
token_endpoint = "https://iam.cloud.ibm.com/identity/token"
headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
}

data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
}
   
req = requests.post(token_endpoint, data=data, headers=headers)
token = req.json()['access_token']
```
{: codeblock}
{: json}


```
import requests, uuid
   
PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])
   
payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
}]

headers = {"Authorization": "Bearer " + token}
req_response = requests.post(endpoint, json=payload, headers = headers)
print("Request OK: " + str(req_response.ok))
```
{: codeblock}



## Next steps
{: #ca-next}

- {{site.data.keyword.aios_short}} is now ready for you to [add deployments to your dashboard](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy) and [configure monitors](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

