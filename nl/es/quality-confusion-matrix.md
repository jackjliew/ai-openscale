---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# Confusion Matrix ![etiqueta beta](images/beta.png)
{: #it-conf-mtx}

Como un detalle de las métricas de calidad, puede ver los registros que el modelo ha analizado incorrectamente. Estas anomalías pueden ser falsos positivos o falsos negativos para modelos de clasificación binarios o pueden ser asignaciones de clases incorrectas para modelos multiclase. También puede ver una lista de los registros de opiniones que el modelo no ha analizado correctamente.
{: shortdesc}

Para consultar la información relacionada, como por ejemplo Confusion Matrix para la clasificación binaria y multiclase, que está disponible para algunas métricas, pulse en la gráfica.

![Tabla de detalles de las métricas de calidad](images/quality_metrics_002.png)

## Pasos
{: #it-conf-mtx-steps}

1. Desde cualquiera de los gráficos **Calidad**, por ejemplo **Exactitud**, pulse en una hora/día del gráfico.
    
    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.004.png)

1. Confusion Matrix muestra los falsos positivos y los falsos negativos. Pulse en una celda para ver el subconjunto de registros de opiniones.

    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.005.png)

1. Revise los registros de opiniones y solicite una explicación de los análisis en relación con el registro de opiniones.

    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.006.png)

1. Transacciones aparece en línea.

    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.007.png)

