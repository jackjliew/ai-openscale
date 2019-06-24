---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Explicación de las transacciones
{: #ie-ov}

Para cada despliegue, puede ver los datos de explicabilidad de transacciones específicas.
{: shortdesc}

## Explicación de las transacciones
{: #ie-view}

En el mosaico de despliegue seleccionado, seleccione la pestaña **Explicar una transacción** ( ![Pestaña Explicar una transacción](images/insight-transact-tab.png)) en el navegador y especifique un ID de transacción.

Cada vez que se envían datos al modelo para la puntuación, se establece un ID de transacción en la cabecera HTTP estableciendo el campo `X-Global-Transaction-Id`. Este ID de transacción se almacena en la tabla de carga útil. Para encontrar una explicación del comportamiento del modelo para una puntuación determinada, especifique el ID de transacción asociado con dicha solicitud de puntuación. Tenga en cuenta que este comportamiento se aplica sólo a las transacciones de Watson Machine Learning (WML) y no es aplicable para transacciones que no sean de WML.
{: note}

### Búsqueda de un ID de transacción en {{site.data.keyword.aios_short}}
{: #ie-find}

1.  En el gráfico de tiempo de su despliegue, deslice el marcador por el gráfico y pulse el enlace **Ver detalles** para [visualizar datos para una hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Pulse el botón **Ver transacciones** para [ver la lista de los ID de transacción](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copie uno de los ID de transacción de la lista, péguelo en el recuadro de búsqueda en la página **Explicar una transacción** y pulse Intro.

    La lista de los ID de transacción también tiene la opción para pulsar simplemente el enlace **Explicar** en la columna Acción para cualquier ID de transacción, lo que abrirá esa transacción en la pestaña Explicabilidad.
    {: note}

  Consulte las secciones siguientes para ver ejemplos de explicaciones de distintos tipos de modelos.

  ![ID de transacción de explicabilidad](images/insight-explain-trans-id.png)

## Ejemplo de modelo categórico
{: #ie-class}

Este ejemplo de explicabilidad es para un modelo de clasificación binaria que aprueba o deniega reclamaciones de seguros. Puede ver los factores que han contribuido positiva o negativamente al resultado final de `DENEGADO` en este caso.

La característica *ANTIGÜEDAD DE LA PÓLIZA* con un valor de `< 1 año` ha tenido el máximo impacto en el modelo para la decisión de un resultado DENEGADO. Las otras características que han contribuido a este resultado han sido *FRECUENCIA DE RECLAMACIÓN* (`Alta`) y *EDAD* (`18`), con sólo un impacto leve de *VALOR DE VEHÍCULO* (`50.000 $`).

![Clasificación binaria de la explicabilidad](images/insight-explain-binary.png)

Aunque los gráficos son útiles para mostrar los factores más significativos en la determinación del resultado de una transacción, los modelos de clasificación también pueden incluir explicaciones avanzadas, que se detallan en las secciones `Cambios mínimos para resultado Aprobado` y `Cambios mínimos para este resultado`.

No hay disponibles explicaciones avanzadas para los modelos de regresión, imagen y texto no estructurado.
{: note}

`Cambios mínimos para resultado Aprobado` nos indica que, si los valores de las características cambiaran a los valores de esta sección, la predicción del modelo cambiaría.

De la misma forma, `Cambios mínimos para este resultado` nos indica que, incluso si los valores de las características se cambiaran a los que se listan en esta sección, la predicción del modelo no cambiaría.

Por lo tanto, estos dos valores nos indican el comportamiento del modelo en la proximidad del punto de datos para el que se está generando la explicación.

![Explicabilidad - Clasificación binaria](images/insight-explain-binary2.png)

## Ejemplo de modelo de imagen
{: #ie-image}

Para un ejemplo de explicabilidad de modelo de clasificación de imagen, puede ver qué partes de una imagen han contribuido positivamente al resultado previsto y cuáles han contribuido negativamente. En el ejemplo siguiente, la imagen de la derecha muestra las partes que han afectado positivamente a la predicción y la imagen de la izquierda muestra las partes de la imagen que han tenido un impacto negativo en el resultado.

- Para {{site.data.keyword.pm_full}}, la carga útil de las imágenes alteradas que se envía mediante la pasarela de aprendizaje automático no puede sobrepasar 1 MB. Para evitar problemas de tiempo de espera excedido, las imágenes no deben sobrepasar 125 x 125 píxeles y se deben enviar secuencialmente de forma que se solicite la explicación de la segunda imagen cuando se haya completado la primera.
{: note}

![Explicabilidad - Clasificación de imagen](images/insight-explain-image.png)

## Ejemplo de modelo de texto no estructurado
{: #ie-unstruct}

Finalmente, este ejemplo de explicabilidad muestra un modelo de clasificación que evalúa datos no estructurados. La explicación muestra las palabras clave que han tenido tanto un impacto positivo como un impacto negativo en el modelo de predicción. También muestra la posición de las palabras clave identificadas en el texto original que se ha especificado como entrada del modelo.

![Explicabilidad - Clasificación de imagen](images/insight-explain-text.png)
