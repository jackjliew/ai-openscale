---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Activity Tracker-Ereignisse
{: #at-events}

Wenn Sie {{site.data.keyword.aios_short}} als Service in Ihrem {{site.data.keyword.cloud_notm}}-Konto eingerichtet haben, werden die folgenden Ereignisse in [{{site.data.keyword.cloud_notm}} Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov){: external} angezeigt.
{: shortdesc}

## Ereignisse für öffentliche APIs
{: #at-pubapi}

| Aktion | Beschreibung |
| -- | -- |
| aiopenscale.metrics.create | Speichern der Metrik in der {{site.data.keyword.aios_short}}-Instanz |
| aiopenscale.payload.create | Protokollieren der Nutzdaten in der {{site.data.keyword.aios_short}}-Instanz |

## Ereignisse für private APIs
{: #at-priapi}

| Aktion | Beschreibung |
| -- | -- |
| aiopenscale.datamart.configure | Konfigurieren der {{site.data.keyword.aios_short}}-Instanz |
| aiopenscale.datamart.delete | Löschen der {{site.data.keyword.aios_short}}-Instanz |
| aiopenscale.binding.create | Hinzufügen einer Servicebindung zur {{site.data.keyword.aios_short}}-Instanz |
| aiopenscale.binding.delete | Servicebindung aus der {{site.data.keyword.aios_short}}-Instanz löschen |
| aiopenscale.subscription.create | Hinzufügen des Abonnements zur {{site.data.keyword.aios_short}}-Instanz |
| aiopenscale.subscription.delete | Löschen des Abonnements aus der {{site.data.keyword.aios_short}}-Instanz |
