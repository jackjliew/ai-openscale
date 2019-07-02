---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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

# Payload logging with the Microsoft Azure ML Service engine
{: #cml-azsrvconfig}

## Bind your Microsoft Azure ML Service engine
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
    
    
## Add Microsoft Azure ML Service subscription
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

## Enable payload logging
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

## Scoring and payload logging
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

