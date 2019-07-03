---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# Error absoluto promedio ![etiqueta beta](images/beta.png)
{: #quality_abserror}

El error absoluto promedio proporciona el promedio de la diferencia absoluta entre la predicción del modelo y el valor objetivo.
{: shortdesc}

## Detalles del error absoluto promedio
{: #quality_abserror-glance}

- **Descripción**: promedio de la diferencia absoluta entre la predicción del modelo y el valor de destino
- **Umbrales predeterminados**: límite superior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: Regresión
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: ninguno

## Interpretación de la pantalla
{: #quality_abserror-display}

![Se muestra el gráfico Error absoluto promedio.](images/xxxx.png)

## Cómo calcularlo
{: #quality_abserror-math}

El error absoluto promedio se calcula sumando todos los errores absolutos y dividiéndolos por el número de errores.

```
                           SUM  | Yi - Xi |
Error absoluto promedio =  ____________________

                          número de errores
```
