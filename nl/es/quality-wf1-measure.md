---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted F1-Measure

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

# Medida F1 ponderada ![etiqueta beta](images/beta.png)
{: #quality_wght_f1-measure}

La medida F1 ponderada proporciona el promedio ponderado de la medida F1 con ponderaciones iguales a la probabilidad de clase.
{: shortdesc}

## Detalles de la medida F1 ponderada
{: #quality_wght_f1-measure-glance}

- **Descripción**: medida ponderada de la medida F1 con ponderaciones iguales a la probabilidad de clase
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación multiclase
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la pantalla
{: #quality_wght_f1-measure-display}

![Se muestra el gráfico Medida F1 ponderada.](images/quality-f1-meas.png)

## Cómo calcularlo
{: #quality_wght_f1-measure-math}

La medida F1 ponderada es el resultado de utilizar los datos ponderados.

```
          (precisión * exhaustividad)
F1 = 2 *  ____________________

          (precisión + exhaustividad)
```
