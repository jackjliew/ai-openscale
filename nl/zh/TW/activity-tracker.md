---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: activity, tracker, events, API, public API, subscription, binding

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

# 「活動追蹤器」的事件
{: #at-events}

當您將 {{site.data.keyword.aios_short}} 當成服務佈建於您的 {{site.data.keyword.cloud_notm}} 帳戶中之後，您可以在 [{{site.data.keyword.cloud_notm}} 活動追蹤器](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov) 中看到下事件。
{: shortdesc}

## 公用 API 事件
{: #at-pubapi}

|動作|說明|
| -- | -- |
| aiopenscale.metrics.create |將度量儲存在 {{site.data.keyword.aios_short}} 實例中|
| aiopenscale.payload.create |將有效負載記載在 {{site.data.keyword.aios_short}} 實例中|

## 專用 API 事件
{: #at-priapi}

|動作|說明|
| -- | -- |
| aiopenscale.datamart.configure |配置 {{site.data.keyword.aios_short}} 實例|
| aiopenscale.datamart.delete |刪除 {{site.data.keyword.aios_short}} 實例|
| aiopenscale.binding.create |新增服務連結至 {{site.data.keyword.aios_short}} 實例|
| aiopenscale.binding.delete |將服務連結從 {{site.data.keyword.aios_short}} 實例刪除|
| aiopenscale.subscription.create |新增訂閱至 {{site.data.keyword.aios_short}} 實例|
| aiopenscale.subscription.delete |將訂閱從 {{site.data.keyword.aios_short}} 實例刪除|
