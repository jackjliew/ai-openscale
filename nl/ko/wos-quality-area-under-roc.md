---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# ROC 아래 영역
{: #quality_roc}

ROC(Receiver Operating Characteristic) 아래 영역 곡선은 재현율 및 거짓 양성 비율 곡선 아래에 영역을 제공하며 폴아웃 비율에 대한 민감성을 계산합니다.
{: shortdesc}

## ROC 아래 영역 개요
{: #quality_roc-glance}

- **설명**: 재현율 및 거짓 양성 비율 곡선 아래의 영역입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 2진 분류
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 오차 행렬

## 표시 내용 해석
{: #quality_roc-display}

![ROC 아래 영역 차트가 표시되어 있습니다.](images/quality-area-under-roc.png)

## 계산법
{: #quality_roc-math}

ROC 아래 영역은 임계값 `T`에 대한 `참 양성 비율` 대 `거짓 양성 비율`로 매개변수화되어 표시됩니다.



