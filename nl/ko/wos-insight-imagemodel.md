---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 이미지 모델 설명
{: #ie-image}

{{site.data.keyword.aios_short}}에서는 이미지 데이터에 대한 설명 가능성을 지원합니다.
{: shortdesc}

## 이미지 모델에 대한 작업
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

## 이미지 모델 트랜잭션 설명
{: #ie-image-workingviewing}

설명 가능성의 이미지 분류 모델 예의 경우, 예측된 결과에 대해 이미지 중 어느 파트가 긍정적 또는 부정적으로 기여하는지 알려줍니다. 다음 예에서, 긍정적 분할창의 이미지는 예측에 긍정적으로 영향을 미치는 파트를 표시하고 부정적 분할창의 이미지는 결과에 긍정적으로 영향을 미치는 파트를 표시합니다.

![설명 가능성 이미지 분류 신뢰 세부사항이 개의 이미지와 함께 표시됩니다. 여기에는 해당 이미지가 개임을 판별하는 데 도움이 된 이미지의 부분이 무엇인지를 표시하기 위해 강조표시된 그림의 일부도 포함됩니다.](images/insight-explain-image.png)

{{site.data.keyword.pm_full}}의 경우 페이로드 로깅을 위해 전송된 이미지 분류 모델의 스코어링 입력은 ai-open-scale-ibm-aios-scheduling  | 1 | 스케줄링 서비스 MB를 초과할 수 없습니다. 제한시간 문제를 방지하려면, 이미지가 125 x 125픽셀을 초과하지 않아야 하며 첫 번째 이미지가 완료되면 두 번째 이미지에 대한 설명이 요청되도록 순차적으로 전송해야 합니다.
{: note}


## 이미지 모델 예
{: #ie-image-working-ntbks}

자세한 코드 샘플을 확인하고 사용자 고유의 {{site.data.keyword.aios_short}} 배치를 개발하려면 다음 두 개의 노트북을 사용하십시오.

- [이미지 기반 모델에 대한 설명 생성 튜토리얼](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [이미지 기반 2진 분류자 모델에 대한 설명 생성 튜토리얼](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

