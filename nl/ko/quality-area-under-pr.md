---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under PR

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

# PR 아래 영역 ![베타 태그](images/beta.png)
{: #quality-area-pr}

PR(Precision Recall) 아래 영역은 정밀도 및 재현율 곡선 아래에 영역을 제공하며, 클래스가 특히 불균형할 때 유용할 수 있습니다.
{: shortdesc}

## PR 아래 영역 개요
{: #quality-area-pr-glance}

- **설명**: 정밀도 및 재현율 곡선 아래의 영역입니다.
- **기본 임계값**: 하한값 = 80%
- **기본 권장사항**:
   - **상승세**: 상승세는 메트릭이 개선되고 있음을 표시합니다. 모델 재훈련이 효과적임을 의미합니다.
   - **하락세**: 하락세는 메트릭이 나빠지고 있음을 표시합니다. 피드백 데이터가 훈련 데이터와 크게 달라집니다.
   - **불규칙하거나 일정하지 않은 변화**: 불규칙하거나 일정하지 않은 변화는 피드백 데이터가 평가 간에 일관되지 않음을 표시합니다. 품질 모니터에 대한 최소 샘플 크기를 늘리십시오.
- **문제점 유형**: 2진 분류
- **차트 값**: 시간 범위의 마지막 값
- **메트릭 세부사항 사용 가능**: 오차 행렬

## 표시 내용 해석
{: #quality-area-pr-display}

![PR 아래 영역이 하향 메트릭 추세로 표시됩니다. ](images/quality-area-under-pr.png)


## 계산법
{: #quality-area-pr-math}

정밀도 재현율 아래 영역은 `정밀도 + 재현율`에 대한 총계를 제공합니다. 

정밀도(P)는 참 양성(Tp) 수를 참 양성 수에 거짓 양성(Fp) 수를 더한 값으로 나눈 값으로 정의됩니다. 

```
               참 양성 수
정밀도 =   ______________________________________________________

              (참 양성 수 + 거짓 양성 수)
```

재현율(R)은 참 양성(Tp) 수를 참 양성 수에 거짓 음성(Fn) 수를 더한 값으로 나눈 값으로 정의됩니다. 

```
            참 양성 수
재현율 =   ______________________________________________________

           (참 양성 수 + 거짓 음성 수)
```
