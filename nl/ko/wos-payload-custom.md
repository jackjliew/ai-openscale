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

# 사용자 정의 기계 학습 엔진을 사용하여 페이로드 로깅
{: #cml-cusconfig}

## 사용자 정의 기계 학습 엔진을 바인딩하십시오.
{: #cml-cusbind}

- 비{{site.data.keyword.pm_full}} 엔진이 사용자 정의로 바인딩됩니다. 즉, 단지 메타데이터이며 비{{site.data.keyword.pm_full}} 서비스와의 직접 통합은 없습니다. `client.data_mart.bindings.add` 메소드를 사용하여 두 개 이상의 기계 학습 엔진을 {{site.data.keyword.aios_short}}에 바인딩할 수 있습니다.

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  다음 명령을 사용하여 서비스 바인딩을 볼 수 있습니다.

    ```python
    client.data_mart.bindings.list()
    ```

    ![Generic ML binding](images/ml-generic-bind.png)

## 사용자 정의 구독 추가
{: #cml-cussub}

- 구독 추가

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- 구독 목록 가져오기

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

## 페이로드 로깅 사용 설정
{: #cml-cusenlog}

- 구독에서 페이로드 로깅 사용 설정

    ```python
    subscription.payload_logging.enable()
    ```

- 로깅 세부사항 가져오기

    ```python
    subscription.payload_logging.get_details()
    ```

자세한 정보는 [페이로드 로깅]()을 참조하십시오.

## 스코어링 및 페이로드 로깅
{: #cml-cusscore}

- 모델을 스코어링하십시오. 전체 예는 [IBM {{site.data.keyword.aios_full}} & 사용자 정의 ML 엔진 노트북](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}을 참조하십시오.

- 페이로드 로깅 테이블에 요청 및 응답 저장

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **참고**: Python 외의 언어인 경우에도 REST API를 사용하여 직접 페이로드 로깅을 수행할 수 있습니다.

    ```json
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

    ```json
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

