---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# 공정성 모니터 구성
{: #mf-monitor}

{{site.data.keyword.aios_full}}에서 공정성 모니터는 서로 다른 모집단 전체에 걸쳐 공정한 결과가 보장되도록 배치의 편향성을 스캔합니다.
{: shortdesc}

## 단계
{: #mf-config}

**공정성** 탭의 **공정성의 개념** 페이지에서 **시작**을 클릭하여 구성 프로세스를 시작하십시오.

![공정성의 개념 페이지](images/fair-what-is.png)

이 프로세스의 전반에서 {{site.data.keyword.aios_full}}에서는 모델을 분석한 후 가장 논리적인 결과를 토대로 권장사항을 작성합니다. **공정성** 탭의 이후 페이지에서는 다음 태스크를 수행해야 합니다.

1. 모니터할 기능을 선택하십시오. 카테고리, 숫자(정수), 부동 또는 이중 공정성 데이터 유형의 특성만 지원됩니다. 기타 데이터 유형의 특성은 지원되지 않습니다.

1. 참조 그룹 및 모니터 대상 그룹을 지정하십시오.

   각 특성을 구성하기 위한 특정 요구사항이 있습니다. 예를 들어 `age`를 모니터 대상 기능 중 하나로 선택한 경우, **참조 그룹** 및 **모니터 대상 그룹**에 직접 값을 입력하여 각 그룹의 연령 범위를 정의해야 합니다.

1.  기능에 대한 공정성 경보 임계값을 설정하십시오.

    공정성 임계값은 참조 그룹에 대한 선호 결과의 백분율과 비교하여 모니터되는 그룹에 대한 선호 결과의 백분율의 허용 가능한 차이를 지정하는 데 사용됩니다.

    대출을 받을 수 있는 사람(`favorable outcome=loan granted`) 및 받을 수 없는 사람(`unfavorable outcome=loan denied`)을 예측하는 모델을 고려해 보십시오. 또한 연령에 대해 모니터되는 값은 `[18,25]`이며 참조 값은 `[26,100]`입니다. 편향성 발견 알고리즘이 실행될 때, 최근 `N`개의 레코드 더하기 섭동된 데이터에서 연령 그룹 `[18,25]` 내의 사람에 대한 선호 결과의 백분율이 `50%` 인 반면, 연령 그룹 `[26,100]` 내의 사람에 대한 선호 결과의 백분율이 `70%`이면 공정성이 50*100/70 = 71.42인 것으로 계산됩니다.

    공정성 임계값이 80%로 설정된 경우, 계산된 공정성이 임계값을 초과하므로 알고리즘이 모델을 편향된 것으로 플래그 지정합니다. 단, 임계값이 70%로 설정되면 모델을 편향된 것으로 보고하지 않습니다.

     해당 화면에 입력하는 값은 모델 스코어링 엔드포인트에 전송한 값이어야 합니다. 결과적으로 페이로드 테이블에 추가됩니다. 데이터를 스코어링 엔드포인트로 전송하기 전에 조작한 경우, 조작된 값을 입력하십시오. 예를 들어, 원래 데이터의 값이 *Gender*에 대해서는 `Male` 및 `Female`이며 스코어링 엔드포인트로 전송된 데이터가 `M` 및 `F`로 조작된 경우, 이 화면에서는 `M` 및 `F`입니다.

1.  모델에 대한 선호 결과를 나타내는 값을 지정하십시오. 모델 출력 스키마에 맵핑 열이 있는 경우 [훈련 데이터](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)의 `label` 열에서 값이 파생됩니다. {{site.data.keyword.pm_full}}에서는 `prediction` 열에 항상 이중 값이 있습니다. 맵핑 열은 이 `prediction` 값을 클래스 레이블에 맵핑하는 데 사용됩니다.

    예를 들어, `prediction` 값이 `1.0`이면 맵핑 열이 `Loan denied` 값을 가질 수 있습니다. 이는 모델의 예측이 `Loan denied`임을 의미합니다. 따라서 모델 출력 스키마가 맵핑 열을 포함하면 맵핑 열에 있는 해당 사항을 사용하여 선호 및 비선호 값을 지정합니다.

    단, 모델 출력 스키마에 맵핑 열이 없으면 선호 및 비선호 값이 `prediction` 열의 값(`0.0`, `1.0` 등)을 사용하여 지정되어야 합니다.

1.  마지막으로 평가 데이터 세트에서 최소 수의 레코드가 사용 가능할 때까지 공정성 측정을 금지하도록 최소 샘플 크기를 설정하십시오. 이로 인해 샘플 크기가 너무 작아서 결과를 왜곡시키는 것을 방지할 수 있습니다. 편향성 검사가 실행될 때마다 최소 샘플 크기를 사용하여 편향성 계산을 수행할 레코드 수를 결정합니다.

    검토를 위해 선택사항 요약이 표시됩니다. 변경해야 할 사항이 있는 경우 해당 섹션의 **편집** 링크를 클릭하십시오. 그렇지 않은 경우 **저장**을 클릭하십시오.

    **다른 특성 추가**를 클릭하여 특성 선택 화면으로 돌아가서 `City`, `Zip Code` 또는 `Account Balance` 등의 추가 기능을 공정성 모니터에 추가할 수도 있습니다.

### 편향성 제거 작업 이해
{: #mf-debias}

편향성 제거 엔드포인트를 확인하려면 **편향성 제거 엔드포인트** 단추를 클릭하십시오. 그러면 cURL, Java 또는 Python 등 다양한 형식의 엔드포인트를 보고 복사할 수 있습니다. 

편향성이 제거된 스코어링 엔드포인트는 배치된 모델의 일반 스코어링 엔드포인트와 완전히 동일하게 사용될 수 있습니다. 배치된 모델의 응답을 리턴하는 것 외에도 `debiased_prediction` 및 `debiased_probability` 열을 리턴합니다.

- `debiased_prediction` 열은 편향성 제거된 예측 값을 포함합니다. {{site.data.keyword.pm_full}}의 경우 이는 예측의 인코딩된 표현입니다. 예를 들어, 모델 예측이 "Loan Granted" 또는 "Loan Denied"인 경우, {{site.data.keyword.pm_full}}에서 이러한 두 값을 각각 "0.0" 및 "1.0"으로 인코딩할 수 있습니다. `debiased_prediction` 열은 편향성 제거된 예측의 인코딩된 표현 등을 포함합니다.

- 반면에 `debiased_probability` 열은 편향성 제거된 예측의 확률을 표시합니다. 각 값이 예측 클래스 중 하나에 속하는 편향성 제거된 예측의 확률을 나타내는 이중 값의 배열입니다.

`decoded-target`으로 `modeling-role`이 있는 열을 포함하는 출력 스키마 내에 열이 있는 경우, 다른 열인 `debiased_decoded_target`도 리턴됩니다.

- `debiased_decoded_target` 열은 편향성 제거된 예측의 문자열 표현을 포함합니다. 예측 값이 "0.0" 또는 "1.0"인 이전 예에서는 `debiased_decoded_target`이 "Loan Granted" 또는 "Loan Denied"를 포함할 것입니다.

모델 수행 엔진({{site.data.keyword.pm_full}}, Amazon Sagemaker, Microsoft Azure ML Studio 등)에 배치된 스코어링 엔드포인트를 직접 호출하는 대신 프로덕션 애플리케이션에서 이 엔드포인트를 호출하는 것이 이상적입니다. 이 방법을 사용하면 {{site.data.keyword.aios_short}}이 `debiased` 값도 모델 배치의 페이로드 로깅 테이블에 저장합니다. 그런 다음 이 엔드포인트를 통해 수행된 모든 스코어링이 자동으로 편향성 제거됩니다.

이 엔드포인트가 런타임 편향성을 처리하므로 페이로드 로깅 테이블에서 최신 스코어링 데이터에 대해 계속 백그라운드 검사를 실행하며 전송된 스코어링 요청을 편향성 제거하는 데 사용되는 편향성 완화 모델을 계속 업데이트합니다. 이런 방법으로 {{site.data.keyword.aios_short}}이 항상 최신 수신 데이터 및 편향성을 감지하고 완화하기 위한 동작을 사용하여 최신 상태로 유지됩니다.

최종적으로 {{site.data.keyword.aios_short}}이 임계값을 사용하여 데이터가 허용 가능하며 편향되지 않았다고 간주되는지 결정합니다. 임계값은 구성된 모든 공정성 속성에 대해 공정성 모니터에서 설정된 임계값의 최신 값으로 사용됩니다.

## 다음 단계
{: #mf-next}

**모니터 구성** 페이지에서 다른 모니터링 카테고리를 선택할 수 있습니다.
