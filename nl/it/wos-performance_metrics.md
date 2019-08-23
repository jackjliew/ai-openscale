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

# Panoramica sulle metriche delle prestazioni ![tag beta](images/beta.png)
{: #anlz_metrics_performance}

Utilizzare il monitoraggio delle prestazioni per conoscere la velocità dei record di dati elaborati dalla distribuzione. È possibile abilitare il monitoraggio delle prestazioni quando si seleziona la distribuzione che deve essere tracciata e monitorata da {{site.data.keyword.aios_short}}.
{: shortdesc}

Le metriche di prestazione sono calcolate in base alle seguenti informazioni:

- calcolo del punteggio dei dati del payload

Al fine di un corretto monitoraggio, ogni richiesta di calcolo del punteggio dovrebbe essere registrata anche in {{site.data.keyword.aios_short}}. La registrazione dei dati di payload è automatizzata per i motori {{site.data.keyword.pm_full}}. Per altri motori di machine learning, i dati del payload possono essere forniti utilizzando il client Python o l'API REST. Il monitoraggio delle prestazioni non crea ulteriori richieste di calcolo del punteggio sulla distribuzione monitorata.

È possibile esaminare i valori delle metriche di prestazione nel tempo sul dashboard {{site.data.keyword.aios_short}}:

![grafico prestazioni](images/performance_metrics_001.png)

## Metriche delle prestazioni supportate
{: #anlz_metrics_performance_supp_quality_mets}

Le seguenti metriche delle prestazioni sono supportate da {{site.data.keyword.aios_short}}:

- [Velocità di trasmissione dei dati](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
