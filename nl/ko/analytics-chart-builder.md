---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# 차트 빌더 ![베타 태그](images/beta.png)
{: #chart_builder}

모델 예측 및 입력을 런타임 시 더 잘 파악할 수 있도록 {{site.data.keyword.aios_short}} 차트 빌더를 사용하여 사용자 정의 시각화를 작성할 수 있습니다. 차트 빌더를 통해 기업에서 중요한 것으로 간주하는 기능 또는 데이터 범위을 기준으로 모델 예측 결과를 확인할 수 있습니다. 차트 빌더는 비즈니스 및 데이터 과학 팀에서 AI 모델을 변경할 수 있도록 데이터의 새로운 추세를 찾아내는 데 도움이 됩니다.
{: shortdesc}

예를 들어 튜토리얼의 신용 위험 모델에 익숙한 경우, 신용 히스토리 속성의 여러 범위에 대한 예측 클래스의 분할을 확인할 수 있습니다.  

   ![기능 수명을 기준으로 성별에 대한 기능 예측을 보여주는 차트](images/by_custom_chart.png)
      
   신용 히스토리의 해당 범위에 대해 예측할 때 모델의 신뢰도를 확인할 수도 있습니다. 사용자 정의 차트(기능, 예측 클래스 및 신뢰도 중에서 선택)를 통해, 선택한 데이터 범위에 있는 배치로 전송되는 스코어링 페이로드를 분석할 수 있습니다. 

   ![기능 수명을 기준으로 성별에 대한 기능 예측을 보여주는 차트](images/by_custom_chart002.png)
   
