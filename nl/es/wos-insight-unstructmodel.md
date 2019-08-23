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

# Explicación de los modelos de texto no estructurado
{: #ie-unstruct}

{{site.data.keyword.aios_short}} da soporte a la explicabilidad para datos de texto no estructurados.
{: shortdesc}

## Trabajar con modelos de texto no estructurados
{: #ie-unstruct-steps}

1. Configure el entorno.
   2. Instale los paquetes de {{site.data.keyword.aios_short}} y {{site.data.keyword.pm_full}}.
   3. Configure sus credenciales.
   4. Instale las bibliotecas necesarias para crear los modelos y realizar el análisis. Incluyen las bibliotecas siguientes:
      - `pandas`
      - `pyspark` (si no se utiliza {{site.data.keyword.DSX}})

1. Cree y despliegue el modelo basado en imagen.
   2. Cargue los datos de entrenamiento en un marco pandas.
   2. Entrene el modelo sobre los datos.
   3. Publique el modelo.
   4. Despliegue y puntúe el modelo.

7. Configure {{site.data.keyword.aios_short}} asignando `APIClient`, suscribiendo el activo y puntuando el modelo.
8. Configure la explicabilidad.
   9. Habilite la explicabilidad.
   10. Obtenga explicaciones de las transacciones.

## Explicación de las transacciones de texto no estructurado
{: #ie-unstruct-xplan}

El ejemplo siguiente de explicabilidad muestra un modelo de clasificación que evalúa el texto no estructurado. La explicación muestra las palabras clave que han tenido tanto un impacto positivo como un impacto negativo en el modelo de predicción. También muestra la posición de las palabras clave identificadas en el texto original que se ha especificado como entrada del modelo.

![Se muestra el gráfico de clasificación de imágenes de explicabilidad. Muestra los niveles de confianza del texto no estructurado](images/insight-explain-text.png)

## Ejemplo de modelo de texto no estructurado
{: #ie-unstruct-ntbkssample}

Utilice el siguiente cuaderno para ver ejemplos de código detallados y desarrollar sus propios despliegues de {{site.data.keyword.aios_short}}:

- [Guía de aprendizaje para generar una explicación para un modelo basado en texto](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

