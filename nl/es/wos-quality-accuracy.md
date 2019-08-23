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

# Exactitud
{: #accuracy-opener}

Exactitud es una medida de la proporción de predicciones correctas que contiene el modelo.
{: shortdesc}

## Detalles de la exactitud
{: #anlz_metrics_supqualdets_acc}

- **Descripción**: la proporción de predicciones correctas
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipos de problema**: clasificación binaria y clasificación multiclase
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix


## Información sobre la Exactitud
{: #acc-understand}

La exactitud puede indicar distintos aspectos en función del tipo de algoritmo:

- *Clasificación multiclase*: la exactitud mide el número de veces que se ha previsto correctamente cualquier clase, normalizada por el número de puntos de datos. Para
obtener más detalles, consulte [Multi-class classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external} en la documentación de Apache Spark.

- *Clasificación binaria*: para un algoritmo de clasificación binaria, la exactitud se mide como el área bajo una curva ROC. Consulte
[Binary classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external} en la documentación de Apache Spark para obtener más detalles.

- *Regresión*: los algoritmos de regresión se miden utilizando el Coeficiente de determinación, o R2. Para obtener más detalles,
consulte la [Evaluación del modelo de regresión](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external} en la documentación de Apache Spark.

### Cómo funciona
{: #acc-works}

Debe añadir datos de opinión etiquetados manualmente mediante la interfaz de usuario de {{site.data.keyword.aios_short}} tal como se muestra
en los ejemplos siguientes, utilizando un [cliente de
Python](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external} o una
[Rest API](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external}.

### Precisión sin sesgo
{: #acc-debias-view}

Cuando hay datos que le dan soporte, la exactitud se calcula en el modelo original y en el modelo sin sesgo. {{site.data.keyword.aios_full_notm}} calcula la exactitud de la salida sin sesgo y la almacena en la tabla de registro de carga útil como una columna adicional.

![Aparece una visualización de modelo con la exactitud calculada para el modelo original y para el modelo sin sesgo](images/debiased-accuracy.png)
