---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Magnitud de la desviación ![etiqueta beta](images/beta.png)
{: #behavior-drift-ovr}

A lo largo del tiempo, la importancia y el impacto de determinadas características en un cambio de modelo. Esto afecta a las aplicaciones asociadas y a los resultados de negocio resultantes. Mediante la detección de desviación, {{site.data.keyword.aios_short}} proporciona una forma de realizar un seguimiento de las métricas del modelo, el rendimiento del modelo y cómo cambia con el tiempo la ponderación de las características. A medida que los datos cambian, la capacidad del modelo para hacer predicciones exactas puede empeorar. La magnitud de la desviación es el grado de degradación del rendimiento predictivo a lo largo del tiempo. Utilice la información sobre desviación para realizar la acción correctiva.
{: shortdesc}

## Información sobre la detección de desviación
{: #behavior-drift-understand}

La desviación es la degradación del rendimiento predictivo a lo largo del tiempo debido a un contexto oculto. A medida que los datos cambian a lo largo del tiempo, la capacidad del modelo para hacer predicciones exactas puede empeorar. {{site.data.keyword.aios_short}} detecta y resalta la desviación para que se pueda llevar a cabo la acción correctiva correspondiente.

### Cómo funciona
{: #behavior-drift-works}

{{site.data.keyword.aios_short}} analiza todas las transacciones para encontrar las que contribuyen a la desviación. A continuación, agrupa los registros en función de los valores de los atributos que han contribuido de forma significativa a la desviación.

### Cómo calcularlo
{: #behavior-drift-math}

Cada tres horas, {{site.data.keyword.aios_short}} calcula la desviación analizando los mismos datos de entrenamiento que ya ha analizado el modelo predictivo. A continuación, compara los resultados con las predicciones del modelo. Si hay cambios o discrepancias, {{site.data.keyword.aios_short}} calcula el alcance de la desviación y, según el umbral que se haya definido, le alerta de la aparición. 


### Visualización de la desviación
{: #behavior-drift-display}

La visualización de la desviación incluye datos estadísticos gráficos y numéricos:

![gráfico de métricas de equidad que muestra una desviación por debajo del umbral](images/drift-example.png)

Si pulsa en el gráfico, puede visualizar las transacciones específicas que contribuyen a la desviación. Se muestran las principales razones de la desviación detectada y se incluye una descripción en lenguaje natural de la observación, así como una lista de los valores inesperados.

![gráfico de métricas de equidad que muestra una desviación por debajo del umbral](images/drift-detection-example.png)

Las transacciones de desviación están disponibles en la pantalla de detalles de transacciones, donde puede pulsar **Explicar** para comprender cómo una transacción específica ha acabado en la categoría de desviación:

![gráfico de métricas de equidad que muestra una desviación por debajo del umbral](images/drift-detection-transactions.png)


## Pasos siguientes

- Para obtener información sobre cómo configurar la detección de desviación, consulte [Configuración del supervisor de detección de desviación](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
- Para mitigar la desviación, una vez que Watson OpenScale la ha detectado, debe crear una nueva versión del modelo que corrija el problema. Un buen lugar por donde empezar es con los puntos de datos resaltados como motivos de la desviación. Introduzca los nuevos datos en el modelo predictivo una vez que haya etiquetado manualmente las transacciones desviadas y utilícelos para reentrenar el modelo.


