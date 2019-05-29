---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: deployment, monitors, data

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

# Preparación de los supervisores para un despliegue
{: #mo-config}

Configure y habilite los supervisores para cada despliegue del que realice el seguimiento con {{site.data.keyword.aios_short}}.
{: shortdesc}

## Selección de un despliegue
{: #mo-select-deploy}

1.  En primer lugar, debe seleccionar un despliegue.

    Si hay varios despliegues para un modelo determinado, al configurar un despliegue todos los demás despliegues para el mismo modelo también se configurarán.
    {: note}

    ![Página Seleccionar despliegue](images/config-select-deploy.png)

1.  Seleccione el mosaico *Preparar para supervisión*.

    ![Preparar para supervisión](images/config-prep-monitor.png)

## Trabajar con datos
{: #mo-work-data}

1.  Ahora proporcionará información sobre su modelo y los datos de entrenamiento; pulse **Siguiente**. Para obtener más información sobre los datos de entrenamiento, consulte [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

    ![Preparar explicación](images/config-what-monitor.png)

1.  En el menú desplegable, seleccione el tipo de datos que analiza su despliegue y pulse **Siguiente**.

    ![Seleccionar tipo de entrada](images/config-input-monitor.png)

### Datos numéricos/categóricos
{: #mo-nuca}

Para datos numéricos/categóricos, debe proporcionar información sobre los datos de entrenamiento para su modelo, a fin de configurar los supervisores.

  ![Seleccionar tipo de configuración](images/config-manual-monitor.png)

- **Configurar manualmente supervisores**: requiere que proporcione la información de conexión para sus datos de entrenamiento.

    - Seleccione el [tipo de algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) y pulse **Siguiente**:

      ![Multiclase](images/multiclass.png)

      Asegúrese de que el formato de los datos de entrenamiento es exactamente el mismo que el que esperaba el modelo. Por ejemplo, si el modelo espera `H` y `M` para la característica *Sexo*, los datos de entrenamiento deberían tener `H` y `M`, no `Hombre` y `Mujer`. Actualmente {{site.data.keyword.aios_short}} sólo da soporte a las ubicaciones de base de datos Db2 o Cloud Object Storage.
        {: important}

    - Especifique la ubicación (`Db2` o `Cloud Object Storage`), y:

        - Para una base de datos Db2, complete lo siguiente:

            - Nombre de host o dirección IP
            - Puerto
            - Base de datos (nombre)
            - Nombre de usuario
            - Contraseña

            ![Página Especificar ubicación de Db2 de datos de entrenamiento](images/config-train-db2-monitor.png)

        - Para Cloud Object Storage, complete lo siguiente:

            - URL de inicio de sesión

              El URL de inicio de sesión debe coincidir con el valor de región del grupo donde se encuentran los datos de entrenamiento. Especificará el grupo de datos de entrenamiento en el paso siguiente.
              {: important}

            - Instancia de recurso (ID)
            - Clave de API

            ![Página Especificar ubicación de Cloud Object Storage de datos de entrenamiento](images/config-train-cos-monitor.png)

    - Asegúrese de tener una conexión válida pulsando el botón **Probar** para conectarse a los datos de entrenamiento. Pulse **Siguiente**.

    - Especifique la ubicación exacta de la base de datos Db2 o Cloud Object Storage donde se encuentran los datos de entrenamiento.

        - Para una base de datos Db2, seleccione un esquema y una tabla de entrenamiento que incluya las columnas que espera el modelo:

          ![Especificar ubicación de Db2 de la tabla de esquema y entrenamiento](images/fair-config-table-db2.png)

        - Para Cloud Object Storage, seleccione un grupo y un conjunto de datos:

          ![Especificar ubicación de Cloud Object Storage de conjunto de datos](images/fair-config-dset-cos.png)

          Pulse **Siguiente** para continuar al paso 5 siguiente.

- **Cargue un archivo de configuración**: elija esta opción si prefiere mantener la privacidad de sus datos de entrenamiento. Puede utilizar un cuaderno Python personalizado para proporcionar a {{site.data.keyword.aios_short}} información para analizar los datos de entrenamiento sin proporcionar acceso a los propios datos de entrenamiento.

  La ejecución del cuaderno Python le permite capturar valores individuales de las columnas del esquema, así como nombres de columna. Además, puede utilizar el cuaderno para preconfigurar el supervisor de equidad.

    - Descargue el [cuaderno personalizado ![Incono de enlace externo](../../icons/launch-glyph.svg "Incono de enlace externo")](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: new_window} y reemplace las credenciales que contenga con sus propias credenciales.

    - Revise atentamente el cuaderno, especificando, donde corresponda, los datos para su modelo. Guarde el cuaderno.

    - Ejecute el cuaderno para generar una archivo de configuración con formato JSON.

    - Cargue el archivo de configuración JSON.

        ![Cargar configuración JSON](images/config-json-monitor.png)

    - Pulse **Siguiente**.

- {{site.data.keyword.aios_short}} localizará los datos de entrenamiento de los metadatos almacenados con el modelo en WML. Elija la columna de etiqueta de los datos de entrenamiento que contenga los valores de predicción y pulse **Siguiente**.

  ![Seleccionar etiqueta de columna](images/fair-config-column.png)

- Seleccione las columnas utilizadas para entrenar el modelo. Estas son las etiquetas que el despliegue del modelo espera en una solicitud. Pulse **Siguiente**.

    ![Seleccionar etiqueta de columna](images/explain-select-column.png)

- Finalmente, seleccione las columnas que contenían texto y que se han convertido en enteros. Por ejemplo, si los datos de entrenamiento originales contenían `Hombre` y `Mujer` para *Sexo*, y ahora se han correlacionado con `0` y `1`, respectivamente, ahora los datos de entrenamiento contienen los valores `0` y `1` para la columna *Sexo*. Identifique esas columnas que ahora contienen enteros, pero que originalmente contenían valores de texto. Pulse **Siguiente**.

    ![Seleccionar tabla de datos](images/explain-text-column.png)

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

Para empezar a configurar supervisores, seleccione una categoría y pulse **Empezar**.
