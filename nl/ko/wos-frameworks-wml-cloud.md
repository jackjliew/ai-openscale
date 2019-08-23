---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #frmwrks-wml}

{{site.data.keyword.pm_full}}을 사용하여 {{site.data.keyword.aios_full}}에서 페이로드 로깅, 피드백 로깅을 수행하고 성능 정확성, 런타임 편향성 감지, 설명 가능성 및 자동-편향성 함수를 측정할 수 있습니다. 

{{site.data.keyword.aios_full}}에서는 다음 {{site.data.keyword.pm_full}} 프레임워크를 전적으로 지원합니다. 
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| Apache Spark MLlib | 분류 | 정형 |
| Apache Spark MLLib | 회귀 | 정형 |
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | 분류 | 비정형(이미지, 텍스트) |
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | 회귀 | 비정형(이미지, 텍스트) |
| Python 함수 | 분류 | 정형 |
| Python 함수 | 회귀 | 정형 |
| scikit-learn | 분류 | 정형 |
| scikit-learn | 회귀 | 정형 |
| XGBoost | 분류 | 정형 |
| XGBoost | 회귀 | 정형 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

<sup>1</sup>Keras 지원에는 공정성에 대한 지원은 포함되지 않습니다.
{: note}

<sup>2</sup>설명 가능성은 모델 / 프레임워크에서 예측 확률을 출력하는 경우에 지원됩니다.
{: note}

## {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 서비스 인스턴스 지정
{: #wml-connect}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 {{site.data.keyword.pm_full}} 인스턴스를 지정하는 것입니다. {{site.data.keyword.pm_short}} 인스턴스는 사용자의 AI 모델 및 배치를 저장하는 곳입니다.
{: shortdesc}

### 선행 조건
{: #wml-prereq}

{{site.data.keyword.aios_short}} 서비스 인스턴스가 있는 계정과 동일한 {{site.data.keyword.Bluemix_notm}} 계정에 프로비저닝된 {{site.data.keyword.pm_full}} 인스턴스가 있어야 합니다. {{site.data.keyword.pm_full}} 인스턴스를 다른 계정에서 프로비저닝한 경우에는 {{site.data.keyword.aios_short}}에서 자동 페이로드 로깅을 사용하여 해당 인스턴스를 구성할 수 없습니다.

### {{site.data.keyword.pm_short}} 서비스 인스턴스에 연결
{: #wml-config}

{{site.data.keyword.aios_short}}은 {{site.data.keyword.pm_full}} 인스턴스에서 AI 모델 및 배치에 연결됩니다.

1.  **구성** 탭의 탐색 분할창에서 **기계 학습 제공자**를 클릭하십시오. 

    ![지원되는 기계 학습 엔진에 대한 타일과 함께 기계 학습 서비스 제공자 선택 화면이 표시됨](images/wos-machine-learning-providers-selection.png)

2.  **기계 학습 제공자 추가** 단추를 클릭한 후 {{site.data.keyword.pm_full}} 타일을 클릭하십시오. {{site.data.keyword.aios_short}}에서 사용자의 {{site.data.keyword.Bluemix_notm}} 계정을 확인하여 기존 {{site.data.keyword.pm_full}} WML 인스턴스를 찾습니다. 
3. **Watson Machine Learning 서비스** 드롭 다운 메뉴에서 인스턴스를 선택하십시오.

    ![{{site.data.keyword.pm_short}} 서비스 선택](images/gs-set-wml.png)

4.  (선택사항) {{site.data.keyword.Bluemix_notm}} 계정 외부의 기계 학습 위치를 지정하려면 **다른 위치 선택**을 사용할 수 있습니다. 유효한 JSON으로 사용자의 위치에 대한 인증 정보를 제공하십시오.

    ![{{site.data.keyword.pm_short}} 인스턴스 설정](images/gs-get-wml.png)

    **저장**을 클릭하십시오.

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택한 후 **구성**을 클릭하십시오.

## 다음 단계
{: #wml-next}

이제 {{site.data.keyword.aios_short}}이 [모니터를 구성](/docs/services/ai-openscale?topic=ai-openscale-mo-config)할 준비가 되었습니다.
