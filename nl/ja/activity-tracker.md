---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

# Activity Tracker イベント
{: #at-events}

{{site.data.keyword.cloud_notm}} アカウント内で {{site.data.keyword.aios_short}} をサービスとしてプロビジョンしたら、[{{site.data.keyword.cloud_notm}} Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov) で次のイベントを参照できます。

## パブリック API に関するイベント
{: #at-pubapi}

| アクション | 説明 |
| -- | -- |
| aiopenscale.metrics.create | {{site.data.keyword.aios_short}} インスタンス内でメトリックを保管します |
| aiopenscale.payload.create | {{site.data.keyword.aios_short}} インスタンス内でペイロードを記録します |

## プライベート API に関するイベント
{: #at-priapi}

| アクション | 説明 |
| -- | -- |
| aiopenscale.datamart.configure | {{site.data.keyword.aios_short}} インスタンスを構成します |
| aiopenscale.datamart.delete | {{site.data.keyword.aios_short}} インスタンスを削除します |
| aiopenscale.binding.create | {{site.data.keyword.aios_short}} インスタンスにサービス・バインディングを追加します |
| aiopenscale.binding.delete | {{site.data.keyword.aios_short}} インスタンスからサービス・バインディングを削除します |
| aiopenscale.subscription.create | {{site.data.keyword.aios_short}} インスタンスにサブスクリプションを追加します |
| aiopenscale.subscription.delete | {{site.data.keyword.aios_short}} インスタンスからサブスクリプションを削除します |
