---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: drift, behavior, metrics

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

# 드리프트 발견 ![베타 태그](images/beta.png)
{: #behavior-drift-ovr}

시간이 지나면서 모델의 특정 기능에 대한 중요성과 영향이 달라지고 있습니다. 이는 연관된 애플리케이션과 이로 인해 발생하는 비즈니스 결과에 영향을 미칩니다. {{site.data.keyword.aios_short}}에서는 드리프트 발견을 통해 모델 메트릭, 모델 성능 및 시간 경과에 따라 기능 영향력이 달라지는 방식을 추적할 수 있습니다. 드리프트란 숨겨진 컨텍스트 때문에 시간이 경과하면서 예상 성능이 저하되는 것을 말합니다. 시간이 경과하면서 데이터가 변경되면 모델의 정확한 예측 수행 능력이 쇠퇴할 수 있습니다. {{site.data.keyword.aios_short}}에서는 사용자가 정정 조치를 취할 수 있도록 드리프트를 발견하고 강조표시합니다.
{: shortdesc}

{{site.data.keyword.aios_short}}에서는 모든 트랜잭션을 분석하여 드리프트의 원인이 되는 트랜잭션을 찾아냅니다. 그런 다음 드리프트의 중요한 원인이 되는 속성 값을 기준으로 레코드를 그룹화합니다. 

## 드리프트 개요
{: #behavior-drift-glance}




## 표시 내용 해석
{: #behavior-drift-display}

![설정된 임계값 미만 드리프트를 보여주는 공정성 지표 차트](images/fairness_metrics_001.png)


## 계산법
{: #behavior-drift-math}

{{site.data.keyword.aios_short}}에서 드리프트를 계산합니다.  
