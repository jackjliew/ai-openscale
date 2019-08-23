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

# 비정형 텍스트 모델 설명
{: #ie-unstruct}

{{site.data.keyword.aios_short}}에서는 비정형 텍스트 데이터에 대한 설명 가능성을 지원합니다.
{: shortdesc}

## 비정형 텍스트 모델에 대한 작업
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

## 비정형 텍스트 트랜잭션 설명
{: #ie-unstruct-xplan}

다음 설명 가능성 예는 비정형 텍스트를 평가하는 분류 모델을 보여줍니다. 설명은 모델 예측에 대한 부정적인 영향 및 긍정적인 영향을 가진 키워드를 표시합니다. 또한 모델에 입력으로 제공된 원래 텍스트에서 식별된 키워드의 위치를 표시합니다.

![설명 가능성 이미지 분류 차트가 표시됩니다. 이는 비정형 텍스트의 신뢰수준을 표시합니다.](images/insight-explain-text.png)

## 비정형 텍스트 모델 예
{: #ie-unstruct-ntbkssample}

자세한 코드 샘플을 확인하고 사용자 고유의 {{site.data.keyword.aios_short}} 배치를 개발하려면 다음 노트북을 사용하십시오.

- [텍스트 기반 모델에 대한 설명 생성 튜토리얼](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

