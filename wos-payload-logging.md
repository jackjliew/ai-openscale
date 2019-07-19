---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests, schema, REST API, API

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

# Payload and feedback logging in {{site.data.keyword.aios_short}}
{: #cdb-payload}

For {{site.data.keyword.aios_short}}, all transactions going to the deployed models must be logged as payload records in the {{site.data.keyword.aios_short}} data mart. The input and output payloads (requests and responses) need to be in the format required by {{site.data.keyword.aios_short}} as described in the specifications. 
{: shortdesc}

{{site.data.keyword.aios_short}} supports payload and feedback logging through the following methods:

- [Using the Python Client](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [Using the REST API](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [Automatically for supported machine learning providers](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## Logging the payload with Python SDK
{: #cdb-payload-log-pythonsdk}

For an example of full working code, see the [AI Openscale and Custom ML Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb) sample notebook.

The following code sample shows how to log the payload by using the Python SDK:

```
records_list = [
   PayloadRecord(request=request_data, 
                 response=response_data,
                 response_time=response_time), 
   PayloadRecord(request=request_data,
                 response=response_data,
                 response_time=response_time)]
subscription.payload_logging.store(records=records_list)
```

### Previewing the payload logging table
{: #cdb-preview-payload-log-table}

You can preview the content of your payload logging table either by directly connecting to the database or by using the Python SDK, which is shown in the following sample output. 

![Python SDK sample output of payload logging table](images/wosntbok.png)


## Logging the payload with the REST API
{: #cdb-payload-log-rest-api}

The following code sample shows how to log the payload by using the REST API:

```
PAYLOAD_STORING_HREF_PATTERN ='{}/v1/data_marts/{}/scoring_payloads'
endpoint = PAYLOAD_STORING_HREF_PATTERN.format(
                                AIOS_CREDENTIALS['url'], 
                                AIOS_CREDENTIALS['data_mart_id'])
deployment_uid = subscription.get_details()['entity']['deployments'][0]['deployment_id']
payload = [{'binding_id': binding_uid, 
            'deployment_id': deployment_uid,
            'subscription_id': subscription.uid,
            'scoring_id': scoring_uid,
            'response': response_data,
            'request': request_data}]
headers = {'Authorization': 'Bearer '+ token}
req_response = requests.post(endpoint, 
                             json=payload,
                             headers = headers)
```



## Next steps
{: #cdb-payload-nxt-stps}

For more information, see [Payload Logging/publishScoringPayload](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API){: external}


