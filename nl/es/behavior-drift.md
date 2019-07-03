---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: drift, behavior, metrics

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

# Detección de desviación ![etiqueta beta](images/beta.png)
{: #behavior-drift-ovr}

A lo largo del tiempo, la importancia y el impacto de determinadas características en un cambio de modelo. Esto afecta a las aplicaciones asociadas y a los resultados de negocio resultantes. Mediante la detección de desviación, {{site.data.keyword.aios_short}} proporciona una forma de realizar un seguimiento de las métricas del modelo, el rendimiento del modelo y cómo cambia con el tiempo la ponderación de las características. La desviación es la degradación del rendimiento predictivo a lo largo del tiempo debido a un contexto oculto. A medida que los datos cambian a lo largo del tiempo, la capacidad del modelo para hacer predicciones exactas puede decaer. {{site.data.keyword.aios_short}} detecta y resalta la desviación para que se pueda llevar a cabo la acción correctiva correspondiente.
{: shortdesc}

{{site.data.keyword.aios_short}} analiza todas las transacciones para encontrar las que contribuyen a la desviación. A continuación, agrupa los registros en función de los valores de los atributos que han contribuido de forma significativa a la desviación.

## Detalles de la desviación
{: #behavior-drift-glance}




## Interpretación de la pantalla
{: #behavior-drift-display}

![gráfico de métricas de equidad que muestra una desviación por debajo del umbral](images/fairness_metrics_001.png)


## Cómo calcularlo
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} calcula la desviación 
