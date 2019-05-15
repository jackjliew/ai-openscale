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

# Eventos do Activity Tracker
{: #at-events}

Quando você tem o {{site.data.keyword.aios_short}} provisionado como um serviço em sua conta do {{site.data.keyword.cloud_notm}}, é possível ver os eventos a seguir no [{{site.data.keyword.cloud_notm}} Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-activity_tracker_ov).
{: shortdesc}

## Eventos para APIs Públicas
{: #at-pubapi}

| Ação | Descrição |
| -- | -- |
| aiopenscale.metrics.create | Armazenar métrica na instância do {{site.data.keyword.aios_short}} |
| aiopenscale.payload.create | Carga útil do log na instância do {{site.data.keyword.aios_short}} |

## Eventos para APIs privadas
{: #at-priapi}

| Ação | Descrição |
| -- | -- |
| aiopenscale.datamart.configure | Configurar a instância do {{site.data.keyword.aios_short}} |
| aiopenscale.datamart.delete | Exclua a instância do {{site.data.keyword.aios_short}} |
| aiopenscale.binding.create | Incluir ligação de serviço na instância do {{site.data.keyword.aios_short}} |
| aiopenscale.binding.delete | Excluir Ligação de Serviço a partir da {{site.data.keyword.aios_short}} Instância |
| aiopenscale.subscription.create | Incluir assinatura na instância do {{site.data.keyword.aios_short}} |
| aiopenscale.subscription.delete | Excluir assinatura da instância do {{site.data.keyword.aios_short}} |
