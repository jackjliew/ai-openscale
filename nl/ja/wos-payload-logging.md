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

# {{site.data.keyword.aios_short}} でのペイロードとフィードバックのロギング
{: #cdb-payload}

{{site.data.keyword.aios_short}} では、デプロイしたモデルに送信されるすべてのトランザクションを、{{site.data.keyword.aios_short}} データマートにペイロード・レコードとして記録する必要があります。 入力ペイロードおよび出力ペイロード (要求および応答) は、仕様で説明しているように、{{site.data.keyword.aios_short}} が必要とするフォーマットでなければなりません。 
{: shortdesc}

{{site.data.keyword.aios_short}} では、以下の方式でペイロードとフィードバックをロギングできます。

- [Python クライアントを使用する](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [REST API を使用する](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [サポート対象の機械学習プロバイダーの場合は自動で実行される](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## Python SDK によるペイロードのロギング
{: #cdb-payload-log-pythonsdk}

完全な作業コードの例については、[AI Openscale とカスタム ML エンジン](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)のサンプル・ノートブックを参照してください。

以下のコード・サンプルは、Python SDK を使用してペイロードをログに記録する方法を示しています。

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

### ペイロード・ロギング・テーブルのプレビュー

ペイロード・ロギング・テーブルの内容は、データベースに直接接続するか、または Python SDK を使用してプレビューできます。Python SDK を使用した場合のプレビューは、以下の出力例に示されています。 

![ペイロード・ロギング・テーブルの Python SDK の出力例](images/wosntbok.png)


## REST API によるペイロードのロギング
{: #cdb-payload-log-rest-api}

以下のコード・サンプルは、REST API を使用してペイロードをログに記録する方法を示しています。

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



## 次のステップ
{: #cdb-payload-nxt-stps}

詳しくは、[Payload Logging](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API)/publishScoringPayload){: external} を参照してください。


