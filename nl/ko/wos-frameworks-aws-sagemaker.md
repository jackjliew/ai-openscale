---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Amazon SageMaker 프레임워크
{: #frmwrks-aws-sage}

Amazon SageMaker를 사용하여 {{site.data.keyword.aios_full}}에서 페이로드 로깅, 피드백 로깅을 수행하고 성능 정확성, 런타임 편향성 감지, 설명 가능성 및 자동-편향성 함수를 측정할 수 있습니다. 

{{site.data.keyword.aios_full}}에서는 다음 Amazon SageMaker 프레임워크를 전적으로 지원합니다.
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| 원시 | 분류 | 정형 |
| 원시 | 회귀<sup>1</sup> | 정형 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

<sup>1</sup>회귀 모델에 대한 지원에는 드리프트 규모가 포함되지 않습니다. 

## {{site.data.keyword.aios_short}}에 Amazon SageMaker 추가
{: #frmwrks-aws-sage-add}

다음 방법 중 하나를 사용하여 {{site.data.keyword.aios_short}}이 Amazon SageMaker와 함께 작동하도록 구성할 수 있습니다.

- 기계 학습 제공자를 {{site.data.keyword.aios_short}}에 처음 추가하는 경우 구성 인터페이스를 사용할 수 있습니다. 자세한 정보는 [Amazon SageMaker 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)을 참조하십시오.
- Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 제공자가 둘 이상인 경우 이 방법을 사용해야 합니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Amazon SageMaker 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)을 참조하십시오.


## 샘플 노트북
{: #frmwrks-aws-sage-smpl-ntbks}

다음 노트북은 Amazon SageMaker로 작업하는 방법을 보여줍니다.

- [신용 위험 예측 모델의 작성 및 배치](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [데이터 마트 작성, 모델 배치 모니터링 및 데이터 분석](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## Amazon SageMaker ML 서비스 인스턴스 지정
{: #csm-connect}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 Amazon SageMaker 서비스 인스턴스를 지정하는 것입니다. Amazon SageMaker 서비스 인스턴스는 사용자의 AI 모델 및 배치를 저장하는 곳입니다.
{: shortdesc}

Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Amazon SageMaker 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)을 참조하십시오.

### Amazon SageMaker 서비스 인스턴스 연결
{: #csm-config}

{{site.data.keyword.aios_short}}은 Amazon SageMaker 서비스 인스턴스에서 AI 모델 및 배치에 연결됩니다.

1.  **구성** 탭의 탐색 분할창에서 **기계 학습 제공자**를 클릭하십시오. 

    ![지원되는 기계 학습 엔진에 대한 타일과 함께 기계 학습 서비스 제공자 선택 화면이 표시됨](images/wos-machine-learning-providers-selection.png)

1.  **기계 학습 제공자 추가** 단추를 클릭한 후 **Amazon SageMaker** 타일을 클릭하십시오. 

    ![Amazon SageMaker 서비스 인증 정보 입력](images/connect-sage-cred.png)

1.  인증 정보를 입력한 후 저장하십시오.

    - 액세스 키 ID: 사용자의 AWS 액세스 키 ID `aws_access_key_id`로, 사용자의 신원을 확인하고 AWS에 대한 호출을 인증하고 권한을 부여합니다.
    - 시크릿 액세스 키: 사용자의 AWS 시크릿 액세스 키 `aws_secret_access_key`로, 사용자의 신원을 확인하고 AWS에 대한 호출을 인증하고 권한을 부여하는 데 필요합니다.
    - 지역: 액세스 키 ID가 작성된 영역을 입력하십시오. 키는 작성된 영역에서 저장 및 사용되고 다른 영역으로 전송할 수는 없습니다.

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택하십시오.

## Amazon SageMaker 기계 학습 엔진을 사용하여 페이로드 로깅
{: #cml-smconfig}

### Amazon SageMaker 기계 학습 엔진 바인딩
{: #cml-smbind}

- 비{{site.data.keyword.pm_full}} 엔진이 사용자 정의로 바인딩됩니다. 즉, 단지 메타데이터이며 비{{site.data.keyword.pm_full}} 서비스와의 직접 통합은 없습니다.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  다음 명령을 사용하여 서비스 바인딩을 볼 수 있습니다.

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker ML 바인딩](images/ml-sagemaker-bind.png)

### Amazon SageMaker ML 구독 추가
{: #cml-smsub}

- 구독 추가

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- 구독 목록 가져오기

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### 페이로드 로깅 사용 설정
{: #cml-smenlog}

- 구독에서 페이로드 로깅 사용 설정

    ```python
    subscription.payload_logging.enable()
    ```

- 로깅 세부사항 가져오기

    ```python
    subscription.payload_logging.get_details()
    ```

### 스코어링 및 페이로드 로깅
{: #cml-smscore}

- 모델을 스코어링하십시오. 전체 예는 [SageMaker Machine Learning Engine 노트북에 대한 작업](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}을 참조하십시오.


- 페이로드 로깅 테이블에 요청 및 응답 저장:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

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

## 다음 단계
{: #csm-next}

- 이제 {{site.data.keyword.aios_short}}이 [모니터를 구성](/docs/services/ai-openscale?topic=ai-openscale-mo-config)할 준비가 되었습니다.
- [Watson OpenScale로 Sagemaker 기계 학습 모니터](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
