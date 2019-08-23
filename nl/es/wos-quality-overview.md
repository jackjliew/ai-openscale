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

# Descripción general de las métricas de calidad
{: #anlz_metrics}

Utilice la supervisión de calidad para determinar con qué exactitud el modelo predice los resultados. Cuando la supervisión de calidad está habilitada, de forma predeterminada genera un conjunto de métricas cada hora. Puede generar estas métricas bajo demanda pulsando el botón **Comprobar calidad ahora** o utilizando el cliente Python.
{: shortdesc}

Las métricas de calidad se calculan según la siguiente información:

- Los datos de opiniones etiquetados manualmente
- Las respuestas de despliegue supervisado para estos datos.

Para una supervisión adecuada, los datos de opiniones se deben registrar regularmente en {{site.data.keyword.aios_short}}. Los datos de opiniones se pueden proporcionar mediante la opción "Añadir datos de opiniones" o mediante el cliente Python o la API REST.

Para motores de aprendizaje automático que no sean {{site.data.keyword.aios_short}}, como por ejemplo Microsoft Azure ML Studio, Microsoft Azure ML Service o Amazon Sagemaker ML, la supervisión de calidad crea solicitudes de puntuación adicionales en el despliegue supervisado.
{: note}

Puede revisar los valores de todas las métricas a lo largo del tiempo en el panel de control de {{site.data.keyword.aios_short}}:

![Gráfico de métricas de calidad que muestra desviación del área bajo ROC](images/quality_metrics_001.png)


Para consultar la información relacionada, como por ejemplo Confusion Matrix para la clasificación binaria y multiclase, que está disponible para algunas métricas, pulse en la gráfica.

![Tabla de detalles de las métricas de calidad](images/quality_metrics_002.png)

## Métricas de calidad soportadas
{: #anlz_metrics_supqualdets}

{{site.data.keyword.aios_short}} da soporte a las métricas de calidad siguientes:

- [Área bajo ROC](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [Área bajo PR](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [Proporción de varianza explicada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_var)
- [Error absoluto promedio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_abserror)
- [Error cuadrático promedio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_squerror)
- [R cuadrado](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_r_squared)
- [Raíz del error cuadrático promedio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-supqualdets_squ_errors_mean)
- [Exactitud](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [Índice de verdaderos positivos ponderados (wTPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-wtpr)
- [Índice de verdaderos positivos (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [Índice de falsos positivos ponderados (wFPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wfpr_weighted)
- [Índice de falsos positivos (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [Exhaustividad ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_weighted_recall)
- [Exhaustividad](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [Precisión ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wgth_prec)
- [Precisión](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [Medida F1 ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wght_f1-measure)
- [Medida F1](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [Pérdida logarítmica](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## Detalles de calidad soportados
{: #anlz_metrics_supqualdets_suppr_dets}

{{site.data.keyword.aios_short}} da soporte a los siguientes detalles de métricas de calidad:

### Confusion Matrix
{: #anlz_metrics_supqualdets_confusion-quickovr}

Confusion Matrix le ayuda a comprender para cuáles de sus datos de opiniones la respuesta de despliegue supervisado es correcta y para cuáles no lo es.

Para obtener más información, consulte [Confusion Matrix](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx).

## Pasos siguientes

- Después de que {{site.data.keyword.aios_short}} detecte problemas con la calidad, como por ejemplo violaciones de umbrales de exactitud, debe crear una nueva versión del modelo que corrija el problema. Utilizando los datos etiquetados manualmente en la tabla de opinión, debe reentrenar el modelo junto con los datos de entrenamiento originales.

