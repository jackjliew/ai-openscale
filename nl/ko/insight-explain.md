---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 트랜잭션 설명
{: #ie-ov}

각 배치에 대해 특정 트랜잭션에 대한 데이터의 설명 가능성을 볼 수 있습니다.
{: shortdesc}

## 트랜잭션 설명
{: #ie-view}

선택된 배치 타일의 네비게이터에서 **트랜잭션 설명** 탭(![트랜잭션 설명 탭](images/insight-transact-tab.png))을 선택하고 트랜잭션 ID를 입력하십시오.

스코어링을 위해 모델에 데이터를 전송할 때마다 `X-Global-Transaction-Id` 필드를 설정하여 HTTP 헤더에 트랜잭션 ID를 설정해야 합니다. 이 트랜잭션 ID는 페이로드 테이블에 저장됩니다. 특정 스코어링에 대한 모델 동작의 설명을 찾으려면 해당 스코어링 요청과 연관된 트랜잭션 ID를 지정하십시오. 이 동작은 {{site.data.keyword.pm_full}} 트랜잭션에만 적용되며 비WML 트랜잭션에는 적용되지 않습니다.
{: note}

### {{site.data.keyword.aios_short}}에서 트랜잭션 ID 찾기
{: #ie-find}

1.  배치에 대한 시간 차트에서 마커를 차트를 가로질러 밀고 [특정 시간에 대한 데이터 시각화](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)에 대한 **세부사항 보기** 링크를 클릭하십시오.
1.  **트랜잭션 보기** 단추를 클릭하여 [트랜잭션 ID 목록을 보십시오](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  목록에서 트랜잭션 ID 중 하나를 복사하여 **트랜잭션 설명** 페이지의 검색 상자에 이를 붙여넣고 Enter를 누르십시오.

    임의의 트랜잭션 ID에 대한 조치 열에서 **설명** 링크를 클릭하는 방법으로도 트랜잭션 ID 목록을 표시할 수 있습니다. 이 경우, 설명 가능성 탭에서 트랜잭션이 열립니다.
    {: note}

  다른 유형의 모델에 대한 설명 예를 보려면 다음 절을 참조하십시오.

  ![설명 가능성 트랜잭션 ID](images/insight-explain-trans-id.png)

## 카테고리 모델 예
{: #ie-class}

이 설명 가능성 예는 보험 청구를 승인하거나 거부하는 2진 분류 모델에 해당됩니다. 이 케이스에서 `DENIED`라는 최종 결과에 긍정적 또는 부정적으로 기여하는 요인을 볼 수 있습니다.

`< 1 year`라는 값을 가진 *POLICY AGE* 특성이 DENIED 결과를 결정하는 데 최대 영향을 미쳤습니다. 이 결과에 기여한 기타 특성은 *CLAIM FREQUENCY*(`High`) 및 *AGE*(`18`)이며 *CAR VALUE*(`$50,000`)는 미미한 영향만 미쳤습니다.

![설명 가능성 2진 분류](images/insight-explain-binary.png)

차트가 트랜잭션의 결과를 판별함에 있어 최대 유효 요인을 표시하는 데 유용한 반면 분류 모델은 `Minimum changes for Approved outcome` 및 `Minimum changes for this outcome` 섹션에 상세한 고급 설명을 포함할 수 있습니다.

회귀, 이미지 및 비정형 텍스트 모델에 대해서는 고급 설명을 사용할 수 없습니다.
{: note}

`Minimum changes for Approved outcome`은 특성의 값이 이 절에 나열된 값으로 변경되면 모델의 예측이 변경됨을 알려줍니다.

이와 마찬가지로 `Minimum changes for this outcome`은 특성의 값이 이 절에 나열된 값으로 변경되더라도 모델의 예측이 변경되지 않음을 알려줍니다.

따라서 이러한 두 값은 설명이 생성되는 데이터 점의 부근에서 모델의 동작에 대해 알려줍니다.

![설명 가능성 2진 분류](images/insight-explain-binary2.png)

## 이미지 모델
{: #ie-image}

{{site.data.keyword.aios_short}}에서는 이미지 데이터에 대한 설명 가능성을 지원합니다. 

### 이미지 모델에 대한 작업
{: #ie-image-working}

1. 환경을 설정하십시오. 
   2. {{site.data.keyword.aios_short}} 및 {{site.data.keyword.pm_full}} 패키지를 설치하십시오. 
   3. 인증 정보를 구성하십시오. 
   4. 모델 작성 및 분석 수행에 필요한 라이브러리를 설치하십시오. 필요한 라이브러리는 다음과 같습니다. 
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. 이미지 기반 모델을 작성하고 배치하십시오. 
   2. 이미지 분류 방식을 기준으로 이미지용 폴더를 작성하십시오. 
       - 기본 `data` 디렉토리에 `train` 및 `validation` 서브디렉토리가 있어야 합니다. 
       - 각 서브디렉토리 내에 분류 디렉토리가 있어야 합니다. 
  2. 이미지 크기를 표준화한 후 훈련 및 유효성 검증에 사용할 서브디렉토리를 설정하십시오. 
  3. 이미지와 해당 클래스를 다시 스케일링하고 검색하기 위해 데이터를 사전 처리하십시오. 
  4. 모델을 정의하고 훈련시키십시오. 
  5. 모델을 저장하십시오. 
  6. 모델을 배치하십시오. 

7. `APIClient`를 지정하고 자산을 구독한 후 모델을 스코어링하여 {{site.data.keyword.aios_short}}을 구성하십시오. 
8. 설명 가능성을 구성하십시오. 
   9. 설명 가능성을 사용으로 설정하십시오. 
   10. 트랜잭션에 대한 설명을 가져오십시오. 
   11. 설명된 이미지를 표시하십시오.  

### 이미지 모델 트랜잭션 설명
{: #ie-image-workingviewing}

설명 가능성의 이미지 분류 모델 예의 경우, 예측된 결과에 대해 이미지 중 어느 파트가 긍정적 또는 부정적으로 기여하는지 알려줍니다. 다음 예에서, 긍정적 분할창의 이미지는 예측에 긍정적으로 영향을 미치는 파트를 표시하고 부정적 분할창의 이미지는 결과에 긍정적으로 영향을 미치는 파트를 표시합니다.

![설명 가능성 이미지 분류](images/insight-explain-image.png)

{{site.data.keyword.pm_full}}의 경우, 페이로드 로깅을 위해 전송되는 이미지 분류 모델에 대한 스코어링 입력은 1MB를 초과할 수 없습니다. 제한시간 문제를 방지하려면, 이미지가 125 x 125픽셀을 초과하지 않아야 하며 첫 번째 이미지가 완료되면 두 번째 이미지에 대한 설명이 요청되도록 순차적으로 전송해야 합니다.
{: note}


### 이미지 모델 예
{: #ie-image-working-ntbks}

자세한 코드 샘플을 확인하고 사용자 고유의 {{site.data.keyword.aios_short}} 배치를 개발하려면 다음 두 개의 노트북을 사용하십시오. 

- [이미지 기반 모델에 대한 설명 생성 튜토리얼](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [이미지 기반 2진 분류자 모델에 대한 설명 생성 튜토리얼](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}


## 비정형 텍스트 모델
{: #ie-unstruct}

{{site.data.keyword.aios_short}}에서는 비정형 텍스트 데이터에 대한 설명 가능성을 지원합니다. 

### 비정형 텍스트 모델에 대한 작업
{: #ie-unstruct-steps}

1. 환경을 설정하십시오. 
   2. {{site.data.keyword.aios_short}} 및 {{site.data.keyword.pm_full}} 패키지를 설치하십시오. 
   3. 인증 정보를 구성하십시오. 
   4. 모델 작성 및 분석 수행에 필요한 라이브러리를 설치하십시오. 필요한 라이브러리는 다음과 같습니다. 
      - `pandas`
      - `pyspark`({{site.data.keyword.DSX}}를 사용하지 않는 경우)

1. 이미지 기반 모델을 작성하고 배치하십시오. 
   2. 훈련 데이터를 pandas 프레임에 로드하십시오. 
   2. 데이터에 대해 모델을 훈련시키십시오. 
   3. 모델을 공개하십시오. 
   4. 모델을 배치하고 스코어링하십시오. 

7. `APIClient`를 지정하고 자산을 구독한 후 모델을 스코어링하여 {{site.data.keyword.aios_short}}을 구성하십시오. 
8. 설명 가능성을 구성하십시오. 
   9. 설명 가능성을 사용으로 설정하십시오. 
   10. 트랜잭션에 대한 설명을 가져오십시오. 

### 비정형 텍스트 트랜잭션 설명
{: #ie-unstruct-xplan}

다음 설명 가능성 예는 비정형 텍스트를 평가하는 분류 모델을 보여줍니다. 설명은 모델 예측에 대한 부정적인 영향 및 긍정적인 영향을 가진 키워드를 표시합니다. 또한 모델에 입력으로 제공된 원래 텍스트에서 식별된 키워드의 위치를 표시합니다.

![설명 가능성 이미지 분류](images/insight-explain-text.png)

### 비정형 텍스트 모델 예
{: #ie-unstruct-ntbkssample}

자세한 코드 샘플을 확인하고 사용자 고유의 {{site.data.keyword.aios_short}} 배치를 개발하려면 다음 노트북을 사용하십시오. 

- [텍스트 기반 모델에 대한 설명 생성 튜토리얼](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}
