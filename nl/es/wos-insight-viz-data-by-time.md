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

# Visualización de los datos correspondientes a una hora específica
{: #it-vdet}

Para ver detalles sobre una estadística de equidad determinada, pulse en el gráfico para una hora específica. Se abre una visualización de los puntos de datos para una característica seleccionada a la hora seleccionada. Siguiendo el ejemplo anterior, en este ejemplo se muestra la característica Edad.
{: shortdesc}

Observe los tres filtros de la parte superior de la página (Característica, Fecha y Hora) que le permiten seleccionar una característica o una hora distinta para revisar los detalles.

![Se muestra un gráfico de series de tiempo con columnas que representan los datos alterados y de carga útil por antigüedad y el número de resultados favorables](images/wos-insight-data-detail.png)

## Interpretación del gráfico
{: #it-intp}

El gráfico muestra varios elementos:

- Puede observar la población que experimenta sesgo (los clientes de entre 18 y 23 años). El gráfico muestra también el porcentaje del resultado esperado para esta población.

- El gráfico muestra el porcentaje del resultado esperado (el 70%) para la población de referencia. Es el promedio del resultado esperado en todas las poblaciones de referencia.

- El gráfico indica la presencia de sesgo, porque el porcentaje de resultados esperados para las poblaciones con una edad comprendida entre 18 y 23
años respecto al porcentaje de resultados esperados para la población de referencia sobrepasa el umbral. En otras palabras, 0,52/0,7 = 0,74, que es inferior al umbral de 0,8.

- El gráfico muestra también la distribución de los valores de referencia y supervisados para cada valor individual del atributo en los datos de la tabla de carga útil que se ha analizado para identificar el sesgo. En otras palabras, si el algoritmo de detección de sesgo ha analizado los últimos 1790 registros de la tabla de carga útil, 120 de esos registros tenían la edad de cliente entre 18 y 23, y el gráfico de barras representa los resultados `Aprobado` y `Denegado` de esa distribución. La distribución de los datos de carga útil se muestra para cada valor individual del atributo de equidad (incluso se muestran los valores de referencia). Esta información se puede utilizar para correlacionar el sesgo con la cantidad de datos que recibe el modelo.

- El gráfico muestra además que la población con edades comprendidas entre los 31 y los 35 años ha recibido el 91% de resultados esperados. Esto significa que es la fuente del sesgo, lo que indica que los datos de ese grupo han causado una desviación en los resultados, y que han causado un aumento en el porcentaje de resultados esperados para la clase de referencia. Esta información se puede utilizar para identificar las partes de los datos de las que se puede reducir la muestra al volver a entrenar el modelo.

- Otro aspecto importante que muestra el gráfico es el nombre de la tabla que contiene los datos que se han identificado para el etiquetado manual. Cada vez que el algoritmo detecta sesgo en un modelo, identifica también los puntos de datos que se pueden enviar para el etiquetado manual por parte de usuarios humanos. A continuación, estos datos etiquetados manualmente se pueden utilizar junto con los datos de entrenamiento originales para volver a entrenar el modelo. Es probable que este modelo reentrenado no esté sesgado. La tabla de etiquetado manual está presente en la base de datos asociada con la instancia de {{site.data.keyword.aios_short}}.
