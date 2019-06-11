---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Activity Tracker 事件
{: #at-events}

将 {{site.data.keyword.aios_short}} 作为 {{site.data.keyword.cloud_notm}} 帐户中的服务供应时，您可以在 [{{site.data.keyword.cloud_notm}} Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov) 中看到以下事件：
{: shortdesc}

## 公共 API 的事件
{: #at-pubapi}

| 操作 |描述|
| -- | -- |
| aiopenscale.metrics.create | 存储 {{site.data.keyword.aios_short}} 实例中的度量 |
| aiopenscale.payload.create | 记录 {{site.data.keyword.aios_short}} 实例中的载荷 |

## 专用 API 的事件
{: #at-priapi}

| 操作 |描述|
| -- | -- |
| aiopenscale.datamart.configure | 配置 {{site.data.keyword.aios_short}} 实例 |
| aiopenscale.datamart.delete | 删除 {{site.data.keyword.aios_short}} 实例 |
| aiopenscale.binding.create | 向 {{site.data.keyword.aios_short}} 实例中添加服务绑定 |
| aiopenscale.binding.delete | 从 {{site.data.keyword.aios_short}} 实例中删除服务绑定 |
| aiopenscale.subscription.create | 向 {{site.data.keyword.aios_short}} 实例中添加预订 |
| aiopenscale.subscription.delete | 从 {{site.data.keyword.aios_short}} 实例中删除预订 |
