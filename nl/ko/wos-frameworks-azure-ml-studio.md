---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

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

# Microsoft Azure ML Studio 프레임워크
{: #frmwrks-azure}

Microsoft Azure ML Studio를 사용하여 {{site.data.keyword.aios_full}}에서 페이로드 로깅, 피드백 로깅을 수행하고 성능 정확성, 런타임 편향성 감지, 설명 가능성 및 자동-편향성 함수를 측정할 수 있습니다. 

{{site.data.keyword.aios_full}}에서는 다음 Microsoft Azure Machine Learning Studio 프레임워크를 전적으로 지원합니다.
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| 원시 | 분류 | 정형 |
| 원시 | 회귀 | 정형 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

## {{site.data.keyword.aios_short}}에 Microsoft Azure ML Studio 추가
{: #frmwrks-azure-add}

다음 방법 중 하나를 사용하여 {{site.data.keyword.aios_short}}이 Microsoft Azure ML Studio와 함께 작동하도록 구성할 수 있습니다.

- 기계 학습 제공자를 {{site.data.keyword.aios_short}}에 처음 추가하는 경우 구성 인터페이스를 사용할 수 있습니다. 자세한 정보는 [Microsoft Azure ML Studio 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)을 참조하십시오.
- Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 제공자가 둘 이상인 경우 이 방법을 사용해야 합니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Microsoft Azure 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)을 참조하십시오.


## 샘플 노트북
{: #frmwrks-azure-smpl-ntbks}

다음 노트북은 Microsoft Azure ML Studio로 작업하는 방법을 보여줍니다.

- [데이터 마트 작성, 모델 배치 모니터링 및 데이터 분석](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure 서비스 모델 스코어링 예](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 추가 탐색
{: #frmwrks-azure-mediumblogs}

-[Watson OpenScale로 Azure 기계 학습 모니터](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [Azure 기계 학습 서비스와 Studio의 차이](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [웹 서비스로 배치된 Azure 기계 학습 모델 이용](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## Microsoft Azure ML Studio 인스턴스 지정
{: #connect-azure}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 Microsoft Azure ML Studio 인스턴스를 지정하는 것입니다. Azure ML Studio 인스턴스는 AI 모델과 배치를 저장하는 곳입니다.
{: shortdesc}

Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Microsoft Azure 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)을 참조하십시오.

### Azure ML Studio 인스턴스 연결
{: #ca-connect}

{{site.data.keyword.aios_short}}은 Azure ML Studio 인스턴스의 AI 모델 및 배치에 연결합니다.

1.  **구성** 탭의 탐색 분할창에서 **기계 학습 제공자**를 클릭하십시오. 

    ![지원되는 기계 학습 엔진에 대한 타일과 함께 기계 학습 서비스 제공자 선택 화면이 표시됨](images/wos-machine-learning-providers-selection.png)

1.  **기계 학습 제공자 추가** 단추를 클릭한 후 **Microsoft Azure ML Studio** 타일을 클릭하십시오. 

    ![Azure ML Studio 신임 정보 입력](images/connect-azure-cred.png)

1.  인증 정보를 입력한 후 저장하십시오.

    - 클라이언트 ID: 클라이언트 ID의 실제 문자열 값으로, 사용자의 신원을 확인하고 Azure Studio에 대한 호출을 인증하고 권한을 부여합니다.
    - 클라이언트 시크릿: 시크릿의 실제 문자열 값으로, 사용자의 신원을 확인하고 Azure Studio에 대한 호출을 인증하고 권한을 부여합니다.
    - 테넌트: 테넌트 ID는 사용자의 조직에 해당하며 Azure AD의 전용 인스턴스입니다. 테넌트 ID를 찾으려면 계정 이름 위에 마우스 커서를 올려 디렉토리/테넌트 ID를 표시하거나, Azure 포털에서 Azure Active Directory > 특성 >  디렉토리 ID를 선택하십시오.
    - 구독 ID: Microsoft Azure 구독을 고유하게 식별하는 구독 인증 정보입니다. 구독 ID는 모든 서비스 호출의 URI 파트를 구성합니다.

    Microsoft Azure 인증 정보를 가져오는 방법에 대한 지침은 [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}를 참조하십시오.
    {: note}

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택한 후 **구성**을 클릭하십시오.

배치를 선택했습니다.

## Microsoft Azure Machine Learning Studio Engine을 사용하여 페이로드 로깅
{: #cml-azconfig}

### Microsoft Azure 기계 학습 엔진 바인딩
{: #cml-azbind}

- 비{{site.data.keyword.pm_full}} 엔진이 사용자 정의로 바인딩됩니다. 즉, 단지 메타데이터이며 비{{site.data.keyword.pm_full}} 서비스와의 직접 통합은 없습니다.

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  다음 명령을 사용하여 서비스 바인딩을 볼 수 있습니다.

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML 바인딩](images/ml-azure-bind.png)

### Microsoft Azure ML Studio 구독 추가
{: #cml-azsub}

- 구독 추가

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
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
{: #cml-azenlog}

- 구독에서 페이로드 로깅 사용 설정

    ```python
    subscription.payload_logging.enable()
    ```

- 로깅 세부사항 가져오기

    ```python
    subscription.payload_logging.get_details()
    ```

### 스코어링 및 페이로드 로깅
{: #cml-azscore}

- 모델을 스코어링하십시오. 전체 예는 [Azure Machine Learning Studio Engine 노트북에 대한 작업](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}을 참조하십시오.

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
{: #ca-next}

이제 {{site.data.keyword.aios_short}}이 [모니터를 구성](/docs/services/ai-openscale?topic=ai-openscale-mo-config)할 준비가 되었습니다.
