---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: drift, behavior, metrics

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

# 드리프트 규모 ![베타 태그](images/beta.png)
{: #behavior-drift-ovr}

시간이 지나면서 모델의 특정 기능에 대한 중요성과 영향이 달라지고 있습니다. 이는 연관된 애플리케이션과 이로 인해 발생하는 비즈니스 결과에 영향을 미칩니다. 드리프트 발견을 통해 {{site.data.keyword.aios_short}}은 모델 메트릭, 모델 성능을 추적하는 방식과 시간 경과에 따라 기능 가중치가 변경되는 방식을 제공합니다. 데이터가 변경되므로 모델의 정확한 예측 기능이 떨어질 수 있습니다. 드리프트 규모는 시간이 지나면서 예측 성능이 떨어지는 범위입니다. 드리프트에 대한 정보를 사용하여 정정 조치를 취하십시오.
{: shortdesc}

## 드리프트 발견 이해
{: #behavior-drift-understand}

드리프트란 숨겨진 컨텍스트 때문에 시간이 경과하면서 예상 성능이 저하되는 것을 말합니다. 시간이 지나면 데이터가 변경되므로 모델의 정확한 예측을 작성하는 기능이 악화될 수 있습니다. {{site.data.keyword.aios_short}}에서는 사용자가 정정 조치를 취할 수 있도록 드리프트를 발견하고 강조표시합니다.

### 작동 방식
{: #behavior-drift-works}

{{site.data.keyword.aios_short}}에서는 모든 트랜잭션을 분석하여 드리프트의 원인이 되는 트랜잭션을 찾아냅니다. 그런 다음 드리프트의 중요한 원인이 되는 속성 값을 기준으로 레코드를 그룹화합니다.

### 계산법
{: #behavior-drift-math}

세 시간마다 {{site.data.keyword.aios_short}}은 예측 모델에 의해 이미 분석된 동일한 훈련 데이터를 분석하여 드리프트를 계산합니다. 그런 다음 결과를 모델의 예측과 비교합니다. 변경 또는 불일치가 있는 경우 {{site.data.keyword.aios_short}}은 드리프트의 범위를 계산한 후 설정된 임계값을 기반으로 발생에 대한 경보를 표시합니다. 


### 드리프트 시각화
{: #behavior-drift-display}

드리프트 시각화에는 그래픽 통계 데이터와 숫자 통계 데이터가 모두 포함됩니다.

![설정된 임계값 미만 드리프트를 보여주는 공정성 지표 차트](images/drift-example.png)

차트를 클릭하여 드리프트에 기여하는 특정 트랜잭션을 표시할 수 있습니다. 발견된 드리프트의 가장 많은 이유가 표시되고 여기에는 예상치 않은 값의 목록 및 관찰에 대한 자연어 설명이 포함됩니다.

![설정된 임계값 미만 드리프트를 보여주는 공정성 지표 차트](images/drift-detection-example.png)

드리프트 트랜잭션은 트랜잭션 세부사항 화면에서 확인할 수 있으며 이 화면에서 **설명**을 클릭하여 특정 트랜잭션이 드리프트 카테고리가 되는 방식을 이해할 수 있습니다.

![설정된 임계값 미만 드리프트를 보여주는 공정성 지표 차트](images/drift-detection-transactions.png)


## 다음 단계

- 드리프트 감지를 설정하는 방법에 대한 정보는 [드리프트 감지 모니터 구성](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)을 참조하십시오. 
- 드리프트를 줄이려면 Watson OpenScale에서 이를 감지한 이후에 사용자가 문제점을 해결하는 새 모델 버전을 빌드해야 합니다. 바람직한 시작점은 드리프트의 원인으로 강조표시된 데이터 점입니다. 드리프트 트랜잭션을 수동으로 레이블링한 후에 예측 모들에 새 데이터를 도입하고 이를 사용하여 모델을 재훈련하십시오. 


