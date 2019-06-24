---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: activity, tracker, events, API, public API, subscription, binding

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Activity Tracker 이벤트
{: #at-events}

{{site.data.keyword.cloud_notm}} 계정에 서비스로 프로비저닝된 {{site.data.keyword.aios_short}}이 있으면 [{{site.data.keyword.cloud_notm}} Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov)에서 다음 이벤트를 볼 수 있습니다.
{: shortdesc}

## 공용 API용 이벤트
{: #at-pubapi}

| 조치 |설명 |
| -- | -- |
| aiopenscale.metrics.create | {{site.data.keyword.aios_short}} 인스턴스에 메트릭 저장 |
| aiopenscale.payload.create | {{site.data.keyword.aios_short}} 인스턴스에 페이로드 로그 |

## 개인 API용 이벤트
{: #at-priapi}

| 조치 |설명 |
| -- | -- |
| aiopenscale.datamart.configure | {{site.data.keyword.aios_short}} 인스턴스 구성 |
| aiopenscale.datamart.delete | {{site.data.keyword.aios_short}} 인스턴스 삭제 |
| aiopenscale.binding.create | {{site.data.keyword.aios_short}} 인스턴스에 서비스 바인딩 추가 |
| aiopenscale.binding.delete | {{site.data.keyword.aios_short}} 인스턴스에서 서비스 바인딩 삭제 |
| aiopenscale.subscription.create | {{site.data.keyword.aios_short}} 인스턴스에 구독 추가 |
| aiopenscale.subscription.delete | {{site.data.keyword.aios_short}} 인스턴스에서 구독 삭제 |
