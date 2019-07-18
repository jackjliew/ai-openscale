---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# 사용자 정의 ML 서비스 인스턴스 지정
{: #co-connect}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 서비스 인스턴스를 지정하는 것입니다. 서비스 인스턴스는 사용자의 AI 모델 및 배치를 저장하는 곳입니다.
{: shortdesc}

## 사용자 정의 서비스 인스턴스 연결
{: #co-config}

{{site.data.keyword.aios_short}}은 서비스 인스턴스에서 AI 모델 및 배치에 연결됩니다. 사용자 정의 서비스를 연결할 수 있습니다. 

1. **구성** 탭에서 **기계 학습 제공자**를 클릭하십시오. 

   ![지원되는 기계 학습 엔진에 대한 타일과 함께 기계 학습 서비스 제공자 선택 화면이 표시됨](images/wos-machine-learning-providers-selection.png)

2. **사용자 정의 환경** 타일을 선택하십시오. 

   ![사용자 정의 선택](images/ml-custom-provider.png)

3. 사용자 정의 기계 학습 제공자의 이름 및 설명을 입력한 후 **다음**을 클릭하십시오.  

4. [목록을 요청](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list)하거나 [개별 스코어링 엔드포인트를 입력하여](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints) 배치에 연결할지 선택하십시오. 

   ![사용자 정의 선택](images/ml-custom-connect-deployments.png)
    
5. **다음**을 클릭하십시오.

### 배치 목록 요청
{: #co-config-request-list}

1. **배치 목록 요청** 타일을 선택한 경우에는 인증 정보 및 API 엔드포인트를 입력한 후 **저장**을 클릭하십시오. 

   ![서비스 인증 정보 입력](images/connect-custom-cred.png)

2. 기계 학습 설정을 저장한 후 **대시보드**로 돌아가서 **인사이트** 탭을 클릭한 후 **배치 추가** 단추를 클릭하십시오. 

3. 목록에서 배치를 선택한 후 **구성**을 클릭하십시오. 

이제 모니터를 구성할 준비가 되었습니다. 

### 개별 스코어링 엔드포인트 제공
{: #co-config-scoring-endpoints}

1. **개별 스코어링 엔드포인트 입력** 타일을 선택한 경우에는 API 엔드포인트에 대한 인증 정보를 입력한 후 **저장**을 클릭하십시오. 

2. 기계 학습 설정을 저장한 후 **대시보드**로 돌아가서 **인사이트** 탭을 클릭한 후 **배치 추가** 단추를 클릭하십시오. 

3. **엔드포인트 추가** 단추를 클릭하십시오. 

4. 드롭 다운 메뉴에서 사용자 정의 환경을 선택하고 배치 이름 및 API 엔드포인트를 입력한 후 **저장**을 클릭하십시오. 

이제 모니터를 구성할 준비가 되었습니다. 

### 작동 방식
{: #co-works}

다음 이미지는 사용자 정의 환경 지원을 보여줍니다. 

![사용자 정의 작동 방식](images/custom-how-works.png)

또한 다음 링크를 참조할 수 있습니다.

[{{site.data.keyword.aios_short}} 페이로드 로깅 API](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[사용자 정의 배치 API](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[Python 클라이언트 바인딩 SDK](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[사용자 정의 기계 학습 엔진에 대한 작업](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[IBM Watson OpenScale용 Python SDK](https://pypi.org/project/ibm-ai-openscale/){: external}

- **모니터를 지원하기 위한 모델의 입력 기준**

  모델은 기본적으로 이름 지정된 필드 및 해당 값의 콜렉션인 특성 벡터를 입력으로 사용해야 합니다(편향성에 대해 모니터되는 필드가 해당 필드 중 하나입니다).

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  이 예에서 `"age"`는 누군가가 공정성을 평가하고 있는 필드일 수 있습니다.

  입력이 입력 특성 공간에서 변환된 텐서/메트릭스인 경우(텍스트 또는 이미지로부터의 심층 학습인 경우에 자주 발생), 현재 릴리스에서는 모델이 {{site.data.keyword.aios_short}} 플랫폼에 의해 처리될 수 없습니다. 확장하면 텍스트 또는 이미지 입력이 있는 심층 학습 모델은 편향성 발견 및 완화를 위해 처리될 수 없습니다.

  또한 설명 가능성을 지원하기 위해 훈련 데이터가 로드되어야 합니다.

  텍스트에 대한 설명 가능성의 경우, 전체 텍스트가 다음 특성 중 하나여야 합니다. 사용자 정의 모델의 이미지에 대한 설명 가능성은 현재 릴리스에서 지원되지 않습니다.
  {: note}

- **모니터를 지원하기 위한 모델의 출력 기준**

  모델은 해당 모델에서 다양한 클래스의 예측 확률과 함께 입력 특성 벡터를 출력해야 합니다.

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  이 예에서 `"personal"` 및 `"camping"`은 가능한 클래스이며 각 스코어링 출력의 스코어는 두 클래스 모두에 지정됩니다. 예측 확률이 누락되면, 편향성 발견은 작동하나 자동 편향성 제거는 작동하지 않습니다.

  이전 스코어링 출력은 {{site.data.keyword.aios_short}}이 REST를 통해 호출할 수 있는 라이브 스코어링 엔드포인트에서 액세스 가능해야 합니다. AzureML, SageMaker 및 {{site.data.keyword.pm_full}}의 경우 {{site.data.keyword.aios_short}}이 직접 원시 스코어링 엔드포인트에 연결되므로 스코어링 스펙 구현에 대해 걱정하지 않아도 됩니다. 

### 다음 단계
{: #co-next}

이제 {{site.data.keyword.aios_short}}이 [모니터를 구성](/docs/services/ai-openscale?topic=ai-openscale-mo-config)할 준비가 되었습니다. 
