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

# 카테고리 모델 설명
{: #ie-class}

이 설명 가능성 예는 보험 청구를 승인하거나 거부하는 2진 분류 모델에 해당됩니다. 이 케이스에서 `DENIED`라는 최종 결과에 긍정적 또는 부정적으로 기여하는 요인을 볼 수 있습니다.
{: shortdesc}

`<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear`라는 값을 가진 *POLICY AGE* 특성이 DENIED 결과를 결정하는 데 최대 영향을 미쳤습니다. 이 결과에 기여한 기타 특성은 *CLAIM FREQUENCY*(`High`) 및 *AGE*(`18`)이며 *CAR VALUE*(`$50,000`)는 미미한 영향만 미쳤습니다.

![설명 가능성 2진 분류가 거부 및 승인된 청구에 대한 세부사항과 함께 표시됨](images/insight-explain-binary.png)

차트가 트랜잭션의 결과를 판별함에 있어 최대 유효 요인을 표시하는 데 유용한 반면 분류 모델은 `Minimum changes for Approved outcome` 및 `Minimum changes for this outcome` 섹션에 상세한 고급 설명을 포함할 수 있습니다.

회귀, 이미지 및 비정형 텍스트 모델에 대해서는 고급 설명을 사용할 수 없습니다.
{: note}

`Minimum changes for Approved outcome`은 특성의 값이 이 절에 나열된 값으로 변경되면 모델의 예측이 변경됨을 알려줍니다.

이와 마찬가지로 `Minimum changes for this outcome`은 특성의 값이 이 절에 나열된 값으로 변경되더라도 모델의 예측이 변경되지 않음을 알려줍니다.

따라서 이러한 두 값은 설명이 생성되는 데이터 점의 부근에서 모델의 동작에 대해 알려줍니다.

![결과 변경에 필요한 최소 변경사항과 함께 설명 가능성 2진 분류 세부사항](images/insight-explain-binary2.png)
