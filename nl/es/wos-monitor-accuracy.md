---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# Configuración del supervisor de calidad (exactitud)
{: #acc-monitor}

El supervisor de calidad (anteriormente denominado supervisor de exactitud) le permite saber la exactitud con la que el modelo predice los resultados.
{: shortdesc}

## Pasos de configuración
{: #acc-config}

En la pestaña **Calidad**, en la página **¿Qué es el supervisor de calidad?**, pulse **Empezar** para iniciar el proceso de configuración.

![Se muestra la página ¿Qué es el supervisor de calidad? y explica que el supervisor de calidad evalúa la exactitud con la que el modelo predice resultados precisos](images/wos-quality-what-is.png)

Configure los valores siguientes en las páginas sucesivas de la pestaña de configuración de exactitud:

-  Establezca el umbral de alerta de exactitud. Seleccione un valor que represente un nivel de exactitud aceptable. Por ejemplo, si utiliza el **Modelo de riesgo crediticio alemán** para la guía de aprendizaje interactiva, establezca la alerta en **90%**. 
    La exactitud es un valor sintetizado de las métricas de ciencia de datos relevantes asociadas con cada tipo de modelo determinado. La puntuación es una medida normalizada que le permite comparar fácilmente la exactitud entre distintos tipos de modelo. En situaciones típicas, una puntuación de exactitud de 80 es suficiente. Para la guía de aprendizaje, para generar más datos, recomendamos 90.
    {: note}

-  Establezca el tamaño mínimo y máximo de la muestra. El tamaño mínimo evita que se mida la exactitud hasta que haya disponible un número mínimo de registros en el conjunto de datos de evaluación; esto garantiza que el tamaño de la muestra no es demasiado pequeño y pueda causar desviaciones en los resultados. El tamaño máximo de la muestra ayuda a gestionar mejor el tiempo y el esfuerzo necesarios para evaluar el conjunto de datos; si se sobrepasa este tamaño, sólo se evaluarán los registros más recientes. Por ejemplo, si utiliza el **Modelo de riesgo crediticio alemán** para la guía de aprendizaje interactiva, establezca el tamaño mínimo de ejemplo en **100** y el tamaño máximo de ejemplo en **10000**.


Aparece un resumen de sus selecciones para su revisión. Si desea cambiar algo, pulse el enlace **Editar** para esa sección. De lo contrario, pulse **Guardar** para completar la configuración.

### Pasos siguientes
{: #acc-next}

Para continuar configurando supervisores, pulse la pestaña **Equidad** y pulse **Empezar**. Para obtener más información, consulte [Configuración del supervisor de equidad](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
