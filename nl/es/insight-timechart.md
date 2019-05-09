---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Supervisión de la equidad, solicitudes promedio por minuto y exactitud
{: #it-ov}

Los datos de supervisión de los despliegues individuales se visualizan en un gráfico de series de tiempo. El gráfico realiza un seguimiento de Supervisión de la equidad, solicitudes promedio por minuto y exactitud durante los últimos 7 días.
{: shortdesc}

## Visualización de los datos para un despliegue
{: #it-vdep}

Seleccione un despliegue desde el panel de control para ver los datos de supervisión para ese despliegue. La parte superior del gráfico de datos de supervisión muestra información sobre el modelo desplegado, incluido cuándo se evaluó la equidad y exactitud del modelo por última vez, y cuándo se evaluará la próxima vez.

![Gráficos de series de tiempo](images/insight-time-chart.png)

Puesto que las comprobaciones de algoritmo se ejecutan sólo cada hora, hay también algunos botones que se proporcionan para permitirle comprobar la equidad y la exactitud. Si no ha proporcionado suficientes registros de carga útil (equidad) o registros de opiniones (exactitud), verá el mensaje siguiente, por ejemplo:

![Botón Exactitud](images/accuracy-button.png)

A continuación, mueva el marcador por el gráfico para ver las estadísticas de una hora individual. En este ejemplo, la hora seleccionada es 1:00 PM CST del 18 de septiembre, que revela las estadísticas siguientes:

![Detalles del gráfico de series de tiempo](images/insight-time-detail.png)

- ***Equidad***: dos de las tres características de Equidad, Valor de vehículo y Código de área, han cumplidos sus umbrales establecidos para la aprobación. La tercera característica de Equidad, Edad, se ha marcado como sesgada. También puede ver el número de resultados esperados (en este caso los porcentajes de Aprobados vs. Denegados) para una población individual en las características cuya equidad se supervisa.
- ***Exactitud***: el promedio de la métrica de Exactitud es del 78%.
- ***Prom. req/mín***: de promedio, se han procesado 300 registros por minuto entre las 1:00 y 2:00 PM CST. El rendimiento se calcula cada minuto, y se informa en el gráfico de su valor promedio en el curso de la hora.

## Visualización de los datos correspondientes a una hora específica
{: #it-vdet}

Para ver la información detallada de una estadística de Equidad determinada, pulse el enlace **Ver detalles** para la hora seleccionada.

Se abre una visualización de los puntos de datos para una característica seleccionada a la hora seleccionada. A continuación se muestra el ejemplo anterior de la característica Edad, etiquetada como sesgada.

Observe los tres filtros de la parte superior de la página (Característica, Fecha y Hora) que le permiten seleccionar una característica o una hora distinta para revisar los detalles.

![Gráfico de series de tiempo](images/insight-data-detail.png)

### Interpretación del gráfico
{: #it-intp}

El gráfico muestra varios elementos:

- Puede observar la población que experimenta sesgo (los clientes de entre 18 y 23 años). El gráfico también muestra el porcentaje del resultado esperado (el 52%) para esta población.

- El gráfico muestra el porcentaje del resultado esperado (el 70%) para la población de referencia. Es el promedio del resultado esperado en todas las poblaciones de referencia.

- El gráfico indica la presencia de sesgo, porque el porcentaje de resultados esperados para las poblaciones con una edad comprendida entre 18 y 23 años respecto al porcentaje de resultados esperados para la población de referencia está por debajo del umbral. En otras palabras, 0,52/0,7 = 0,74, que es inferior al umbral de 0,8.

- El gráfico muestra también la distribución de los valores de referencia y supervisados para cada valor individual del atributo en los datos de la tabla de carga útil que se ha analizado para identificar el sesgo. En otras palabras, si el algoritmo de detección de sesgo ha analizado los últimos 1790 registros de la tabla de carga útil, 120 de esos registros tenían la edad de cliente entre 18 y 23, y el gráfico de barras representa los resultados `Aprobado` y `Denegado` de esa distribución. La distribución de los datos de carga útil se muestra para cada valor individual del atributo de equidad (incluso se muestran los valores de referencia). Esta información se puede utilizar para correlacionar el sesgo con la cantidad de datos que recibe el modelo.

- El gráfico muestra además que la población con edades comprendidas entre los 31 y los 35 años ha recibido el 91% de resultados esperados. Esto significa que es la fuente del sesgo, lo que indica que los datos de ese grupo han causado una desviación en los resultados, y que han causado un aumento en el porcentaje de resultados esperados para la clase de referencia. Esta información se puede utilizar para identificar las partes de los datos de las que se puede reducir la muestra al volver a entrenar el modelo.

- Otro aspecto importante que muestra el gráfico es el nombre de la tabla que contiene los datos que se han identificado para el etiquetado manual. Cada vez que el algoritmo detecta sesgo en un modelo, identifica también los puntos de datos que se pueden enviar para el etiquetado manual por parte de usuarios humanos. A continuación, estos datos etiquetados manualmente se pueden utilizar junto con los datos de entrenamiento originales para volver a entrenar el modelo. Es probable que este modelo reentrenado no esté sesgado. La tabla de etiquetado manual está presente en la base de datos asociada con la instancia de {{site.data.keyword.aios_short}}.

## Datos de tiempo de ejecución y entrenamiento
{: #it-rtsw}

El conmutador de datos de tiempo de ejecución y entrenamiento le permite alternar las diferencias entre su modelo entrenado y los datos recopilados en tiempo de ejecución que desencadenan un aviso de sesgo.

![Conmutador de entrenamiento de tiempo de ejecución](images/runtime_train_data.png)

## Ver transacciones
{: #it-tra}

Esta opción le permite ver las transacciones individuales que han contribuido al sesgo al pulsar el botón **Ver transacciones**.

![Ver transacciones](images/view_transactions.png)

Aparece una lista de transacciones donde el despliegue ha tenido un comportamiento sesgado. Pulse el enlace **Explicar** para cualquiera de los ID de transacción para obtener información detallada sobre esa transacción en la pestaña Explicabilidad. Para obtener más información, consulte [Supervisión de la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

Seleccione la vista **Todas las transacciones** para ver todas las transacciones de la característica seleccionada (en este ejemplo "EDAD") y el periodo seleccionado (en este ejemplo "15 de septiembre de 2018 a las 1:00 PM"):

![Lista de todas las transacciones](images/transaction_list1.png)

Seleccione la vista **Transacciones sesgadas** para ver sólo el subconjunto de transacciones que ha recibido los resultados sesgados. Cada transacción sesgada se compara con una transacción similar pero ligeramente modificada (perturbada) que muestra cómo el cambio del valor de la característica supervisada (EDAD) producirá un resultado favorable para la transacción sesgada:

![Lista de transacciones sesgadas](images/transaction_list2.png)

## Modelo de producción y modelo sin sesgo
{: #it-prdb}

Puede utilizar estas dos pestañas para alternar entre su modelo de producción y un modelo sin sesgo creado por {{site.data.keyword.aios_short}}. Consulte [Cómo funciona la eliminación del sesgo](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) para obtener más detalles.

![Alternar entrenamiento de tiempo de ejecución](images/bias-debias.png)

Si selecciona la pestaña **Modelo sin sesgo**, se muestran los cambios en el modelo sin sesgo, en comparación con el modelo en producción. En este ejemplo, la Equidad del modelo ha aumentado del 74% al 93%, con una reducción de la Exactitud de sólo el 1%. El gráfico también refleja el estado de resultados mejorados para grupos con edades comprendidas entre 18 y 23 años.

![Alternar entrenamiento de tiempo de ejecución](images/insight-data-detail2.png)

### Opciones para la eliminación del sesgo
{: #it-dbo}

- *Eliminación pasiva del sesgo*: cuando {{site.data.keyword.aios_short}} comprueba si hay sesgo, también elimina el sesgo de los datos, analizando el comportamiento del modelo e identificando los datos donde el modelo actúa de forma sesgada.

  A continuación, {{site.data.keyword.aios_short}} crea un modelo de aprendizaje automático para predecir si es probable que el modelo actúe de forma sesgada en un nuevo punto de datos determinado. {{site.data.keyword.aios_short}} analiza los datos que recibe el modelo cada hora y busca los puntos de datos donde {{site.data.keyword.aios_short}} cree que el modelo actúa de forma sesgada. Para estos puntos de datos, el atributo de equidad se perturba de minoría a mayoría, y los datos perturbados se envían al modelo original para la predicción. Esta predicción del modelo original se utiliza como la salida sin sesgo.

  {{site.data.keyword.aios_short}} realiza esta eliminación de sesgo cada hora, en todos los datos que ha recibido el modelo durante la última hora. También calcula la equidad de la salida sin sesgo y la muestra en la pestaña **Modelo sin sesgo**.

- *Eliminación activa del sesgo*: en la eliminación activa del sesgo, puede utilizar un punto final de API REST de eliminación de sesgo de su aplicación. Este punto final de API REST llamará inmediatamente a su modelo y comprobará su comportamiento.

  Si {{site.data.keyword.aios_short}} cree que el modelo actúa de forma sesgada, llevará a cabo la perturbación de datos mencionada anteriormente, y los devolverá al modelo original. La salida del modelo original en los datos perturbados se devolverá como la predicción no sesgada. Si {{site.data.keyword.aios_short}} determina que el modelo original no actúa de forma sesgada, {{site.data.keyword.aios_short}} devolverá la predicción del modelo original como la predicción no sesgada. Por lo tanto, utilizando este punto final de API REST, puede asegurarse de que la aplicación no toma decisiones en función de la salida sesgada de los modelos.

Seleccione el enlace **Punto final de puntuación sin sesgo** para buscar el punto final de API REST sin sesgo

![Eliminar sesgo de punto final de API](images/insight-debias-api.png)
