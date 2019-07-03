---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Configuración de la supervisión de exactitud o calidad
{: #acc-monitor}

El supervisor de calidad (denominado anteriormente supervisor de exactitud) le permite saber la exactitud con la que el modelo predice los resultados.
{: shortdesc}

## Pasos de configuración
{: #acc-config}

En la pestaña **Exactitud**, en la página **¿Qué es la exactitud?**, pulse **Empezar** para iniciar el proceso de configuración.

![Página ¿Qué es la exactitud?](images/accuracy-what-is.png)

Configure los valores siguientes en las páginas sucesivas de la pestaña de configuración de exactitud:

-  Establezca el umbral de alerta de exactitud. Seleccione un valor que represente un nivel de exactitud aceptable.

    La exactitud es un valor sintetizado de las métricas de ciencia de datos relevantes asociadas con cada tipo de modelo determinado. La puntuación es una medida normalizada que le permite comparar fácilmente la exactitud entre distintos tipos de modelo. En situaciones típicas, una puntuación de exactitud de 80 es suficiente.
    {: note}

-  Establezca el tamaño mínimo y máximo de la muestra. El tamaño mínimo evita que se mida la exactitud hasta que haya disponible un número mínimo de registros en el conjunto de datos de evaluación; esto garantiza que el tamaño de la muestra no es demasiado pequeño y pueda causar desviaciones en los resultados. El tamaño máximo de la muestra ayuda a gestionar mejor el tiempo y el esfuerzo necesarios para evaluar el conjunto de datos; si se sobrepasa este tamaño, sólo se evaluarán los registros más recientes.


Aparece un resumen de sus selecciones para su revisión. Si desea cambiar algo, pulse el enlace **Editar** para esa sección. De lo contrario, pulse **Guardar** para completar la configuración.

### Pasos siguientes
{: #acc-next}

En la página **Configurar supervisores**, puede seleccionar otra categoría de supervisión.
