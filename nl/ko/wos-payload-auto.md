---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# 페이로드 로깅 자동화
{: #fmrk-workaround-pyld-lg}

자동 페이로드 로깅은 {{site.data.keyword.aios_full}} 및 {{site.data.keyword.pm_full}}이 동일한 {{site.data.keyword.Bluemix_notm}} 계정에서 프로비저닝된 경우 이 둘 간에 존재합니다. 다음 경우와 옵션 중 하나를 사용하여 동일한 계정에 있지 않은 {{site.data.keyword.pm_full}} 인스턴스 또는 다른 기계 학습 제공자에 대해 페이로드 로깅을 자동화할 수도 있습니다.
{: shortdesc}

### 경우 1: 스코어링 입력 및 출력의 원본 형식({{site.data.keyword.aios_short}}에서 필요한 형식과 다름)을 유지합니다.
{: #fmrk-workaround-case1}

애플리케이션에서 변경할 수 없는 원래 페이로드 형식을 사용하는 경우 다음 옵션 중 하나를 선택하십시오.

- 옵션 1: 사용자 정의 기계 학습 엔진 스코어링 엔드포인트에서 두 페이로드 형식을 모두 승인해야 합니다. 

   페이로드 형식에 따라 다름: {{site.data.keyword.aios_short}}({{site.data.keyword.pm_full}} 유형) 또는 사용자의 엔드포인트에서 해당 형식으로 출력을 리턴합니다. 형식이 사용자의 형식인 경우 {{site.data.keyword.aios_short}} 형식으로 변환하고 페이로드 로깅 표에 페이로드 레코드로 저장하십시오. 스코어링 입력 형식이 {{site.data.keyword.aios_short}} 형식이면 페이로드를 저장하지 마십시오(이 페이로드는 사용자가 아니라 {{site.data.keyword.aios_short}}에서 가져옴).

   자세한 정보는 [두 페이로드 형식 사용](#fmrk-workaround-notsuppt)을 참조하십시오.

- 옵션 2: 특정 이유 때문에 단일 REST API 엔드포인트에서 해당 로직을 임베드하는 경우 두 엔드포인트를 정의할 수 있습니다. 

   그러나 애플리케이션에서 한 엔드포인트를 사용하는 경우 페이로드 로깅을 추가하고 예상 형식으로 변환해야 합니다. 두 번째 엔드포인트는 편향과 설명 가능성 등의 필수 계산을 수행하기 위해 {{site.data.keyword.aios_short}}에서 사용합니다. 이 엔드포인트에는 페이로드 로깅이 필요하지 않습니다. {{site.data.keyword.aios_short}} 구성 중에 두 번째 엔드포인트가 호환 가능 형식의 엔드포인트를 가리켜야 합니다.

   자세한 정보는 [두 엔드포인트 사용](#fmrk-workaround-opt2-cs1)을 참조하십시오.

- 옵션 3: 페이로드 로깅 모듈을 원래 엔드포인트 또는 다운스트림 애플리케이션으로 이동하십시오. 

   애플리케이션에서 이 옵션을 지원하는 경우 사용자 정의 기계 학습 엔진의 한 엔드포인트만 개발하면 됩니다. 즉, {{site.data.keyword.aios_short}}의 엔드포인트입니다.

### 경우 2: {{site.data.keyword.aios_short}}에 필요한 페이로드 형식에 대해 작업
{: #fmrk-workaround-case2}

이 경우 사용자의 형식(스코어링 입력/출력)에서 {{site.data.keyword.aios_short}}에 필요한 형식으로 변환할 필요가 없습니다.

내부 스코어링 요청을 사용자 페이로드로 로깅하지 않기 때문에({{site.data.keyword.aios_short}}에서 계산) 두 엔드포인트를 개발하거나 단일 엔드포인트의 추가 로직을 코딩해야 합니다.

- 옵션 1: 두 개의 엔드포인트. 경우 1의 옵션 2와 거의 같습니다. 유일한 차이점은 이미 맞춰져 있으므로 형식을 변환할 필요가 없다는 것입니다.

- 옵션 2: 단일 엔드포인트. 스코어링 요청이 사용자의 애플리케이션에서 오는지 감지하지 않아도 됩니다. 이 작업은 스코어링 페이로드의 추가 정보(메타데이터라고도 함)를 보내 수행할 수 있습니다. 이 메타데이터가 감지되면 페이로드를 로깅해야 합니다.

## 두 페이로드 형식 사용
{: #fmrk-workaround-notsuppt}

XYZ 오퍼링을 사용하여 내 모델에 서비스를 제공한다고 가정해 보겠습니다. XYZ는 이 단계의 {{site.data.keyword.aios_short}}에서 지원하지 않습니다.

여러 다운스트림 애플리케이션에서 XYZ의 배치를 사용하고 있으며 스코어링 페이로드의 형식을 변경할 수 없습니다. 그러나 스코어링 엔드포인트 로직을 수정할 수 있습니다.

### 단계

1. XYZ 배치를 랩핑하는 사용자 정의 기계 학습 엔진을 개발하십시오.
2. XYZ와 {{site.data.keyword.aios_short}} 둘 다의 페이로드 형식을 지원하도록 사용자 정의 기계 학습 엔진에서 스코어링 엔드포인트를 구현하십시오.
3. 페이로드 형식을 발견하도록 사용자 정의 기계 학습 엔진의 스코어링 엔드포인트에 로직을 추가하십시오.
4. 다운스트림 앱에서 페이로드가 오는 경우 {{site.data.keyword.aios_short}} 형식으로 변환하고 {{site.data.keyword.aios_short}}의 페이로드 레코드로 로깅하십시오.
5. 다운스트림 앱 스코어링 엔드포인트를 사용자가 작성한 새 엔드포인트로 전환하십시오.

스코어링 엔드포인트의 URL은 동일하게 유지해야 하므로 프록시라고도 하는 URL 경로 재지정을 사용하십시오.

## 두 엔드포인트 사용
{: #fmrk-workaround-opt2-cs1}

예를 들어 다운스트림 애플리케이션이 중단되므로 페이로드 형식을 변경할 수 없는 경우 별도의 엔드포인트를 사용해야 합니다. 이 접근 방식은 다음 구성요소로 구성됩니다.

- 입력/출력에 사용자 정의 형식을 사용하는 원래 스코어링 엔드포인트가 포함된 스코어링 엔드포인트(사용자 형식)
- 섭동 엔드포인트({{site.data.keyword.aios_short}} 형식) 및 검색 엔드포인트가 있는 사용자 정의 ml 엔진. 섭동 엔드포인트는 원래 스코어링 엔드포인트를 랩핑하고 {{site.data.keyword.aios_short}} 형식에서 사용자의 형식으로 변환하며 사용자의 출력을 {{site.data.keyword.aios_short}} 형식으로 변환합니다. {{site.data.keyword.aios_short}}에서 스코어링 요청을 정정하고 출력을 이해하는 데 필요합니다.
- 페리오르 로깅 기능이 있는 스코어링 엔드포인트 랩퍼. 이 랩퍼는 원래 스코어링 엔드포인트가 아니라 다운스트림 애플리케이션에서 사용합니다. 해당 로직은 페이로드 로깅 기능을 사용하여 확장되었습니다. 스코어링 요청을 실행할 때마다 입력과 출력이 {{site.data.keyword.aios_short}} 형식으로 변환되고 로깅됩니다.

다음 플로우차트에서는 사용자 정의 기계 학습 엔진에서 섭동 엔드포인트와 검색 엔드포인트를 처리하고 사용자의 형식으로 변환하는 사용자 정의 기계 학습 엔진 솔루션을 보여줍니다.

![REST API 엔드포인트 스펙](images/woscustommlworkflow.png)

### 단계
{: #fmrk-workaround-smple-cd}

1. 노트북을 사용하여 Microsoft Azure Machine Learning Service에 신용 위험 모델(scikit-learn) 배치용 스코어링 엔드포인트를 작성하십시오. 자세한 정보는 [이 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb)을 참조하십시오.
2. 사용자 정의 기계 학습 엔진을 작성하여 Microsoft Azure Cloud에 Flask 애플리케이션으로 배치하십시오. 섭동 및 검색 엔드포인트를 작성하십시오.자세한 정보는 [이 배치 지침](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure)을 참조하십시오.
3. 사용자 정의 기계 학습 엔진과 작동하도록 {{site.data.keyword.aios_short}}를 구성하십시오.자세한 정보는 [이 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb)을 참조하십시오.
4. Microsoft Azure Machine Learning Service에서 페이로드 로깅을 자동화하는 스코어링 엔드포인트 랩퍼를 작성하십시오. 자세한 정보는 [이 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb)을 참조하십시오.

다음 항목에 특히 주의하십시오.

- 인증 정보: 튜토리얼에 따라 작업하기 더 쉽도록 {{site.data.keyword.aios_short}} 인증 정보는 코드로 하드 코딩되어 있습니다(스코어링 엔드포인트 랩퍼). 실제 인증 정보로 이 값을 업데이트해야 합니다.
- Python SDK 대 REST API: 튜토리얼에서는 Python SDK를 사용하여 페이로드를 로깅합니다. REST API를 사용하여 이 작업을 수행할 수 있지만 토큰을 직접 생성하거나 새로 고쳐야 합니다. 
- {{site.data.keyword.cloud_notm}} 대 Cloud Pak for Data: {{site.data.keyword.wos4d_notm}}을 사용하는 경우 인증 정보의 형식이 다릅니다. [샘플 노트북은 여기에서 확인](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb). {{site.data.keyword.aios_short}} 클라이언트 클래스도 다릅니다. `APIClient4ICP` 클라이언트 클래스를 사용합니다.
- 개별 엔드포인트/패키지로 페이로드 로깅 - 페이로드 로깅 및 변환 메소드를 개별 패키지 또는 엔드포인트로 추출. 그러면 스코어링 엔드포인트 외부에서 페이로드 배치를 삽입하려는 경우 재사용할 수 있습니다.

