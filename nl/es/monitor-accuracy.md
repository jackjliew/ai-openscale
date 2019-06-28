---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# Exactitud
{: #acc-monitor}

La exactitud le permite conocer la precisión con la que el modelo predice los resultados.
{: shortdesc}

## Información sobre la Exactitud
{: #acc-understand}

La exactitud puede indicar distintos aspectos en función del tipo de algoritmo:

- *Clasificación multiclase*: la exactitud mide el número de veces que se ha predicho correctamente cualquier clase, normalizada por el número de puntos de datos. Para obtener más detalles, consulte [Clasificación multiclase ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window} en la documentación de Apache Spark.

- *Clasificación binaria*: para un algoritmo de clasificación binaria, la exactitud se mide como el área bajo una curva ROC. Consulte [Clasificación binaria ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window} en la documentación de Apache Spark para obtener más detalles.

- *Regresión*: los algoritmos de regresión se miden utilizando el Coeficiente de determinación, o R2. Para obtener más detalles, consulte [Evaluación del modelo de regresión ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window} en la documentación de Apache Spark.

### Cómo funciona
{: #acc-works}

Debe añadir datos de opinión etiquetados manualmente mediante la interfaz de usuario de {{site.data.keyword.aios_short}} tal como se muestra a continuación, utilizando un [cliente Python ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} o una [API REST ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window}.

Revise [Infraestructuras soportadas](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram) para ver las limitaciones de supervisión de la exactitud.

### Precisión sin sesgo
{: #acc-debias-view}

Cuando hay datos que le dan soporte, la precisión del modelo incluye tanto el modelo original como el modelo sin sesgo. {{site.data.keyword.aios_full_notm}} calcula la precisión de la salida sin sesgo y la almacena en la tabla de registro de carga útil como una columna adicional.

![Aparece una visualización de modelo con la precisión calculada para el modelo original y para el modelo sin sesgo](images/debiased-accuracy.png)

## Configuración del supervisor de exactitud
{: #acc-config}

1.  En la página *¿Qué es la exactitud?*, pulse **Siguiente** para iniciar el proceso de configuración.

    ![Página ¿Qué es la exactitud?](images/accuracy-what-is.png)

1.  En la página *Establecer umbral de exactitud*, seleccione un valor que represente un nivel de exactitud aceptable.

    La exactitud es un valor sintetizado de las métricas de ciencia de datos relevantes asociadas con cada tipo de modelo determinado. La puntuación es una medida normalizada que le permite comparar fácilmente la exactitud entre distintos tipos de modelo. En situaciones típicas, una puntuación de exactitud de 80 es suficiente.
    {: note}

    ![Establecer límite de exactitud](images/accuracy-set-limit.png)

    Pulse **Siguiente** para continuar.

1.  Ahora, establezca el tamaño mínimo y máximo de la muestra. El tamaño mínimo evita que se mida la exactitud hasta que haya disponible un número mínimo de registros en el conjunto de datos de evaluación; esto garantiza que el tamaño de la muestra no es demasiado pequeño y pueda causar desviaciones en los resultados. El tamaño máximo de la muestra ayuda a gestionar mejor el tiempo y el esfuerzo necesarios para evaluar el conjunto de datos; si se sobrepasa este tamaño, sólo se evaluarán los registros más recientes.

     ![Configurar tamaño de la muestra](images/accuracy-config-sample.png)

1.  Pulse el botón **Siguiente**.

    Aparece un resumen de sus selecciones para su revisión. Si desea cambiar algo, pulse el enlace **Editar** para esa sección.

1.  Pulse **Guardar** para completar la configuración.

Ahora se le presenta la opción de proporcionar directamente datos de opinión al modelo, a fin de evaluar la exactitud.

  ![Enviar datos de opinión](images/accuracy-send-feedback0.png)

Seleccione el botón *Añadir datos de opinión* para cargar un archivo de datos con formato CSV; establezca el delimitador para que coincida con sus datos.

Se espera que el archivo CSV de opinión tenga los valores de todas las características, y el valor de destino/etiqueta asignado manualmente. Por ejemplo, los datos de entrenamiento del modelo de fármacos contiene los valores de características `"EDAD"`, `"SEXO"`, `"BP"`, `"COLESTEROL"`,`"NA"`,`"K"`, y el valor de destino/etiqueta `"FÁRMACO"`. El archivo CSV de opinión debe incluir valores para estos campos; un ejemplo sería `[43, M, ALTO, NORMAL, 0.6345, 1.4587, FármacoX]`. Si se proporciona una cabecera para el archivo CSV de opinión, los nombres de campo se correlacionan utilizando esa cabecera. De lo contrario, el orden de los campos **DEBE** ser exactamente el mismo que en el esquema de entrenamiento. Para obtener más información sobre los datos de entrenamiento, consulte [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
{: important}

Observe que los tipos de predicción que devuelve el modelo y la columna de etiqueta/destino de los datos de opinión deben coincidir.
{: note}

  ![Delimitador de exactitud](images/accuracy-delimit.png)

Los tamaños de archivo actualmente están limitados a 8 MB.
{: note}

Como alternativa, puede publicar datos de opinión mediante los fragmentos de código `cURL` o `Python` proporcionados.

Los campos y valores de los fragmentos de código se deben sustituir con sus valores reales, ya que los que se proporcionan son sólo ejemplos.
{: important}

También puede elegir **Salir** para omitir este paso opcional; aún podrá cargar un archivo CSV para su evaluación posteriormente.

### Pasos siguientes
{: #acc-next}

En la página *Configurar supervisores*, puede seleccionar otra categoría de supervisión.
