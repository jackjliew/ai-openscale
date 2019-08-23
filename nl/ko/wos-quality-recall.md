---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 재현율
{: #quality_recall}

재현율은 양성 클래스에서 올바른 예측의 비율을 제공합니다.
{: shortdesc}

## 재현율 개요
{: #quality_recall-glance}

- **설명**: 양성 클래스에 대한 올바른 예측의 비율입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 2진 분류
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 오차 행렬

## 재현율 메트릭 표시 해석
{: #quality_recall-display}

![재현율 차트가 표시되어 있습니다.](images/quality-recall.png)

### 공정성 스코어
{: #quality_recall-display-fairness-score}

재현율 메트릭의 경우 다음 공정성 스코어가 표시됩니다.  

![재현율 스코어 백분율이 표시됩니다.](images/wos-quality-recall-score.png)

### 스케줄
{: #quality_recall-display-schedule}

**스케줄** 분할창은 **마지막 평가** 및 **다음 평가** 시간을 표시합니다. 수량 메트릭은 매시간 평가됩니다. **지금 품질 확인**을 클릭하여 평가를 강제 실행할 수 있습니다. **피드백 데이터 추가**를 클릭하여 피드백을 추가할 수도 있습니다. 

![마지막 평가 시간과 다음 평가 시간을 표시하는 스케줄 분할창이 표시됩니다.](images/wos-quality-schedule.png)


### 권장사항
{: #quality_recall-display-recommendations}

차트 해석에 도움이 되도록, 모델 효과를 개선 또는 개악하는 트랜드를 표시하는 **권장사항** 분할창이 표시합니다. 

![권장사항 분할창이 표시됩니다.](images/wos-quality-positive-recommendation.png)




## 계산법
{: #quality_recall-math}

재현율(R)은 참 양성(Tp) 수를 참 양성 수에 거짓 음성(Fn) 수를 더한 값으로 나눈 값으로 정의됩니다.

```
            참 양성 수
재현율 =   ______________________________________________________

           (참 양성 수 + 거짓 음성 수)
```
