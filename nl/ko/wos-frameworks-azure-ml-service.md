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

- [데이터 마트 작성, 모델 배치 모니터링 및 데이터 분석](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure 서비스 모델 스코어링 예](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 추가 탐색
{: #frmwrks-azureservice-mediumblogs}

- [Azure 기계 학습 서비스와 Studio의 차이](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
