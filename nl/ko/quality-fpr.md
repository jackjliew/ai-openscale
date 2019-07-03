---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# 거짓 양성 비율(FPR) ![베타 태그](images/beta.png)
{: #quality_fpr_false}

거짓 양성 비율은 양성 클래스에서 잘못된 예측의 비율을 제공합니다.
{: shortdesc}

## 거짓 양성 비율(FPR)
{: #quality_fpr_false-glance}

- **설명**: 양성 클래스에 대한 잘못된 예측의 비율입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 2진 분류
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 오차 행렬

## 표시 내용 해석
{: #quality_fpr_false-display}

![거짓 양성 비율 차트가 표시되어 있습니다.](images/quality-fpr.png)

## 계산법
{: #quality_fpr_false-math}

거짓 양성 비율은 총 거짓 양성 수를 거짓 양성 수에 참 음성 수를 더한 값으로 나눠서 계산됩니다. 

```
                        총 거짓 양성 수
거짓 양성 비율 =  ______________________________________________________

                       (거짓 양성 수 + 참 음성 수)
```
