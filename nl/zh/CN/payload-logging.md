---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# {{site.data.keyword.aios_short}} 中的有效内容和反馈日志记录
{: #cdb-payload}

对于 {{site.data.keyword.aios_short}}，所有转至已部署模型的事务都必须记录为 {{site.data.keyword.aios_short}} 数据集市中的有效内容记录。输入和输出有效内容（请求和响应）需要采用 {{site.data.keyword.aios_short}} 要求的格式，如规范中所述。
{: shortdesc}

{{site.data.keyword.aios_short}} 通过以下方法支持有效内容和反馈日志记录：

- [使用 Python 客户机](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [使用 REST API](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [为受支持的机器学习提供程序自动](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## 使用 Python SDK 记录有效内容
{: #cdb-payload-log-pythonsdk}

有关完整有效代码的示例，请参阅 [AI Openscale 和 Custom ML Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb) 样本笔记本。

以下代码样本显示如何使用 Python SDK 来记录有效内容：

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

### 预览有效内容日志记录表

您可以通过直接连接到数据库或使用以下样本输出中显示的 Python SDK 来预览有效内容日志记录表的内容。 

![有效内容日志记录表的 Python SDK 样本输出](images/wosntbok.png)


## 使用 REST API 记录有效内容
{: #cdb-payload-log-rest-api}

以下代码样本显示如何使用 REST API 来记录有效内容：

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



## 后续步骤
{: #cdb-payload-nxt-stps}

有关更多信息，请参阅[有效内容日志记录](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API)/publishScoringPayload){: external}


