---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted False Positive Rate, wFPR

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

# Índice de falsos positivos ponderados (wFPR)
{: #quality_wfpr_weighted}

El índice de falsos positivos (wFPR) proporciona el promedio ponderado de la clase Indice de falsos positivos (FPR) con ponderaciones iguales a la probabilidad de clase.
{: shortdesc}

## Detalles del índice de falsos positivos ponderados (wFPR)
{: #quality_wfpr_weighted-glance}

- **Descripción**: proporción de predicciones incorrectas en clase positiva
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación multiclase
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la pantalla
{: #quality_wfpr_weighted-display}

![Se muestra el gráfico Índice de falsos positivos ponderados.](images/quality-fpr.png)

## Cómo calcularlo
{: #quality_wfpr_weighted-math}

El índice de falsos positivos ponderados es la aplicación del FPR con datos ponderados.

```
                   número de falsos positivos
FPR =  ______________________________________________________

       (número de falsos positivos + número de negativos verdaderos)
```
