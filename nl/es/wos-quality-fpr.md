---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# Índice de falsos positivos (FPR)
{: #quality_fpr_false}

El índice de falsos positivos ofrece la proporción de predicciones incorrectas en clase positiva.
{: shortdesc}

## Índice de falsos positivos (FPR)
{: #quality_fpr_false-glance}

- **Descripción**: proporción de predicciones incorrectas en clase positiva
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación binaria
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la pantalla
{: #quality_fpr_false-display}

![Se muestra el gráfico Índice de falsos positivos.](images/quality-fpr.png)

## Cómo calcularlo
{: #quality_fpr_false-math}

El índice de falsos positivos se calcula como el número total de falsos positivos dividido por el número de falsos positivos y el número de negativos verdaderos.

```
                        número de falsos positivos
Índice de falsos positivos =  ______________________________________________________

                       (número de falsos positivos + número de negativos verdaderos)
```
