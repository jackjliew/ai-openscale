---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted False Positive Rate, wFPR

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

# 가중된 거짓 양성 비율(wFPR) ![베타 태그](images/beta.png)
{: #quality_wfpr_weighted}

가중된 거짓 양성 비율(wFPR)은 클래스 확률과 동일한 가중치로 가중된 클래스 거짓 양성 비율(FPR) 평균을 제공합니다.
{: shortdesc}

## 가중된 거짓 양성 비율(wFPR) 개요
{: #quality_wfpr_weighted-glance}

- **설명**: 클래스 가능성과 동일한 가중치로 가중된 클래스 FPR의 평균입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 다중 클래스 분류
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 오차 행렬

## 표시 내용 해석
{: #quality_wfpr_weighted-display}

![가중된 거짓 양성 비율 차트가 표시되어 있습니다.](images/quality-fpr.png)

## 계산법
{: #quality_wfpr_weighted-math}

가중된 거짓 양성 비율은 가중 데이터를 사용하여 FPR를 적용한 결과입니다. 

```
                   거짓 양성 수
FPR =  ______________________________________________________

       (거짓 양성 수 + 참 음성 수)
```
