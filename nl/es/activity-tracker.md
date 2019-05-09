---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: activity, tracker, events, API, public API

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

# Sucesos de Activity Tracker
{: #at-events}

Cuando tiene {{site.data.keyword.aios_short}} suministrado como servicio en su cuenta de {{site.data.keyword.cloud_notm}}, puede ver los sucesos siguientes en [{{site.data.keyword.cloud_notm}} Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov).
{: shortdesc}

## Sucesos para las API públicas
{: #at-pubapi}

| Acción | Descripción |
| -- | -- |
| aiopenscale.metrics.create | Almacenar métrica en la instancia de {{site.data.keyword.aios_short}} |
| aiopenscale.payload.create | Registrar carga útil en la instancia de {{site.data.keyword.aios_short}} |

## Sucesos para las API privadas
{: #at-priapi}

| Acción | Descripción |
| -- | -- |
| aiopenscale.datamart.configure | Configurar la instancia de {{site.data.keyword.aios_short}} |
| aiopenscale.datamart.delete | Suprimir la instancia de {{site.data.keyword.aios_short}} |
| aiopenscale.binding.create | Añadir enlace de servicio a la instancia de {{site.data.keyword.aios_short}} |
| aiopenscale.binding.delete | Suprimir enlace de servicio de la instancia de {{site.data.keyword.aios_short}} |
| aiopenscale.subscription.create | Añadir suscripción a la instancia de {{site.data.keyword.aios_short}} |
| aiopenscale.subscription.delete | Suprimir suscripción de la instancia de {{site.data.keyword.aios_short}} |
