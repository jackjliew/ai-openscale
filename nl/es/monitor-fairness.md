---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor

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

# Equidad
{: #mf-monitor}

La equidad supervisa si el despliegue está sesgado, para ayudar a garantizar resultados equitativos entre las distintas poblaciones.
{: shortdesc}

## Información sobre la equidad
{: #mf-understand}

{{site.data.keyword.aios_short}} comprueba si su modelo desplegado está sesgado en tiempo de ejecución. Para detectar sesgos en un modelo desplegado,
debe definir atributos de equidad, como Edad o Sexo, tal como se detalla en [Configuración del supervisor de equidad](#mf-config) más abajo.

Es obligatorio especificar el esquema de salida para un modelo o función en Watson {{site.data.keyword.pm_short}}, a fin que la comprobación de sesgo esté habilitada en {{site.data.keyword.aios_short}}. El esquema de salida se puede especificar utilizando la propiedad `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` en la parte de metadatos de la API `store_model`. Para obtener más información, consulte la [documentación del cliente de WML ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wml-api-pyclient-dev.mybluemix.net/#repository){: new_window}.

### Cómo funciona
{: #mf-works}

Antes de configurar el supervisor de equidad debe comprender algunos conceptos clave imprescindibles:

- *Atributos de equidad*: son atributos del modelo para los que es probable que el modelo muestre un sesgo. Como ejemplo, para el atributo de equidad **`Sexo`**, el modelo podría estar sesgado para valores de sexo específicos (`Mujer`, `Transexual`, etc.) Otro ejemplo de atributo de equidad es **`Edad`**, donde el modelo podría estar sesgado para las personas de un grupo de edad, por ejemplo `de 18 a 25`.

- *Valor de referencia/supervisado*: los valores de los atributos de equidad se dividen en dos categorías distintas, Referencia y Supervisado. Los valores supervisados son aquellos para los que es probable que haya una discriminación. En el caso de un atributo de equidad como **`Sexo`**, los valores supervisados podrían ser `Mujer` y `Transexual`. Para un atributo de equidad numérico, por ejemplo **`Edad`**, los valores supervisados podrían ser `[18-25]`. Todos los demás valores de un atributo de equidad determinado se considerarán valores de referencia, por ejemplo `Sexo=Hombre` o `Edad=[26,100]`.

- *Resultado favorable/desfavorable*: la salida del modelo se categoriza como Favorable o Desfavorable. Como ejemplo, si el modelo predice si una persona debe obtener o no un préstamo, la columna Favorable podría ser `Préstamo otorgado` o `Préstamo otorgado parcialmente`, mientras que el resultado Desfavorable podría ser `Préstamo denegado`. Por lo tanto, el resultado Favorable es uno que se considera positivo, mientras que el resultado Desfavorable se considera negativo.

El algoritmo de {{site.data.keyword.aios_short}} calcula el sesgo cada hora, utilizando los últimos `N` registros presentes en la tabla de registro de carga útil; el valor de `N` se especifica al configurar la equidad. El algoritmo perturba estos últimos `N` registros para generar datos adicionales.

La perturbación se realiza cambiando el valor del atributo de equidad de Referencia a Supervisado, o viceversa. A continuación, los datos perturbados se envían al modelo para evaluar su comportamiento. El algoritmo considera los últimos `N` registros de la tabla de carga útil, y el comportamiento del modelo en los datos perturbados, para decidir si el modelo actúa de manera sesgada.

Se considera que un modelo está sesgado si, en este conjunto de datos combinado, el porcentaje de resultados favorables de la clase supervisada es inferior al porcentaje de resultados favorables para la clase de referencia, por algún valor de umbral. Este valor de umbral se especificará al configurar la equidad.

Los valores de equidad pueden ser superiores al 100%. Esto significa que el grupo supervisado ha recibido más resultados favorables que el grupo de referencia. Además, si no se envía ninguna solicitud de puntuación nueva, el valor de equidad se mantendrá constante.
{: note}

### Visualización del sesgo ![etiqueta beta](images/beta.png)
{: #mf-monitor-bias-viz}

Cuando se detecta un sesgo potencial, {{site.data.keyword.aios_short}} realiza varias funciones para confirmar si el sesgo es real. {{site.data.keyword.aios_short}} altera los datos invirtiendo el valor supervisado y el valor de referencia y luego ejecutando este nuevo registro con el modelo. A continuación, muestra la salida resultante como salida sin sesgo. {{site.data.keyword.aios_short}} también entrena un modelo sin sesgo duplicado que a continuación utiliza para detectar cuándo un modelo realizará una predicción sesgada. Los resultados de estas determinaciones están disponibles en la visualización del sesgo, que incluye las vistas siguientes: 

- **Carga útil + Alterados**: incluye la solicitud de puntuación recibida para la hora seleccionada más registros adicionales de las horas anteriores si no se cumple el número mínimo de registros necesarios para la evaluación. Incluye registros alterados/sintetizados adicionales utilizados para probar la respuesta del modelo cuando el valor de la característica supervisada cambia.

   Tome nota de los siguientes detalles de carga útil y alterados:

   - Número de registros que se leen durante esta hora de la tabla de carga útil
   - Registros adicionales que se leen de las horas anteriores (por ejemplo, si el valor `min_records` en la configuración de equidad se establece en 1000, y entre las 2 pm y las 3 pm solo se añaden 10 registros, para cumplir el requisito mínimo el sistema leería 990 registros adicionales de las horas anteriores).
   - Registros alterados por atributo de equidad
   - Indicación de fecha y hora del registro de mayor antigüedad del periodo de tiempo para el que se debe calcular el sesgo
   - Indicación de fecha y hora del registro más nuevo o último del periodo de tiempo para el que se debe calcular el sesgo

  ![Ejemplo de carga útil más alterados](images/payload&perturbed.png)



- **Carga útil**: las solicitudes de puntuación reales recibidas por el modelo durante la hora seleccionada.

   Tome nota de los siguientes detalles de carga útil:
   
   - Número de registros que se leen o en los que se realiza la operación sin sesgo desde la tabla de carga útil
   - Indicación de fecha y hora del registro de mayor antigüedad del periodo de tiempo para el que se debe calcular el sesgo
   - Indicación de fecha y hora del registro más nuevo o último del periodo de tiempo para el que se debe calcular el sesgo


  ![Ejemplo de datos de carga útil](images/payload.png)

- **Entrenamiento**: los registros de datos de entrenamiento utilizados para entrenar el modelo.

   Tome nota de los siguientes detalles de entrenamiento:
   
   - Número de registros de datos de entrenamiento. Los datos de entrenamiento se leen una vez, y la distribución se almacena en la variable `subscription/fairness_configuration`. Al calcular la distribución, deberíamos encontrar también el número de registros de datos de entrenamiento y almacenarlo en la misma distribución. Además, cuando se cambian los datos de formación, lo que indica que se ejecuta de nuevo el mandato `POST /data_distribution`, este valor se actualiza en la variable `fairness_configuration/training_data_distribution`. Al enviar la métrica, también deberíamos enviar este valor.
   - La hora a la que se procesan por última vez los datos de entrenamiento (primera vez y actualizaciones subsiguientes)

  ![Ejemplo de datos de entrenamiento](images/training.png)
   

   
- **Sin sesgo**: la salida del algoritmo sin sesgo tras procesar el tiempo de ejecución y los datos alterados.

   Tome nota de los siguientes detalles sin sesgo:
   
   - Número de registros que se leen/en los que se realiza la operación sin sesgo desde la tabla de carga útil
   - Registros adicionales que se leen para realizar sesgo, y por lo tanto también sin sesgo. El mismo número que en la selección `Carga útil + Alterados`
   - Registros alterados por atributo de equidad
   - Indicación de fecha y hora del registro de mayor antigüedad del periodo de tiempo para el que se debe calcular el sesgo
   - Indicación de fecha y hora del registro más nuevo o último del periodo de tiempo para el que se debe calcular el sesgo

  ![Ejemplo de datos sin sesgo](images/debiased.png)
  
### Ejemplo
{: #mf-ex1}

Considere un punto de datos donde, para `Sexo=Hombre` (Valor de referencia), el modelo predice un resultado favorable, pero cuando se perturba el registro cambiando `Sexo` a `Mujer` (valor supervisado), mientras se mantienen sin cambios todos los demás valores de características, el modelo predice un resultado desfavorable. En general se dice que un modelo muestra sesgo si hay puntos de datos suficientes (en los últimos `N` registros de la tabla de carga útil, más los datos perturbados) donde el modelo actúa de manera sesgada.

### Modelos soportados
{: #mf-supmo}

 {{site.data.keyword.aios_short}} da soporte a la detección de sesgo sólo para aquellos modelos y funciones Python que esperan alguna clase de datos estructurados en su vector de característica.

## Configuración del supervisor de equidad
{: #mf-config}

1.  En la página *¿Qué es la equidad?*, pulse **Siguiente** para iniciar el proceso de configuración.

    ![Página ¿Qué es la equidad?](images/fair-what-is.png)

1.  En la página *Seleccionar las características que desea supervisar*, busque y seleccione los atributos de equidad que desee utilizar y pulse **Siguiente**.

    Sólo se da soporte a las características de un tipo de datos de equidad categórico, numérico (entero), flotante o doble. No se da soporte a características con otros tipos de datos.
    {: note}

    En este ejemplo se han seleccionado las características `Edad`, `Sexo` y `Grupo étnico`.

    ![Página Seleccionar características para supervisar con selecciones](images/fair-select-feature.png)

    Pulse **Siguiente** para continuar.

1.  Cada característica tiene requisitos específicos para configurar. En este ejemplo, define los rangos de **`Edad`** para un grupo de referencia y un grupo supervisado especificando de forma manual los valores directamente en cada grupo.

    En este ejemplo, para el atributo de equidad de **`Edad`**, si cree que es probable que el modelo esté sesgado para las personas cuya edad esté comprendida entre los 18 y los 25 años, el valor de grupo supervisado será `[18-25]` y el valor de grupo de referencia será `[26-100]`. En caso del atributo de equidad **`Sexo`**, el valor de grupo de referencia podría ser `Hombre`, mientras que los valores de grupo supervisado podrían ser `Mujer` y `Transexual`.

    ![Configurar valores de edad](images/fair-config-age.png)

    Pulse **Siguiente** para continuar

1.  Establezca el límite de umbral para equidad, para **`Edad`**.

    Se utiliza un umbral de equidad para especificar una diferencia aceptable entre el porcentaje de resultados favorables para el grupo supervisado en comparación con el porcentaje de resultados favorables para el grupo de referencia.

    Considere un modelo que predice quién debe obtener un préstamo (`resultado favorable=préstamo otorgado`) y quién no (`resultado desfavorable=préstamo denegado`). Además, el valor supervisado de edad es `[18,25]` y el valor de referencia es `[26,100]`. Cuando se ejecuta el algoritmo de detección de sesgo, este encuentra que el porcentaje de resultados favorables para las personas del grupo de edad `[18,25]` en los últimos `N` registros más los datos perturbados es del `50%`, mientras que el porcentaje de resultados favorables para las personas del grupo de edad `[26,100]` es del `70%`, la equidad se calcula como 50*100/70 = 71,42.

    Si el umbral de equidad está establecido en el 80%, el algoritmo marcará el modelo como sesgado, ya que la equidad que se ha calculado es inferior al umbral. Sin embargo, si el umbral se establece en el 70%, no notificará el modelo como sesgado.

    ![Configurar valores de edad](images/fair-config-age-limit.png)

    Pulse **Siguiente** cuando haya seleccionado un umbral de equidad.

1.  Configure las características `Sexo` y `Grupo étnico` de la misma forma:

     ![Configurar valores de sexo](images/fair-config-gender.png)

     ![Configurar valores de grupo étnico](images/fair-config-ethnic.png)

     **Nota**: Los valores que especifica en estas pantallas deben ser los que se envían al punto final de puntuación del modelo (y, en consecuencia, se añadirán a la tabla de carga útil). Si los datos se manipulan antes de enviarlos al punto final de puntuación, especifique los valores manipulados. Por ejemplo, si los datos originales tenían valores de `Hombre` y `Mujer` para *Sexo* y se han manipulado de forma que los datos enviados al punto final de puntuación han sido `H` y `M`, especifique `H` y `M` en la pantalla.

     Pulse **Siguiente** cuando haya terminado con cada una de las características.

1.  Ahora, especifique valores que representen un resultado favorable para el modelo. Los valores se derivan de la columna `etiqueta` de los [datos de entrenamiento](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata), si el esquema de salida del modelo contiene una columna de correlación. En WML, la columna `predicción` siempre tiene un valor doble. La columna de correlación se utiliza para especificar la correlación de este valor `predicción` en la etiqueta de clase.

    Por ejemplo, si el valor `predicción` es `1.0`, la columna de correlación podría tener un valor de `Préstamo denegado`; esto implica que la predicción del modelo es `Préstamo denegado`. Por lo tanto, si el esquema de salida del modelo contiene una columna de correlación, especifique los valores Favorable y Desfavorable utilizando aquellos presentes en la columna de correlación.

    Sin embargo, si la columna de correlación no está presente en el esquema de salida del modelo, los valores Favorable y Desfavorable se deben especificar utilizando el valor de la columna `predicción` (`0.0`, `1.0`, etc.)

     ![Configurar resultado](images/fair-config-outcome.png)

     Pulse **Siguiente**.

1.  Finalmente, establezca un tamaño de muestra mínimo, para evitar la medición de equidad hasta que haya disponible un número mínimo de registros en el conjunto de datos de evaluación. Esto garantiza que el tamaño de la muestra no es demasiado pequeño y pueda causar desviaciones en los resultados. Cada vez que se ejecuta la comprobación de sesgo, se utilizará el tamaño mínimo de muestra para decidir el número de registros sobre el que se calculará el sesgo.

     ![Configurar tamaño de la muestra](images/fair-config-sample.png)

1.  Pulse el botón **Siguiente**.

    Aparece un resumen de sus selecciones para su revisión. Si desea cambiar algo, pulse el enlace **Editar** para esa sección.

    Puede seleccionar también el enlace **Añadir otra característica** para volver a la pantalla de selección de características y añadir más características al supervisor de equidad, por ejemplo: `Ciudad`, `Código postal` o `Saldo de cuenta`.

1.  Pulse **Guardar** para completar la configuración.

### Cómo funciona la eliminación del sesgo
{: #mf-debias}

A continuación, se le presentará una pantalla que proporciona un punto final de puntuación sin sesgo.

  ![API para eliminar el sesgo](images/fair-debias-api.png)

El punto final de puntuación sin sesgo se puede utilizar exactamente como el punto final de puntuación normal del modelo desplegado. Además de devolver la respuesta del modelo desplegado, también devuelve dos columnas adicionales denominadas `debiased_prediction` y `debiased_probability`.

- La columna `debiased_prediction` contiene el valor de predicción sin sesgo. En el caso de Watson Machine Learning (WML), es la representación codificada de la predicción. Por ejemplo, si la predicción del modelo es "Préstamo otorgado" o "Préstamo denegado", WML puede codificar estos dos valores como "0.0" y "1.0", respectivamente. La columna `debiased_prediction` contiene dicha representación codificada de la predicción sin sesgo.

- La columna `debiased_probability`, por otro lado, representa la probabilidad de la predicción sin sesgo. Se trata de una matriz de valor doble, donde cada valor representa la probabilidad de la predicción sin sesgo perteneciente a una de las clases de predicción.

También se devuelve otra columna, `debiased_decoded_target`, en caso de que tenga una columna en el esquema de salida que contenga una columna con `modeling-role` como `decoded-target`.

- La columna `debiased_decoded_target` contiene la representación de serie de la predicción sin sesgo. En el ejemplo anterior, donde el valor de predicción era "0.0" o "1.0", `debiased_decoded_target` contendrá "Préstamo otorgado" o "Préstamo denegado".

Idealmente, llamaría directamente a este punto final desde su aplicación de producción, en lugar de llamar directamente al punto final de puntuación de su modelo desplegado en el motor de servicio del modelo (Watson Machine Learning, Amazon Sagemaker, Microsoft Azure ML Studio, etc.) De esta forma, {{site.data.keyword.aios_short}} también almacenará los valores `sin sesgo` en la tabla de registro de carga útil de su modelo de despliegue. A continuación, se eliminará automáticamente el sesgo de toda la puntuación realizada mediante este punto final.

Puesto que este punto final se ocupa del sesgo en tiempo de ejecución, continuará realizando comprobación en segundo plano de los últimos datos de puntuación de la tabla de registro de carga útil, y continuará actualizando el modelo de mitigación de sesgos que se utiliza para eliminar el sesgo de las solicitudes de puntuación. De esta forma, {{site.data.keyword.aios_short}} está siempre actualizado con los últimos datos entrantes, y con su comportamiento para detectar y mitigar sesgos.

Finalmente, {{site.data.keyword.aios_short}} utiliza un umbral para decidir qué datos son ahora aceptables y se consideran ahora sin sesgo. Este umbral se toma como el valor mínimo de los umbrales establecidos en el supervisor de equidad para todos los atributos de equidad configurados.

### Pasos siguientes
{: #mf-next}

En la página *Configurar supervisores*, puede seleccionar otra categoría de supervisión.
