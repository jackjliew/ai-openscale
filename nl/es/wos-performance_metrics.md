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

# Descripción general de las métricas de rendimiento ![etiqueta beta](images/beta.png)
{: #anlz_metrics_performance}

Utilice la supervisión de rendimiento para conocer la velocidad de los registros de datos procesados por el despliegue. La supervisión de rendimiento se habilita al seleccionar el despliegue para el seguimiento y la supervisión por parte de {{site.data.keyword.aios_short}}.
{: shortdesc}

Las métricas de rendimiento se calculan en función de la información siguiente:

- Los datos de carga útil de puntuación

Para una supervisión adecuada, cada solicitud de puntuación se debe registrar también en {{site.data.keyword.aios_short}}. El registro de datos de carga útil está automatizado para los motores de {{site.data.keyword.pm_full}}. Para otros motores de aprendizaje automático, los datos de carga útil se pueden proporcionar mediante el cliente Python o la API REST. La supervisión de rendimiento no crea ninguna solicitud de puntuación adicional en el despliegue supervisado.

Puede revisar el valor de las métricas de rendimiento a lo largo del tiempo en el panel de control de {{site.data.keyword.aios_short}}:

![Gráfico de rendimiento](images/performance_metrics_001.png)

## Métricas de rendimiento soportadas
{: #anlz_metrics_performance_supp_quality_mets}

{{site.data.keyword.aios_short}} da soporte a las siguientes métricas de rendimiento:

- [Productividad](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
