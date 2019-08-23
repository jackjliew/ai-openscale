---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R cuadrado
{: #quality_r_squared}

R cuadrado es la proporción de diferencia entre la varianza de destino y la varianza para error de predicción con la varianza de destino. Puede indicar la exactitud con la que los datos que ha utilizado para crear el modelo se ajustan a la regresión.
{: shortdesc}

## Detalles de R cuadrado
{: #quality_r_squared-glance}

- **Descripción**: proporción de diferencia entre la varianza de destino y la varianza para error de predicción con la varianza de destino
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: Regresión
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: ninguno

## Interpretación de la pantalla
{: #quality_r_squared-display}

![Se muestra el gráfico R cuadrado.](images/xxxx.png)

## Cómo calcularlo
{: #quality_r_squared-math}

La métrica R cuadrado se define en la fórmula siguiente.

```
                  variación explicada
R squared =ai-open-scale-ibm-aios-scheduling  | 1 | Servicio de planificación-  _____________________

                    variación total
```
