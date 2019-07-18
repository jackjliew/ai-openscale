---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# 설명 분산의 비율 ![베타 태그](images/beta.png)
{: #quality_var}

설명 분산의 비율은 설명 분산과 목표 분산의 비율을 제공합니다. 설명 분산은 대상 분산과 예측 오차 분산 간의 차이입니다.
{: shortdesc}

## 설명 분산의 비율 개요
{: #quality_var-glance}

- **설명**: 설명 분산의 비율은 설명 분산과 대상 분산의 비율입니다. 설명 분산은 대상 분산과 예측 오차 분산 간의 차이입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 회귀
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 없음

## 표시 내용 해석
{: #quality_var-display}

![설명 분산의 비율 차트가 표시되어 있습니다.](images/xxxx.png)

## 계산법
{: #quality_var-math}

설명 분산의 비율은 숫자의 평균을 구한 후 각 숫자에서 평균을 빼고 그 결과를 제곱하여 계산됩니다. 그런 다음 제곱을 수행합니다.

```
                                  그룹 간 제곱합
설명 분산의 비율 =  ________________________________

                                      제곱 총계의 합
```
