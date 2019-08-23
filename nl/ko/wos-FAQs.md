---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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

# 자주 묻는 질문(FAQ)
{: #wos-faqs}

여기에서는 {{site.data.keyword.aios_full}} 사용자가 가장 자주 묻는 질문 중 일부를 다룹니다.
{: shortdesc}

## 질문
{: #wos-faqs-questions}

- [{{site.data.keyword.aios_short}}이란 무엇입니까?](#faq-whatsa)
- [{{site.data.keyword.aios_short}}의 가격은 얼마입니까?](#faq-pricing)
- [{{site.data.keyword.aios_short}}의 무료 평가판이 있습니까?](#faq-freetrial)
- [내 AI 모델은 모두 Azure에 있습니다. Microsoft Azure ML 엔진을 {{site.data.keyword.aios_short}}과 함께 사용할 수 있습니까?](#faq-azure)
- [내 AI 모델은 모두 Amazon에 있습니다. Amazon SageMaker ML 엔진을 {{site.data.keyword.aios_short}}과 함께 사용할 수 있습니까?](#faq-sagemaker)
- [{{site.data.keyword.aios_short}}을 {{site.data.keyword.icp4dfull_notm}}에서 사용할 수 있습니까? ](#faq-icp)
- [나만의 서버에서 {{site.data.keyword.aios_short}}을 실행하고 싶습니다. 컴퓨터 처리 능력을 얼마나 할당해야 합니까?](#faq-sizing)
- [어떻게 예측 열을 정수 데이터 유형에서 카테고리 데이터 유형으로 변환합니까?](#wos-faqs-convert-data-types)
- [{{site.data.keyword.aios_short}}에서 내 훈련 데이터에 액세스해야 하는 이유는 무엇입니까?](#trainingdata)

### {{site.data.keyword.aios_short}}이란 무엇입니까?
{: #faq-whatsa}

Watson OpenScale은 장소에 관계없이 빌드되어 실행 중인 모델에 대해 라이프사이클 전반에서 AI를 통해 결과를 추적하고 측정하며 변화하는 비즈니스 상화에 맞춰 AI를 변경하고 제어합니다.

이 동영상을 보면 {{site.data.keyword.aios_short}}의 간단한 개요를 알 수 있습니다.

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="AI에서의 신뢰성 및 투명성" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

### {{site.data.keyword.aios_short}}의 가격은 얼마입니까?
{: #faq-pricing}

Lite 플랜에서 전환할 준비가 되면 설명 가능성에 대한 트랜잭션, 피드백 행 또는 페이로드 수에 대한 제한 없이 최대 24개의 배치된 모델에 대한 모니터링을 포함하는 **표준** 가격 플랜이 제공됩니다. [{{site.data.keyword.Bluemix}} 카탈로그](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external}에서 최신 정보를 확인할 수 있습니다.


### {{site.data.keyword.aios_short}}의 무료 평가판이 있습니까?
{: #faq-freetrial}

{{site.data.keyword.aios_short}}은 Lite 플랜을 통해 무료 평가판을 제공합니다. 등록하려면 [{{site.data.keyword.aios_short}} 웹 페이지](https://www.ibm.com/cloud/watson-openscale/){: external}를 방문하여 **지금 시작하기**를 클릭하십시오. 원하는 기간만큼 Lite 플랜을 사용할 수 있습니다(월별 사용량 제한이 적용되며 매달 새로 고쳐짐).

### 내 AI 모델은 모두 Azure에 있습니다. Microsoft Azure ML 엔진을 {{site.data.keyword.aios_short}}과 함께 사용할 수 있습니까?
{: #faq-azure}

{{site.data.keyword.aios_short}}은 Microsoft Azure ML Studio와 Microsoft Azure ML 서비스 엔진을 모두 지원합니다. 자세한 정보는 [Microsoft Azure ML Studio 프레임워크](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure) 및 [Microsoft Azure ML 서비스 프레임워크](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service)를 참조하십시오.

### 내 AI 모델은 모두 Amazon에 있습니다. Amazon SageMaker ML 엔진을 {{site.data.keyword.aios_short}}과 함께 사용할 수 있습니까?
{: #faq-sagemaker}

{{site.data.keyword.aios_short}}은 Amazon SageMaker ML 엔진을 지원합니다. 자세한 정보는 [Amazon SageMaker 프레임워크](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage)를 참조하십시오.

### {{site.data.keyword.aios_short}}을 {{site.data.keyword.icp4dfull_notm}}에서 사용할 수 있습니까?
{: #faq-icp}

{{site.data.keyword.aios_short}}은 {{site.data.keyword.icp4dfull_notm}}용 프리미엄 추가 기능 중 하나입니다. 

### 나만의 서버에서 {{site.data.keyword.aios_short}}을 실행하고 싶습니다. 컴퓨터 처리 능력을 얼마나 할당해야 합니까?
{: #faq-sizing}

3노드 및 6노드 구성을 위한 [하드웨어 구성](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#inst-hwt)에 대한 구체적인 지침이 있습니다. IBM 기술 영업 팀이 구체적인 구성의 크기를 지정하는 데 도움을 줄 수도 있습니다. {{site.data.keyword.aios_short}}은 {{site.data.keyword.icp4dfull_notm}}의 추가 기능으로 실행되므로 두 소프트웨어 제품 모두에 대한 요구사항을 고려해야 합니다.

### 어떻게 예측 열을 정수 데이터 유형에서 카테고리 데이터 유형으로 변환합니까?
{: #wos-faqs-convert-data-types}

모델에 대한 공정성 모니터링을 구성할 때 예측 열은 예측 레이블이 카테고리인 경우에도 정수 숫자 값에만 허용됩니다. 정수가 아니라 카테고리 기능에 대해 이를 구성하는 방법은 무엇입니까? 수동 변환이 필요합니까? 

훈련 데이터에는 "거부된 대출", "승인된 대출" 등의 레이블이 있습니다. {{site.data.keyword.pm_full}} 스코어링 엔드포인트에 의해 리턴되는 예측 값은 "0.0", "1.0" 등의 값을 가집니다. 또한 스코어링 엔드포인트에는 예측의 텍스트 표현을 포함하는 선택적 열이 있습니다. 예를 들어, 예측=1.0이면 predictionLabel 열이 "승인된 대출" 값을 가질 수 있습니다. 해당 열이 사용 가능하면 모델에 대한 긍정적인 결과 및 부정적인 결과를 구성하는 동안 "승인된 대출" 및 "거부된 대출"이라는 문자열 값을 지정할 수 있습니다. 해당 열을 사용할 수 없으면 긍정/부정 클래스에 대해 1.0, 0.0이라는 정수/이중 값을 지정해야 합니다.

{{site.data.keyword.pm_full}}에는 {{site.data.keyword.pm_full}} 스코어링 엔드포인트 출력의 스키마 및 다른 열에 대한 역할을 정의하는 출력 스키마 개념이 있습니다. 역할은 어느 열이 예측값을 포함하는지, 어느 열이 예측 확률 및 클래스 레벨 값을 포함하는지 등을 식별합니다. 출력 스키마는 모델 빌더를 사용하여 작성된 모델에 대해 자동으로 설정됩니다. 또한 {{site.data.keyword.pm_full}} Python 클라이언트를 사용하여 설정될 수 있습니다. 사용자는 출력 스키마를 사용하여 예측에 대한 문자열 표현을 포함하는 열을 정의할 수 있습니다. 이는 열에 대한 modeling_role을 'decoded-target'으로 설정하여 수행합니다. {{site.data.keyword.pm_full}} Python 클라이언트에 대한 문서는 http://wml-api-pyclient-dev.mybluemix.net/#repository에서 사용 가능합니다. 사용할 출력 스키마 및 API를 이해하기 위한 "OUTPUT_DATA_SCHEMA" 검색은 OUTPUT_DATA_SCHEMA를 매개변수로 허용하는 store_model API입니다.

### {{site.data.keyword.aios_short}}에서 내 훈련 데이터에 액세스해야 하는 이유는 무엇입니까?
{: #trainingdata}

Db2 또는 {{site.data.keyword.cos_full_notm}}에 저장되어 있는 훈련 데이터에 대한 {{site.data.keyword.aios_short}} 액세스 권한을 제공하거나 훈련 데이터에 액세스할 수 있는 노트북을 실행해야 합니다. {{site.data.keyword.aios_short}}은 다음과 같은 이유로 훈련 데이터에 대한 액세스가 필요합니다.

- 대조 설명을 생성하기 위해: 설명을 작성하려면 훈련 데이터의 구분 값, 표준 편차 및 중앙값과 같은 통계에 액세스해야 합니다.
- 훈련 데이터 통계를 표시하기 위해: 편향성 세부사항 페이지를 채우려면 {{site.data.keyword.aios_short}}에 통계를 생성할 훈련 데이터가 있어야 합니다.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

노트북 기반 접근 방식에서 사용자는 {{site.data.keyword.aios_short}}에서 배치를 구성할 때 통계 및 기타 정보를 업로드하게 됩니다. 이는 {{site.data.keyword.aios_short}}에 더 이상 노트북 외부 즉 사용자 환경에서 실행되는 훈련 데이터에 대한 액세스 권한이 없음을 의미합니다. 구성 중에 업로드된 정보에 대한 액세스 권한만 보유합니다.


