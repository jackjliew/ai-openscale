---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: deployment, monitors, data

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

# Preparación de los supervisores para un despliegue
{: #mo-config}

Configure y habilite los supervisores para cada despliegue del que realice el seguimiento con {{site.data.keyword.aios_short}}.
{: shortdesc}

Por ejemplo, si utiliza el **modelo de riesgo crediticio alemán** para la guía de aprendizaje interactiva, seleccione el despliegue de modelo, establezca el tipo de datos para el registro de carga útil y confirme los valores que se presentan como parte de la sección de detalles del modelo.

## Selección de un despliegue
{: #mo-select-deploy}

1. En la pestaña **Detalles**, pulse el botón **Añadir a panel de control**. 

   Aparece una lista de los despliegues de modelos disponibles. Si no ve ningún despliegue de modelo, debe desplegar un modelo utilizando el proveedor de aprendizaje automático. Para la guía de aprendizaje, seleccione el **Modelo de riesgo crediticio alemán**.

   ![Se muestra la pantalla Seleccionar un despliegue de modelo. Tiene selecciones para un proveedor de aprendizaje automático y un despliegue.](images/wos-select-model-deployment.png)

2. Pulse un despliegue de modelo y, a continuación, pulse **Configurar**.

   Si hay varios despliegues para un modelo determinado, al configurar un despliegue todos los demás despliegues para el mismo modelo también se configurarán.

   Una vez que se ha guardado las selecciones, está listo para configurar supervisores, lo que incluye el registro de carga útil, la exactitud y la equidad. 

2. Para empezar, pulse **Configurar supervisores**.

## Proporcionar detalles de registro de carga útil
{: #mo-work-data}

Debe proporcionar información sobre el modelo y los datos de entrenamiento. Para obtener más información sobre los datos de entrenamiento, consulte [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) Para la guía de aprendizaje, en el campo **Tipo de datos**, seleccione **Datos numéricos/categóricos** y, para el **Tipo de algoritmo**, seleccione **Clasificación binaria**.

![Se muestra la pantalla para especificar el tipo de entrada con selecciones para el tipo de datos y el tipo de algoritmo](images/config-what-monitor.png)

- Si utiliza una instancia de {{site.data.keyword.pm_full}} que se encuentra en la misma región que la instancia de {{site.data.keyword.aios_short}}, aunque debe seleccionar Tipo de datos y Tipo de algoritmo, determinada información del registro de carga útil se configura automáticamente. 
- De lo contrario, en la pestaña y las ventanas de **Registro de carga útil**, debe especificar información acerca de los tipos de datos y algoritmos y el registro de carga útil. 

   Hay requisitos específicos en función de las selecciones. Para obtener más información, consulte [Datos numéricos/categóricos](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan).

   Antes de poder configurar los supervisores, debe copiar uno de los fragmentos de código que se deben ejecutar. Ejecute el mandato cURL en la aplicación cliente o el mandato Python en el cuaderno de ciencia de datos. Esto proporciona una forma de registrar las solicitudes de despliegue de modelo y escribir datos de respuesta en la base de datos de carga útil.
   
Una vez que ha enviado los detalles de registro de carga útil, mediante el método de {{site.data.keyword.pm_full}} local o mediante la API, debe volver a la pantalla **Registro de carga útil** y pulsar **He terminado**.

![Se muestra la pantalla Registro de carga útil](images/payload-logging-gosales001.png)

Si la puntuación se envía correctamente a {{site.data.keyword.aios_short}}, después de pulsar el botón **He terminado** se muestra la pantalla siguiente. El botón está oculto y ve el mensaje **El registro se ha activado correctamente**.

![Tras la carga correcta de los datos, se muestra la pantalla Registro de carga útil](images/payload-logging-gosales002.png)


### Proporcionar detalles del modelo
{: #mo-work-model-dets}

Proporcione información sobre el modelo de modo que {{site.data.keyword.aios_short}} pueda acceder a la base de datos y entender cómo se ha configurado el modelo. Por ejemplo, si utiliza el **Modelo de riesgo crediticio alemán** para la guía de aprendizaje interactiva, muchos de los campos se completan automáticamente.

Específicamente para configurar supervisores, debe realizar las tareas siguientes:

1. Especifique la ubicación de los datos de entrenamiento. Para ello, especifique la ubicación, el nombre de host o la dirección IP, el nombre de la base de datos y la información de autenticación.
2. En la base de datos, debe seleccionar la tabla de entrenamiento seleccionando el esquema y la tabla.
3. Seleccione la columna de etiqueta de la tabla de entrenamiento, por ejemplo, para la guía de aprendizaje, pulse el mosaico **Riesgo**.
4. Seleccione las características que se han utilizado para entrenar el despliegue de inteligencia artificial.
5. Seleccione el texto y las características categóricas.
6. Seleccione la columna de predicción de despliegue, por ejemplo, para la guía de aprendizaje, pulse el mosaico **predictedLabel**.
7. Por último, puede revisar los detalles del modelo antes de guardarlos.

En las secciones siguientes se proporciona información específica que se encuentra en función del tipo de modelo, ya sea [Datos numéricos/categóricos](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan) o [Imágenes y texto no estructurado](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datai).


### Datos numéricos/categóricos
{: #mo-nuca}

Para datos numéricos/categóricos, debe proporcionar información sobre los datos de entrenamiento para su modelo, a fin de configurar los supervisores.

- **Configurar manualmente supervisores**: requiere que proporcione la información de conexión para sus datos de entrenamiento.

    - Seleccione el [tipo de algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) y pulse **Siguiente**:

      El formato de los datos de entrenamiento debe coincidir con el modelo. Por ejemplo, si el modelo espera `H` y `M` para la característica `Sexo`, los datos de entrenamiento deberían tener `H` y `M`, no `Hombre` y `Mujer`.  El release actual de {{site.data.keyword.aios_short}} sólo da soporte a las ubicaciones de base de datos Db2 o Cloud Object Storage.
        {: important}

    - Especifique la ubicación (`Db2` o `Cloud Object Storage`), y:

        - Para una base de datos Db2, especifique la información siguiente:

            - Nombre de host o dirección IP
            - Puerto
            - Base de datos (nombre)
            - Nombre de usuario
            - Contraseña

        - Para Cloud Object Storage, especifique la información siguiente:

            - URL de inicio de sesión: el URL de inicio de sesión debe coincidir con el valor de la región del grupo en el que se encuentran los datos de entrenamiento. Especificará el grupo de datos de entrenamiento en el paso siguiente.
            - Instancia de recurso (ID)
            - Clave de API

    - Para garantizar una conexión válida, pulse el botón **Probar** para conectarse a los datos de entrenamiento.
    - Especifique la ubicación exacta de la base de datos Db2 o Cloud Object Storage donde se encuentran los datos de entrenamiento.

        - Para una base de datos Db2, seleccione un esquema y una tabla de entrenamiento que incluya las columnas que espera el modelo.
        - Para Cloud Object Storage, seleccione un grupo y un conjunto de datos.

- **Cargue un archivo de configuración**: elija esta opción si prefiere mantener la privacidad de sus datos de entrenamiento. Puede utilizar un cuaderno Python personalizado para proporcionar a {{site.data.keyword.aios_short}} información para analizar los datos de entrenamiento sin proporcionar acceso a los propios datos de entrenamiento.

  La ejecución del cuaderno Python le permite capturar valores individuales de las columnas del esquema, así como nombres de columna. Además, puede utilizar el cuaderno para preconfigurar el supervisor de equidad.

   - Descargue el [cuaderno
personalizado](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external} y sustituya las credenciales por las suyas propias.
   - Revise atentamente el cuaderno, especificando, donde corresponda, los datos para su modelo. Guarde el cuaderno.
   - Ejecute el cuaderno para generar una archivo de configuración con formato JSON.
   - Cargue el archivo de configuración JSON.

     ![Cargar configuración JSON](images/config-json-monitor.png)

- {{site.data.keyword.aios_short}} localiza los datos de entrenamiento de los metadatos almacenados con el modelo en {{site.data.keyword.pm_full}}. Elija la columna de etiqueta de los datos de entrenamiento que contenga los valores de predicción.
- Seleccione las columnas utilizadas para entrenar el modelo. Estas son las etiquetas que el despliegue del modelo espera en una solicitud.
- Finalmente, seleccione las columnas que contenían texto y que se han convertido en enteros. Por ejemplo, si los datos de entrenamiento originales contenían `Hombre` y `Mujer` para `Sexo`, y ahora se han correlacionado con `0` y `1`, respectivamente, ahora los datos de entrenamiento contienen los valores `0` y `1` para la columna `Sexo`. Identifique esas columnas que ahora contienen enteros, pero que originalmente contenían valores de texto.

### Imágenes y texto no estructurado
{: #mo-imun}

- **Imágenes**

  Para modelos que aceptan imágenes como entrada, la imagen se debe representar con el formato de (altura) x (anchura) x (nº canales), donde cada punto representa valores de monocromo o RGB para cada píxel.

- **Texto no estructurado**

   Para modelos que aceptan texto como entrada, se espera que el modelo acepte todo el texto, y no representaciones vectorizadas del texto.

## Revise y guarde la configuración
{: #mo-save}

Revise el resumen de selección y pulse **Guardar** para continuar.

  ![Seleccionar tabla de datos](images/config-summary-monitor.png)

### Pasos siguientes
{: #mo-next}

Para continuar configurando supervisores, pulse la pestaña **Calidad** y pulse **Empezar**. Para obtener más información, consulte [Configuración del supervisor de calidad](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
