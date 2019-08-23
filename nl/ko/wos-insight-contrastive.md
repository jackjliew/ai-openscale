---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 대조 설명에서 관련 긍정 및 관련 부정을 사용함
{: #ie-pp-pn}

대조 설명에 대해 {{site.data.keyword.aios_short}}은 관련 긍정 및 관련 부정 값을 표시합니다. 
{: shortdesc}

- 관련 긍정은 개념을 결정하는 데 중요한 찾은 결과입니다.
- 관련 부정은 부재로 인해 중요한 찾지 못한 결과입니다.

{{site.data.keyword.aios_short}}은 관련 긍정을 항상 표시합니다. 하지만 표시할 관련 부정이 없는 경우가 있습니다. 이 경우에는 이 특성의 값이 이미 중앙 값에 있거나 값을 중앙값에서 멀리 이동시킨 결과로서 예측이 변경되지 않은 것입니다.

이에 대한 이해를 높이려면 {{site.data.keyword.aios_short}}이 관련 부정 값을 계산할 때 모든 특성의 값을 중앙값에서 먼 값으로 변경한다는 점을 고려하십시오. 관련 부정의 경우 이는 중앙값에서 가장 먼 특성 값을 의미합니다. 데이터 점의 값이 이미 중앙값에 있는 경우 또는 값을 중앙값에서 먼 값으로 변경한 경우에도 예측이 변경되지 않으면 표시할 관련 부정이 없습니다. 관련 긍정의 경우 {{site.data.keyword.aios_short}}은 예측이 변경되지 않도록 중앙값 쪽으로 특성 값의 최대 변경을 찾습니다. 사실상 이는 트랜잭션을 설명하는 관련 긍정이 거의 항상 있음을 의미합니다.

