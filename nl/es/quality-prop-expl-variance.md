---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# Proporción de varianza explicada ![etiqueta beta](images/beta.png)
{: #quality_var}

La proporción de varianza explicada es la proporción de varianza explicada y la varianza de destino. La varianza explicada es la diferencia entre la varianza de destino y la varianza de error de predicción.
{: shortdesc}

## Detalles de la proporción de varianza explicada
{: #quality_var-glance}

- **Descripción**: la proporción de varianza explicada es la proporción de varianza explicada y la varianza de destino. La varianza explicada es la diferencia entre la varianza de destino y la varianza de error de predicción.
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: Regresión
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: ninguno

## Interpretación de la pantalla
{: #quality_var-display}

![Se muestra el gráfico Proporción de varianza explicada.](images/xxxx.png)

## Cómo calcularlo
{: #quality_var-math}

La proporción de varianza explicada se calcula realizando el promedio de los números y, a continuación, para cada número, restando el promedio y realizando el cuadrado de los resultados. A continuación calcula los cuadrados

```
                                    suma de cuadrados entre grupos
Proporción de varianza explicada =  ________________________________

                                      total de la suma de cuadrados
```
