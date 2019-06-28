---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de métricas y transacciones ![etiqueta beta](images/beta.png)
{: #anlz_metrics}

Puede utilizar {{site.data.keyword.aios_full}} para analizar métricas y transacciones mediante diversos medios.
{: shortdesc}

## Confusion Matrix ![etiqueta beta](images/beta.png)
{: #it-conf-mtx}

Como un detalle de las métricas de calidad, puede ver los registros que el modelo ha analizado incorrectamente. Estas anomalías pueden ser falsos positivos o falsos negativos para modelos de clasificación binarios o pueden ser asignaciones de clases incorrectas para modelos multiclase. También puede ver una lista de los registros de opiniones que el modelo no ha analizado correctamente.
{: shortdesc}

1. Desde cualquiera de los gráficos **Calidad**, por ejemplo **Equidad** pulse en una hora/día del gráfico.
    
    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.004.png)

1. Confusion Matrix muestra los falsos positivos y los falsos negativos. Pulse en una celda para ver el subconjunto de registros de opiniones.

    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.005.png)

1. Revise los registros de opiniones y solicite una explicación de los análisis en relación con el registro de opiniones.

    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.006.png)

1. Transacciones aparece en línea.

    ![Lista de transacciones sesgadas](images/Confusion_Matrix_040819.007.png)

