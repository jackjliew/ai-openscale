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

# Raíz del error cuadrático promedio
{: #supqualdets_squ_errors_mean}

La vista Raíz del error cuadrático promedio (RMSE) muestra la diferencia entre los valores previstos y los valores observados del modelo.
{: shortdesc}

## Detalles de raíz del error cuadrático promedio
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Descripción**: raíz cuadrada de media de cuadrado de la diferencia entre la predicción del modelo y el valor de destino
- **Umbrales predeterminados**: límite superior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: Regresión
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: ninguno

## Interpretación de la pantalla
{: #supqualdets_squ_errors_mean-display}

![Se muestra el gráfico Raíz del error cuadrático promedio.](images/xxxx.png)

## Cómo calcularlo
{: #supqualdets_squ_errors_mean-math}

La raíz del error cuadrático promedio es igual a la raíz cuadrada del promedio de (previsiones menos valores observados) al cuadrado.

```
          ___________________________________________________________
RMSE  =  √(previsiones - valores observados)*(previsiones - valores observados)
```
