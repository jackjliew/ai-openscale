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

# 성능 메트릭 개요 ![베타 태그](images/beta.png)
{: #anlz_metrics_performance}

성능 모니터링을 사용하여 배치에서 처리하는 데이터 레코드의 속도를 알 수 있습니다. {{site.data.keyword.aios_short}}에서 추적하고 모니터링할 배치를 선택하는 경우 성능 모니터링을 사용으로 설정합니다.
{: shortdesc}

성능 메트릭은 다음 정보를 기반으로 계산됩니다.

- 스코어링 페이로드 데이터

적합한 모니터링을 위해 모든 스코어링 요청을 {{site.data.keyword.aios_short}}에도 기록해야 합니다. 페이로드 데이터 로깅은 {{site.data.keyword.pm_full}} 엔진에 대해 자동으로 설정되어 있습니다. 다른 기계 학습 엔진의 경우 Python 클라이언트 또는 REST API를 사용하여 페이로드 데이터를 제공할 수 있습니다. 성능 모니터링은 모니터링된 배치에 대한 추가 스코어링 요청을 작성하지 않습니다.

{{site.data.keyword.aios_short}} 대시보드에서 시간이 경과함에 따른 성능 메트릭 값을 검토할 수 있습니다.

![성능 차트](images/performance_metrics_001.png)

## 지원되는 성능 메트릭
{: #anlz_metrics_performance_supp_quality_mets}

다음 성능 메트릭이 {{site.data.keyword.aios_short}}에서 지원됩니다.

- [처리량](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
