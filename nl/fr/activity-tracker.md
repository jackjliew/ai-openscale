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

# Evénements d'Activity Tracker
{: #at-events}

Lorsque vous avez {{site.data.keyword.aios_short}} mis à disposition en tant que service
dans votre compte {{site.data.keyword.cloud_notm}},
vous pouvez voir les événements suivants dans
[{{site.data.keyword.cloud_notm}}Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov).
{: shortdesc}

## Evénements pour les API publiques
{: #at-pubapi}

| Action | Description |
| -- | -- |
| aiopenscale.metrics.create | Stockage d'une métrique dans l'instance de {{site.data.keyword.aios_short}} |
| aiopenscale.payload.create | Journalisation d'un contenu dans l'instance de {{site.data.keyword.aios_short}} |

## Evénements pour les API privées
{: #at-priapi}

| Action | Description |
| -- | -- |
| aiopenscale.datamart.configure | Configuration de l'instance de {{site.data.keyword.aios_short}} |
| aiopenscale.datamart.delete | Suppression de l'instance de {{site.data.keyword.aios_short}} |
| aiopenscale.binding.create | Ajout d'une liaison de service à l'instance de {{site.data.keyword.aios_short}} |
| aiopenscale.binding.delete | Suppression d'une liaison de service de l'instance de {{site.data.keyword.aios_short}} |
| aiopenscale.subscription.create | Ajout d'un abonnement à l'instance de {{site.data.keyword.aios_short}} |
| aiopenscale.subscription.delete | Suppression d'un abonnement de l'instance de {{site.data.keyword.aios_short}} |
