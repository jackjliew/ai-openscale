---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, weighted recal

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

# Exhaustividad ponderada ![etiqueta beta](images/beta.png)
{: #quality_weighted_recall}

La exhaustividad ponderada proporciona la media ponderada de exhaustividad con ponderaciones iguales a la probabilidad de clase.
{: shortdesc}

## Detalles de la exhaustividad ponderada
{: #quality_weighted_recall-glance}

- **Descripción**: media ponderada de exhaustividad con ponderaciones iguales a la probabilidad de clase
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación multiclase
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la pantalla
{: #quality_weighted_recall-display}

![Se muestra el gráfico Exhaustividad ponderada](images/quality-recall.png)

## Cómo calcularlo
{: #quality_weighted_recall-math}

La exhaustividad ponderada (wR) se define como el número de verdaderos positivos (Tp) sobre el número de verdaderos positivos más el número de falsos negativos (Fn) utilizados con los datos ponderados. 

```
                  número de verdaderos positivos
Exhaustividad =   ______________________________________________________

                  (número de verdaderos positivos + número de falsos negativos)
```
