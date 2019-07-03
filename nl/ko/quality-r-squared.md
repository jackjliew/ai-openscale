---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R 제곱 ![베타 태그](images/beta.png)
{: #quality_r_squared}

R 제곱은 목표 분산과 목표 분산에 대한 예측 오차의 분산 간 차의 비율로, 모델 작성에 사용된 데이터가 회귀에 얼마나 적합한지 알 수 있습니다.
{: shortdesc}

## R 제곱 개요
{: #quality_r_squared-glance}

- **설명**: 대상 분산과 대상 분산에 대한 예측 오차의 분산 간 차이의 비율입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 회귀
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 없음

## 표시 내용 해석
{: #quality_r_squared-display}

![R 제곱 차트가 표시되어 있습니다.](images/xxxx.png)

## 계산법
{: #quality_r_squared-math}

R 제곱 메트릭은 다음 공식으로 정의됩니다. 

```
               설명 분산
R 제곱 = 1 -  _____________________

                총 분산
```
