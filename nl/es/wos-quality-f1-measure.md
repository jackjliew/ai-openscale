---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, F1-Measure

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

# Medida F1
{: #quality_f1-measr}

La medida F1 proporciona el promedio absoluto de precisión y exhaustividad.
{: shortdesc}

## Detalles de la medida F1
{: #quality_f1-measr-glance}

- **Descripción**: media armónica de precisión y exhaustividad
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación binaria
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la pantalla
{: #quality_f1-measr-display}

![Se muestra el gráfico Medida F1.](images/quality-f1-meas.png)

## Cómo calcularlo
{: #quality_f1-measr-math}

La medida F1 es el promedio armónico ponderado, o media, de precisión y exhaustividad.

```
          (precisión * exhaustividad)
F1 = 2 *  ____________________

          (precisión + exhaustividad)
```

