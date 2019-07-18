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

# 평균 제곱근 오차 ![베타 태그](images/beta.png)
{: #supqualdets_squ_errors_mean}

평균 제곱근 오차(RMSE) 보기는 모델의 예측 값과 관측 값 간의 차를 보여줍니다.
{: shortdesc}

## 평균 제곱근 오차 개요
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **설명**: 모델 예측과 목표값 간의 제곱 오차 평균의 제곱근입니다.
- **기본 임계값**: 상한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **하락세**: 하락세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 회귀
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 없음

## 표시 내용 해석
{: #supqualdets_squ_errors_mean-display}

![평균 제곱근 오차 차트가 표시되어 있습니다.](images/xxxx.png)

## 계산법
{: #supqualdets_squ_errors_mean-math}

평균 제곱근 오차는 (예상 값에서 관측 값을 빼서) 제곱한 평균의 제곱근과 같습니다.

```
          ___________________________________________________________
RMSE  =  √(예상 값 - 관측 값)*(예상 값 - 관측 값)
```
