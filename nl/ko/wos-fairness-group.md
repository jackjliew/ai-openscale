---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# 그룹에 대한 공정성
{: #quality_group}

그룹에 대한 공정성 메트릭은 다른 그룹에 비해 한 그룹이 더 선호하는 결과를 제공하는 모델의 경향을 나타냅니다. 그룹은 연령, 성별 또는 인종 등의 그룹일 수 있습니다.
{: shortdesc}


## 그룹에 대한 공정성 개요
{: #quality_group-glance}

- **설명**: 모델이 다른 그룹보다 한 그룹의 선호 결과를 더 많이 제공하는 경향입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**: 배치된 모델에서 편향성 제거된 응답을 수신하기 위해 비즈니스 애플리케이션에서 사용할 수 있는 편향성 제거된 스코어링 엔드포인트입니다.
- **문제점 유형**: 모두
- **데이터 유형**: 정형
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 예

## 보호된 속성
{: #quality_group-atts}

{{site.data.keyword.aios_short}}에서는 알려진 보호된 속성이 모델에 존재하는지 여부를 자동으로 식별합니다. {{site.data.keyword.aios_short}}에서 이러한 속성을 발견할 경우, 프로덕션 시 잠재적으로 중요한 속성에 대한 편향을 추적할 수 있도록 존재하는 각 속성에 대해 편향 모니터를 구성할 것을 자동으로 권장합니다. 

### 성별
{: #quality_group-sex}

{{site.data.keyword.aios_short}}에서는 **성별** 속성 내에서 `Woman` 및 `Non-Binary`는 모니터되는 값이 되고 `Male`은 참조 값이 되도록 편향 모니터를 구성할 것을 권장합니다. 

### 인종
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}}에서는 **인종** 속성 내에서 `White-caucasian`은 참조 값이 되고 다른 인종은 모니터되는 값이 되도록 편향 모니터를 구성할 것을 권장합니다.

### 결혼 여부
{: #quality_group-marital}

{{site.data.keyword.aios_short}}에서는 **결혼 여부** 속성 내에서 `married`는 참조 값이 되고 `single`은 모니터되는 값이 되도록 편향 모니터를 구성할 것을 권장합니다.

### 연령
{: #quality_group-age}

{{site.data.keyword.aios_short}}에서는 **연령** 속성 내에서 연령 범위에 따라 실행 가능한 편향성 제거가 생성되도록 편향 모니터를 구성할 것을 권장합니다.

### 우편번호
{: #quality_group-zip}

{{site.data.keyword.aios_short}}에서는 **우편번호** 속성 내에서 개별 우편번호를 스코어링하도록 편향 모니터를 구성할 것을 권장합니다.
