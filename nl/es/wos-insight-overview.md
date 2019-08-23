---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: dashboard, navigating, navigation, insights

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

# Obtención de detalles con {{site.data.keyword.aios_short}}
{: #io-ov}

Puede realizar un seguimiento de todos los despliegues que está supervisando mediante el panel de control de {{site.data.keyword.aios_full}}. El panel de control es la vista principal de {{site.data.keyword.aios_short}} y le proporciona la forma de obtener detalles del rendimiento de sus modelos.
{: shortdesc}

## Detalles
{: #io-ins}

La pestaña **Detalles** (![Panel de control Detalles](images/insight-dash-tab.png)) proporciona una vista de alto nivel de su supervisión del despliegue.

  ![Panel de control Detalles](images/insight-dashboard.png)

- ***Despliegues supervisados***: en este ejemplo, se supervisan un total de 10 despliegues. Ocho de los diez
despliegues se muestran como mosaicos individuales.

- ***Alertas de Calidad***: un total de 3 alertas de Calidad (denominada anteriormente Exactitud) que se representan en los mosaicos siguientes. En este ejemplo, los despliegues `Rendimiento de controlador`, `Análisis de mercado` y `Riesgo de precios` muestran los valores de Exactitud de `60%`, `65%` y `79%`, respectivamente.

- ***Alertas de equidad***: Hay un total de 6 alertas de equidad, representadas en los mosaicos siguientes y con una
pequeña etiqueta `BIAS`. En este ejemplo, los despliegues `Rendimiento de controlador`, `Análisis de mercado`, `Conformidad normativa`, `Detección de fraudes`, `Optimización Premium` y `Estimación de coste de daños` muestran valores de Equidad de `59%`, `68%`, `62%`, `64%`, `79%` y `63%`, respectivamente.

Cada mosaico proporciona un resumen de la actividad de supervisión para ese despliegue. Observe que el despliegue `Direccionamiento de centro de llamadas` no muestra ningún problema, lo que indica un modelo preciso y considerablemente estable.


## Detalles de equidad, calidad, rendimiento, exactitud y análisis
{: #it-ov}

Seleccione cualquiera de los mosaicos de despliegue individuales para ver más detalles sobre ese despliegue. Se muestran datos de supervisión para despliegues individuales en una serie de gráficos. Los gráficos realizan el seguimiento de las métricas, como por ejemplo la equidad, el promedio de solicitudes por minuto y la exactitud a lo largo de los días, las semanas o los meses.

- [Visualización de los datos para un despliegue](/docs/services/ai-openscale?topic=ai-openscale-it-vdep)
- [Visualización de los datos correspondientes a una hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-vdet)
- [Equidad](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)
- [Calidad](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)
- [Desviación](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
- [Rendimiento](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_performance)
- [Análisis](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)
- [Opciones para la eliminación del sesgo](/docs/services/ai-openscale?topic=ai-openscale-it-dbo)

## Explicabilidad
{: #io-tran}

Utilice la pestaña **Explicar una transacción** (![pestaña Explicar una transacción](images/insight-transact-tab.png)) para buscar un ID de transacción específico para explicar una transacción de despliegue determinada.

- [Explicación de las transacciones](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)
- [Explicación de los modelos categóricos](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Explicación de los modelos de imagen](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Explicación de los modelos de texto no estructurado](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Explicaciones contrastativas](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)

## Pasos siguientes
{: #io-next}

- [Añadir más despliegues para supervisar](/docs/services/ai-openscale?topic=ai-openscale-dpl-select).

