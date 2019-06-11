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

# Eventi di Activity Tracker
{: #at-events}

Quando si dispone di {{site.data.keyword.aios_short}} fornito come servizio nel proprio account {{site.data.keyword.cloud_notm}}, è possibile visualizzare i seguenti eventi in Activity Tracker di [{{site.data.keyword.cloud_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov).
{: shortdesc}

## Eventi per le API pubbliche
{: #at-pubapi}

| Azione | Descrizione |
| -- | -- |
| aiopenscale.metrics.create | Memorizza la metrica nell'istanza {{site.data.keyword.aios_short}} |
| aiopenscale.payload.create | Registra il payload nell'istanza {{site.data.keyword.aios_short}} |

## Eventi per le API private
{: #at-priapi}

| Azione | Descrizione |
| -- | -- |
| aiopenscale.datamart.configure | Configura l'istanza {{site.data.keyword.aios_short}} |
| aiopenscale.datamart.delete | Elimina l'istanza {{site.data.keyword.aios_short}} |
| aiopenscale.binding.create | Aggiunge il bind del servizio all'istanza {{site.data.keyword.aios_short}} |
| aiopenscale.binding.delete | Elimina il bind del servizio dall'istanza {{site.data.keyword.aios_short}} |
| aiopenscale.subscription.create | Aggiunge la sottoscrizione all'istanza {{site.data.keyword.aios_short}} |
| aiopenscale.subscription.delete | Elimina la sottoscrizione dall'istanza {{site.data.keyword.aios_short}} |
