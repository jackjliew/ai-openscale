---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# Área bajo ROC ![etiqueta beta](images/beta.png)
{: #quality_roc}

El Área bajo la curva de característica operativa de receptor proporciona el área bajo exhaustividad y la curva del índice de falsos positivos. Calcula la sensibilidad respecto al índice de repercusión.
{: shortdesc}

## Detalles del área bajo ROC
{: #quality_roc-glance}

- **Descripción**: área bajo exhaustividad y curva de índice de falsos positivos.
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación binaria
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la pantalla
{: #quality_roc-display}

![Se muestra el gráfico Área bajo ROC.](images/quality-area-under-roc.png)

## Cómo calcularlo
{: #quality_roc-math}

El Área bajo ROC se traza paramétricamente como el `Índice de verdaderos positivos` en relación con el `Índice de falsos positivos` con respecto a un umbral `T`.

