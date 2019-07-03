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

# {{site.data.keyword.aios_short}}에서 페이로드 및 피드백 로깅
{: #cdb-payload}

{{site.data.keyword.aios_short}}의 경우, 배치된 모델로 이동하는 모든 트랜잭션은 {{site.data.keyword.aios_short}} 데이터 마트에서 페이로드 레코드로 로깅해야 합니다. 입력 및 출력 페이로드(요청과 응답)는 스펙에 설명된 대로 {{site.data.keyword.aios_short}}에 필요한 형식으로 되어 있어야 합니다.
{: shortdesc}

{{site.data.keyword.aios_short}}은 다음 방법을 통해 페이로드 및 피드백 로깅을 지원합니다. 

- [Python 클라이언트 사용](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [REST API 사용](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [지원되는 기계 학습 제공자에 대해 자동으로](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## Python SDK를 사용한 페이로드 로깅
{: #cdb-payload-log-pythonsdk}

작동하는 전체 코드의 예는 [AI Openscale 및 사용자 정의 ML 엔진](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb) 샘플 노트북을 참조하십시오.

다음 코드 샘플에서는 Python SDK를 사용하여 페이로드를 로깅하는 방법을 보여줍니다.

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

### 페이로드 로깅 테이블 미리보기

다음 샘플 결과에 표시된 대로 직접 데이터베이스에 연결하거나 Python SDK를 사용하여 페이로드 로깅 표의 컨텐츠를 미리볼 수 있습니다. 

![페이로드 로깅 표의 Python SDK 샘플 출력](images/wosntbok.png)


## REST API를 사용한 페이로드 로깅
{: #cdb-payload-log-rest-api}

다음 코드 샘플에서는 REST API를 사용하여 페이로드를 로깅하는 방법을 보여줍니다.

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



## 다음 단계
{: #cdb-payload-nxt-stps}

자세한 정보는 [페이로드 로깅](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API)(/publishScoringPayload)을 참조하십시오. {: external}


