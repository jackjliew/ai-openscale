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

# Exhaustividad
{: #quality_recall}

La exhaustividad ofrece la proporción de predicciones correctas en clase positiva.
{: shortdesc}

## Detalles de la exhaustividad
{: #quality_recall-glance}

- **Descripción**: proporción de predicciones correctas en clase positiva
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación binaria
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la visualización de la métrica de exhaustividad
{: #quality_recall-display}

![Se muestra el gráfico Exhaustividad.](images/quality-recall.png)

### Puntuación de equidad
{: #quality_recall-display-fairness-score}

Para la métrica de exhaustividad, se muestra la siguiente puntuación de equidad. 

![Se muestra el porcentaje de puntuación de Exhaustividad.](images/wos-quality-recall-score.png)

### Planificación
{: #quality_recall-display-schedule}

El panel **Planificación** muestra las horas de la **Última evaluación** y la **Próxima evaluación**. Las métricas de calidad se evalúan cada hora. Puede forzar la evaluación pulsando **Comprobar calidad ahora**. También puede añadir opiniones pulsando **Añadir datos de opiniones**.

![Se muestra el panel de planificación, que muestra la hora de la última evaluación y de la siguiente evaluación](images/wos-quality-schedule.png)


### Recomendación
{: #quality_recall-display-recommendations}

Para ayudarle a interpretar el gráfico, el panel **Recomendación** muestra las tendencias que indican mejora o deterioro de la efectividad del modelo.

![Se muestra la página de recomendación.](images/wos-quality-positive-recommendation.png)




## Cómo calcularlo
{: #quality_recall-math}

La exhaustividad (R) se define como el número de verdaderos positivos (Tp) sobre el número de verdaderos positivos más el número de falsos negativos (Fn).

```
                       número de verdaderos positivos
Exhaustividad =   ______________________________________________________

           (número de verdaderos positivos + número de falsos negativos)
```
