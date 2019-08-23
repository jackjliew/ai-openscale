---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Explicación de las transacciones
{: #ie-ov}

Para cada despliegue, puede ver los datos de explicabilidad de transacciones específicas. Las transacciones aparecen sólo cuando hay datos para dar soporte a los supervisores y se basan en los umbrales establecidos, el tiempo planificado de ejecución de los supervisores y la disponibilidad de los datos de carga útil de {{site.data.keyword.pm_full}}.
{: shortdesc}

## Visualización de las explicaciones por ID de transacción
{: #ie-view}

1. Pulse un mosaico de despliegue.
2. Pulse la pestaña **Explicar una transacción** (![Pestaña Explicar una transacción](images/insight-transact-tab.png)) en el navegador.
3. Especifique un ID de transacción.

Cada vez que se envían datos al modelo para la puntuación, se establece un ID de transacción en la cabecera HTTP estableciendo el campo `X-Global-Transaction-Id`. Este ID de transacción se almacena en la tabla de carga útil. Para encontrar una explicación del comportamiento del modelo para una puntuación determinada, especifique el ID de transacción asociado con dicha solicitud de puntuación. Tenga en cuenta que este comportamiento se aplica sólo a las transacciones de {{site.data.keyword.pm_full}} y no es aplicable para transacciones que no sean de WML.
{: note}

## Búsqueda de un ID de transacción en {{site.data.keyword.aios_short}}
{: #ie-find}

1.  En el gráfico de tiempo de su despliegue, deslice el marcador por el gráfico y pulse el enlace **Ver detalles** para [visualizar datos para una hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Pulse el botón **Ver transacciones** para [ver la lista de los ID de transacción](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copie uno de los ID de transacción de la lista, péguelo en el recuadro de búsqueda en la página **Explicar una transacción** y pulse Intro.

    La lista de los ID de transacción también tiene la opción para pulsar simplemente el enlace **Explicar** en la columna Acción para cualquier ID de transacción, lo que abrirá esa transacción en la pestaña Explicabilidad.
    {: note}

  Consulte las secciones siguientes para ver ejemplos de explicaciones de distintos tipos de modelos.

  ![ID de transacción de explicabilidad](images/insight-explain-trans-id.png)

## Búsqueda de explicaciones en los detalles de los gráficos
{: #ie-view-ui}

Puesto que existen explicaciones para las métricas de equidad y desviación, puede pulsar en los gráficos para obtener una vista detallada de los conjuntos de datos y a continuación pulsar el botón **Ver transacciones** para las métricas de equidad o pulsar un mosaico de transacción de desviación para ver las explicaciones de la transacción.

- Para uno de los atributos de equidad, como por ejemplo sexo o edad, pulse el atributo y a continuación el gráfico y pulse el botón **Ver transacciones**.
- Para el supervisor de desviación, pulse **Magnitud de la desviación**, pulse el gráfico y a continuación un mosaico para ver las transacciones asociadas con ese grupo de desviación específico.

## Pasos siguientes
{: #ie-trans-id-next}

- [Explicación de los modelos categóricos](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Explicación de los modelos de imagen](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Explicación de los modelos de texto no estructurado](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Explicaciones contrastativas](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
