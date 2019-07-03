---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased, Logarithmic loss

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

# 로그 손실 ![베타 태그](images/beta.png)
{: #quality_log_loss}

로그 손실은 대상 클래스 가능성(신뢰도)의 로그 평균을 제공합니다. 기대 로그 우도라고도 하며, 모델 성능을 가늠하는 효과적인 척도입니다.
{: shortdesc}

## 로그 손실 개요
{: #quality_log_loss-glance}

- **설명**: 대상 클래스 가능성(신뢰도)의 로그 평균입니다. 기대 로그 우도라고도 합니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 2진 분류 및 다중 클래스 분류
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 없음

## 표시 내용 해석
{: #quality_log_loss-display}

![로그 손실이 표시되어 있습니다.](images/quality-log-loss.png)

## 계산법
{: #quality_log_loss-math}

2진 모델의 경우 다음 공식을 사용하여 로그 손실이 계산됩니다. 

```
-(y log(p) + (1-y)log(1-p))
```

p = 참 레이블, y = 예측 확률

다중 클래스 모델의 경우 다음 공식을 사용하여 로그 손실이 계산됩니다. 

```
  M
-SUM Yo,c log(Po,c)
 c=1 
```

M > 2, p = 참 레이블, y = 예측 확률
