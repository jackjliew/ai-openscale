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

# Microsoft Azure ML 서비스 프레임워크
{: #frmwrks-azure-service}

Microsoft Azure ML 서비스를 사용하여 {{site.data.keyword.aios_full}}에서 페이로드 로깅, 피드백 로깅을 수행하고 성능 정확성, 런타임 편향성 감지, 설명 가능성 및 자동-편향성 함수를 측정할 수 있습니다. 

{{site.data.keyword.aios_full}}에서는 다음 Microsoft Azure Machine Learning 서비스 프레임워크를 완전히 지원합니다.
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| 원시 | 분류 | 정형 |
| scikit-learn | 분류 | 정형 |
| scikit-learn | 회귀 | 정형 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

## {{site.data.keyword.aios_short}}에 Microsoft Azure ML 서비스 추가
{: #frmwrks-azureservice-addsrvc}

다음 방법 중 하나를 사용하여 {{site.data.keyword.aios_short}}이 Microsoft Azure ML 서비스와 함께 작동하도록 구성할 수 있습니다.

- 기계 학습 제공자를 {{site.data.keyword.aios_short}}에 처음 추가하는 경우 구성 인터페이스를 사용할 수 있습니다. 자세한 정보는 [Microsoft Azure ML 서비스 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)을 참조하십시오.
- Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 제공자가 둘 이상인 경우 이 방법을 사용해야 합니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Microsoft Azure 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)을 참조하십시오.


{{site.data.keyword.aios_short}}은 Azure ML 서비스와 상호작용하기 위해 필요한 다양한 REST 엔드포인트를 호출합니다. 이를 수행하려면 Azure 기계 학습 서비스 {{site.data.keyword.aios_short}}을 바인딩해야 합니다.

1. Azure Active Directory 서비스 프린시펄 작성
2. UI 또는 {{site.data.keyword.aios_short}} Python SDK를 통해 Azure ML 서비스 바인딩을 추가할 때 인증 정보 세부사항을 지정하십시오.

## JSON 요청 및 응답 파일에 대한 요구사항
{: #frmwrks-azureservice-JSON}

{{site.data.keyword.aios_short}}이 Azure ML 서비스에 대해 작업하려면 작성되는 웹 서비스 배치가 특정 요구사항을 충족해야 합니다. 작성되는 웹 서비스 배치는 아래에 설명된 요구사항에 따라 JSON 요청을 승인하고 JSON 응답을 리턴해야 합니다.

### 필수 웹 서비스 JSON 요청 형식
{: #frmwrks-azureservice-JSON-sample-request}

- REST API 요청 본문은 JSON 오브젝트의 한 JSON 배열이 포함된 JSON 문서여야 합니다.
- JSON 배열의 이름은 `"input"`으로 지정해야 합니다.
- 각각의 JSON 오브젝트는 단순 키-값 쌍만 포함할 수 있습니다. 여기서 값은 문자열, 숫자, `true`, `false` 또는 `null`만 될 수 있습니다.
- 값은 JSON 오브젝트 또는 배열이 아니어야 합니다.
- 배열에 있는 각각의 JSON 오브젝트는 `null`이 아닌 값을 사용할 수 있는지 여부에 관계없이 모두 동일한 키(및 키 수)를 가지고 있어야 합니다.


다음 샘플 JSON 파일은 선행 요구사항을 충족하며 자체 JSON 요청 파일 작성을 위한 템플리트로 사용될 수 있습니다.


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


### 필수 웹 서비스 JSON 응답 형식
{: #frmwrks-azureservice-JSON-sample-response}

JSON 응답 파일을 작성할 때 다음과 같은 항목에 유의하십시오.

- REST API 응답 본문은 JSON 오브젝트의 한 JSON 배열이 포함된 JSON 문서여야 합니다.
- JSON 배열의 이름은 `"output"`으로 지정해야 합니다.
- 각각의 JSON 오브젝트는 키-값 쌍만 포함할 수 있습니다. 여기서 값은 문자열, 숫자, `true`, `false`, `null` 또는 다른 JSON 오브젝트 또는 배열이 포함되지 않은 배열만 될 수 있습니다.
- 값은 JSON 오브젝트가 아니어야 합니다.
- 배열에 있는 각각의 JSON 오브젝트는 `null`이 아닌 값을 사용할 수 있는지 여부에 관계없이 모두 동일한 키(및 키 수)를 가지고 있어야 합니다.
- 분류 모델의 경우: 웹 서비스는 각 클래스에 대한 확률의 배열을 리턴해야 하고 확률의 순서는 배열의 각 JSON 오브젝트에 대해 일관되어야 합니다.
  - 예: 클래스가 `Risk` 또는 `No Risk`인 신용 위험을 예측하는 2진 분류 모델을 가지고 있다고 가정해 봅니다.
  - "output" 배열에서 다시 리턴된 모든 결과의 경우 오브젝트는 다음 양식의 고정 순서로 확률을 포함하는 키-값 쌍을 포함해야 합니다.
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

Azure ML Studio와 서비스 모두에서 사용된 Azure ML 시각적 도구와 일관성을 유지하기 위해 이를 권장하지만 다음과 같은 키 이름은 사용하지 않아도 됩니다.

- 모델의 예측된 값을 표시하는 출력 키에 대한 키 이름 `"Scored Labels"`
- 각 클래스에 대한 확률의 배열을 표시하는 출력 키에 대한 키 이름 `"Scored Probabilities"`

다음 샘플 JSON 파일은 선행 요구사항을 충족하며 자체 JSON 응답 파일 작성을 위한 템플리트로 사용될 수 있습니다.


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

## 샘플 노트북
{: #frmwrks-azureservice-smpl-ntbks}

다음 노트북은 Microsoft Azure ML 서비스로 작업하는 방법을 보여줍니다.

- [MS Azure 서비스 모델 스코어링 예](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## Microsoft Azure ML 서비스 인스턴스 지정
{: #connect-azureservice}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 Microsoft Azure ML 서비스 인스턴스를 지정하는 것입니다. Azure ML 서비스 인스턴스는 AI 모델 및 배치를 저장하는 위치입니다.
{: shortdesc}

Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 이를 프로그래밍 방식으로 수행하는 방법에 대한 자세한 정보는 [Microsoft Azure 서비스 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)을 참조하십시오.

## Azure ML 서비스 인스턴스 연결
{: #ca-connect}

{{site.data.keyword.aios_short}}은 Azure ML 서비스 인스턴스의 AI 모델 및 배치에 연결됩니다.

1.  **구성** 탭의 탐색 분할창에서 **기계 학습 제공자**를 클릭하십시오. 
1.  **기계 학습 제공자 추가** 단추를 클릭한 후 **Microsoft Azure ML 서비스** 타일을 클릭하십시오. 
1.  인증 정보를 입력한 후 저장하십시오.

    - 클라이언트 ID: 클라이언트 ID의 실제 문자열 값이며 사용자의 신원을 확인하고 Azure 서비스에 대해 작성하는 호출을 인증하고 이 호출에 권한을 부여합니다.
    - 클라이언트 시크릿: 시크릿의 실제 문자열 값이며 사용자의 신원을 확인하고 Azure 서비스에 대해 작성하는 호출을 인증하고 이 호출에 권한을 부여합니다.
    - 테넌트: 테넌트 ID는 사용자의 조직에 해당하며 Azure AD의 전용 인스턴스입니다. 테넌트 ID를 찾으려면 계정 이름 위에 마우스 커서를 올려 디렉토리/테넌트 ID를 표시하거나, Azure 포털에서 Azure Active Directory > 특성 >  디렉토리 ID를 선택하십시오.
    - 구독 ID: Microsoft Azure 구독을 고유하게 식별하는 구독 인증 정보입니다. 구독 ID는 모든 서비스 호출의 URI 파트를 구성합니다.

    Microsoft Azure 인증 정보를 가져오는 방법에 대한 지침은 [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}를 참조하십시오.
    {: note}

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택한 후 **구성**을 클릭하십시오.

배치를 선택했습니다.

## Microsoft Azure ML 서비스 엔진을 사용하여 페이로드 로깅
{: #cml-azsrvconfig}

### Microsoft Azure ML 서비스 엔진 바인딩
{: #cml-azsrvbind}

비{{site.data.keyword.pm_full}} 엔진이 사용자 정의로 바인딩됩니다. 즉, 단지 메타데이터이며 비{{site.data.keyword.pm_full}} 서비스와의 직접 통합은 없습니다.
   
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

다음 명령을 사용하여 서비스 바인딩을 볼 수 있습니다.

```
    client.data_mart.bindings.list()
```
{: codeblock}

샘플 출력:

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### Microsoft Azure ML 서비스 구독 추가
{: #cml-azsrvsub}

구독 추가

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

구독 목록 가져오기

```
    subscriptions = client.data_mart.subscriptions.get_details()

subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
```
{: codeblock}

### 페이로드 로깅 사용 설정
{: #cml-azsrvenlog}

구독에서 페이로드 로깅 사용 설정

```
    subscription.payload_logging.enable()
```
{: codeblock}

로깅 세부사항 가져오기

```
    subscription.payload_logging.get_details()
```
{: codeblock}

### 스코어링 및 페이로드 로깅
{: #cml-azsrvscore}

모델을 스코어링하십시오. 전체 예는 [Azure 기계 학습 서비스 엔진에 대한 작업 노트북](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}을 참조하십시오.

페이로드 로깅 테이블에 요청 및 응답 저장:

```
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

subscription.payload_logging.store(records=records_list)
```
{: codeblock}
{: python}
   
Python 이외의 언어의 경우에는 REST API를 사용하여 직접 페이로드 로깅을 수행할 수도 있습니다.
   
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



## 다음 단계
{: #ca-next}

- 이제 {{site.data.keyword.aios_short}}에서 사용자가 [모니터를 구성](/docs/services/ai-openscale?topic=ai-openscale-mo-config)할 수 있도록 준비가 되었습니다. 
- [Azure 기계 학습 서비스와 Studio의 차이](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

