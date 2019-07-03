---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Mean squared error

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

# 평균 제곱 오차 ![베타 태그](images/beta.png)
{: #quality_squerror}

평균 제곱 오차는 모델 예측과 목표값 간 제곱 오차의 평균을 제공합니다. 추정기의 품질 척도로 사용할 수 있습니다.
{: shortdesc}

## 평균 제곱 오차 개요
{: #quality_squerror-glance}

- **설명**: 모델 예측과 목표값 간의 제곱 오차의 평균입니다.
- **기본 임계값**: 상한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **하락세**: 하락세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 회귀
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 없음

## 표시 내용 해석
{: #quality_squerror-display}

![평균 제곱 오차 차트가 표시되어 있습니다.](images/xxxx.png)

## 계산법
{: #quality_squerror-math}

가장 단순한 형태의 평균 제곱 오차는 다음 공식으로 표시됩니다. 

```
                         SUM  (Yi - ^Yi) * (Yi - ^Yi)
평균 제곱 오차  =  ____________________________

                             오차 수
```
