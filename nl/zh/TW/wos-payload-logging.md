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

# {{site.data.keyword.aios_short}} 中的有效負載和回饋記載
{: #cdb-payload}

對於 {{site.data.keyword.aios_short}}，在 {{site.data.keyword.aios_short}} 資料集區中，前往所部署模型的所有交易都必須記載成有效負載記錄。輸入及輸出有效負載（要求和回應）需要採用 {{site.data.keyword.aios_short}} 所需的格式，如規格中所述。
{: shortdesc}

{{site.data.keyword.aios_short}} 支援透過下列方法來記載有效負載和回饋：

- [使用 Python 用戶端](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [使用 REST API](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [為支援的機器學習提供者自動記載](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## 使用 Python SDK 來記載有效負載
{: #cdb-payload-log-pythonsdk}

如需完整有效的程式碼範例，請參閱 [AI Openscale 和自訂 ML 引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)樣本記事本。

下列程式碼範例顯示如何使用 Python SDK 來記載有效負載：

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

### 預覽有效負載記載表格

您可以直接連接至資料庫，或使用下列範例輸出所示的 Python SDK，來檢閱您有效負載記載表格的內容。 

![有效負載記載表格的 Python SDK 範例輸出](images/wosntbok.png)


## 使用 REST API 來記載有效負載
{: #cdb-payload-log-rest-api}

下列程式碼範例顯示如何使用 REST API 來記載有效負載：

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



## 後續步驟
{: #cdb-payload-nxt-stps}

如需相關資訊，請參閱[有效負載記載](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API)/publishScoringPayload){: external}


