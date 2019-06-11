---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: machine learning, services, ml, custom 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 사용자 정의 ML 서비스 인스턴스 지정
{: #co-connect}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 서비스 인스턴스를 지정하는 것입니다. 서비스 인스턴스는 사용자의 AI 모델 및 배치를 저장하는 곳입니다.
{: shortdesc}

## 사용자 정의 서비스 인스턴스 연결
{: #co-config}

{{site.data.keyword.aios_short}}은 서비스 인스턴스에서 AI 모델 및 배치에 연결됩니다.

1.  {{site.data.keyword.aios_short}} 도구의 홈 페이지에서 **시작**을 클릭하십시오.

    ![홈 페이지](images/gs-config-start.png)

2.  **사용자 정의** 타일을 선택하고 **다음**을 클릭하십시오.

    ![사용자 정의 선택](images/connect-custom.png)

3.  옵션 중 하나를 선택하여 배치에 연결하십시오.

    ![사용자 정의 선택](images/connect-custom-deploy.png)

4.  "개별 스코어링 엔드포인트 입력" 타일을 선택한 경우 인증 정보를 입력하십시오.

    ![서비스 인증 정보 입력](images/connect-custom-cred.png)

5.  **다음**을 클릭하십시오.

    - "개별 스코어링 엔드포인트 입력" 타일을 선택한 경우 배치 이름 및 엔드포인트를 제공해야 합니다.

      ![서비스 인증 정보 입력](images/connect-custom-endpoint.png)

      **다음**을 클릭하십시오.

    - "배치 목록 요청" 타일을 선택한 경우 호스트 이름 또는 IP 주소 및 포트 번호를 제공해야 합니다.

      ![서비스 인증 정보 입력](images/connect-custom-apiendpoint.png)

      **다음**을 클릭하십시오.

      그런 다음 배치의 목록을 선택하십시오.

      ![서비스 인증 정보 입력](images/connect-custom-apiendpoint2.png)

6.  선택된 배치를 검토하십시오.

    ![서비스 인증 정보 입력](images/connect-custom-deploy2.png)

7.  **다음**을 클릭하십시오.

### 작동 방식
{: #co-works}

이 이미지는 사용자 정의 환경 지원을 표시합니다.

![사용자 정의 작동 방식](images/custom-how-works.png)

또한 다음 링크를 참조할 수 있습니다.

[AIOS 페이로드 로깅 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[사용자 정의 배치 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[Python 클라이언트 바인딩 SDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[사용자 정의 기계 학습 엔진에 대한 작업 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[IBM Watson OpenScale에 대한 Python SDK![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

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

  위의 스코어링 출력은 {{site.data.keyword.aios_short}}이 REST를 통해 호출할 수 있는 라이브 스코어링 엔드포인트에서 액세스 가능해야 합니다. AzureML, SageMaker 및 WML의 경우, {{site.data.keyword.aios_short}}이 직접 원시 스코어링 엔드포인트에 연결합니다. 따라서 스코어링 스펙 구현에 대해 걱정할 필요가 없습니다.

### 다음 단계
{: #co-next}

{{site.data.keyword.aios_short}}이 [데이터베이스를 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db)할 준비가 되었습니다.
