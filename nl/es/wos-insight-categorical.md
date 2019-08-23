---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Explicación de un modelo categórico
{: #ie-class}

Este ejemplo de explicabilidad es para un modelo de clasificación binaria que aprueba o deniega reclamaciones de seguros. Puede ver los factores que han contribuido positiva o negativamente al resultado final de `DENEGADO` en este caso.
{: shortdesc}

La característica *ANTIGÜEDAD DE LA PÓLIZA* con un valor de `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear` ha tenido el máximo impacto en el modelo para la decisión de un resultado DENEGADO. Las otras características que han contribuido a este resultado han sido *FRECUENCIA DE RECLAMACIÓN* (`Alta`) y *EDAD* (`18`), con sólo un impacto leve de *VALOR DE VEHÍCULO* (`50.000 $`).

![Se muestra la clasificación binaria de explicabilidad con detalles sobre las reclamaciones denegadas y aprobadas](images/insight-explain-binary.png)

Aunque los gráficos son útiles para mostrar los factores más significativos en la determinación del resultado de una transacción, los modelos de clasificación también pueden incluir explicaciones avanzadas, que se detallan en las secciones `Cambios mínimos para resultado Aprobado` y `Cambios mínimos para este resultado`.

No hay disponibles explicaciones avanzadas para los modelos de regresión, imagen y texto no estructurado.
{: note}

`Cambios mínimos para resultado Aprobado` nos indica que, si los valores de las características cambiaran a los valores de esta sección, la predicción del modelo cambiaría.

De la misma forma, `Cambios mínimos para este resultado` nos indica que, incluso si los valores de las características se cambiaran a los que se listan en esta sección, la predicción del modelo no cambiaría.

Por lo tanto, estos dos valores nos indican el comportamiento del modelo en la proximidad del punto de datos para el que se está generando la explicación.

![Detalles de la clasificación binaria de explicabilidad con los cambios mínimos que serían necesarios para cambiar los resultados](images/insight-explain-binary2.png)
