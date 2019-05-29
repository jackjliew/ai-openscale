---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: databases, connections, scoring, requests

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

# Especificación de una base de datos
{: #connect-db}

Especifique una base de datos para que la utilice su instancia de {{site.data.keyword.aios_short}}.
{: shortdesc}

## Conexión a la base de datos
{: #cdb-connect}

{{site.data.keyword.aios_short}} utiliza una base de datos para almacenar datos de carga útil, opinión y medidas. Antes de seleccionar una base de datos, también puede seleccionar un esquema para la base de datos (un esquema es una colección con nombre de tablas de la base de datos).

1.  Elija una base de datos. Tiene dos opciones: la base de datos gratuita o una base de datos nueva o existente. 

    ![Seleccionar base de datos](images/gs-config-database.png)

    Si tiene una cuenta de {{site.data.keyword.cloud_notm}}, puede adquirir un servicio
de `Databases for PostgreSQL` o `Db2 Warehouse` que se aproveche de las ventajas de la integración con
Watson Studio y los servicios de aprendizaje continuo. Si elige no adquirir un servicio de pago, puede utilizar el almacenamiento interno gratuito
de PostgreSQL con {{site.data.keyword.aios_short}}, pero no podrá configurar el aprendizaje continuo para su modelo.
    {: note}

### Base de datos del plan Lite gratuito
{: #cdb-lite}

**NOTA**: La base de datos gratuita tiene algunas limitaciones importantes:

- La base de datos gratuita está alojada y no se puede acceder a ella directamente.
- {{site.data.keyword.aios_full}} tendrá acceso completo a su base de datos, y por lo tanto tendrá acceso completo a sus datos.
- La base de datos gratuita no cumple el GDPR. Si el modelo procesa información de identificación personal, no puede utilizar la base de datos gratuita. Debe adquirir una base de datos nueva, o utilizar una base de datos existente que cumpla las reglas del GDPR. Consulte [Seguridad de la información](/docs/services/ai-openscale?topic=ai-openscale-is-ov) para obtener más información.

Para continuar utilizando la base de datos gratuita, pulse el mosaico **Utilizar la base de datos gratuita alojada por {{site.data.keyword.aios_short}}** y a continuación revise los datos de resumen y pulse **Guardar**.

  ![Seleccionar base de datos](images/gs-config-database2.png)
  
Puede actualizar a otra base de datos desde la base de datos gratuita, pero no es posible volver a configurar una instancia de Compose for Postgres, Database for Postgres o Db2 para la base de datos gratuita. Después de actualizar, no es posible volver a la base de datos gratuita. Los datos actuales, como la configuración, los resultados de puntuación y las explicaciones, no se pueden volver a utilizar. Al seleccionar otro esquema o base de datos, el entorno de {{site.data.keyword.aios_short}} se restablece completamente.



### Base de datos nueva o existente
{: #cdb-exn}

1.  Una vez que ha seleccionado la opción "Utilizar una base de datos existente o adquirir una nueva", {{site.data.keyword.aios_short}} comprueba si hay bases de datos existentes en su cuenta de {{site.data.keyword.Bluemix_notm}}.

1.  Seleccione el tipo de base de datos existente (Compose for Postgres, Database for Postgres o Db2), una base de datos en el menú desplegable **Base de datos** y a continuación un **Esquema**:

    {{site.data.keyword.aios_short}} utiliza la base de datos PostgreSQL o Db2 para almacenar datos de salida o de reentrenamiento del despliegue de modelo. Actualmente no se da soporte a los planes Lite Db2. Para obtener más información sobre los datos de entrenamiento, consulte [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
    {: note}

    ![Seleccionar base de datos](images/gs-config-database3.png)

1.  También puede pulsar **Seleccionar otra ubicación** para especificar una ubicación de base de datos fuera de su cuenta de {{site.data.keyword.Bluemix_notm}}.

    {{site.data.keyword.aios_short}} utiliza la base de datos PostgreSQL o Db2 para almacenar datos de salida o de reentrenamiento del despliegue de modelo. Actualmente no se da soporte a los planes Lite Db2.
    {: note}

    - Seleccione el **Tipo de base de datos** (`Compose for PostgreSQL`, `Database for PostgreSQL` o `Db2`) y a continuación proporcione la información de conexión:

        - Para una base de datos `Compose for PostgreSQL`, complete lo siguiente:

            - Nombre de host o dirección IP
            - Puerto
            - Base de datos (nombre)
            - Nombre de usuario
            - Contraseña

            ![Especificar ubicación de base de datos Compose for Postgres](images/db-config-cpostgres.png)

        - Para una base de datos `Database for PostgreSQL`, complete lo siguiente:

            - Nombre de host o dirección IP
            - Puerto SSL
            - Certificado codificado en Base-64
            - Base de datos (nombre)
            - Nombre de usuario
            - Contraseña

            ![Especificar ubicación de base de datos Database for Postgres](images/db-config-dpostgres.png)

        - Para una base de datos `Db2`, complete lo siguiente:

            - Nombre de host o dirección IP
            - Puerto SSL
            - Base de datos (nombre)
            - Nombre de usuario
            - Contraseña

            ![Especificar ubicación de Db2](images/db-config-db2.png)

    - Una vez que se ha conectado correctamente, puede seleccionar un esquema.

      Es necesario proporcionar explícitamente el nombre de esquema si proporciona una instancia de Db2 con acceso limitado, lo que no permite que el nombre de esquema se genere automáticamente. Esto es aplicable al plan Entry de Db2 Warehouse.
      {: important}

      ![Seleccionar esquema](images/gs-config-database5.png)

1.  Pulse **Siguiente** para revisar los datos de resumen y a continuación pulse **Guardar**.

## Envío de una solicitud de puntuación
{: #cdb-score}

Para configurar supervisores, {{site.data.keyword.aios_short}} requiere que se envíe una solicitud de puntuación, a fin de empezar a registrar los datos que se supervisarán.

{{site.data.keyword.aios_short}} puntúa automáticamente los modelos desplegados en Watson Machine Learning.
{: note:}

Seleccione un despliegue, en este caso "Detector de fraude" y a continuación utilice los fragmentos de código `cURL` o `Python` proporcionados para registrar los datos de solicitud y respuesta de despliegue del modelo. Consulte [Registro de carga útil para instancias de servicio que no sea Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect) para obtener más información.

Los campos y valores de los fragmentos de código se deben sustituir con sus valores reales, ya que los que se proporcionan son sólo ejemplos.
{: important}

![Seleccionar base de datos](images/config-send-scoring.png)

Una vez que ha ejecutado el registro de carga útil, verá una marca de comprobación en la columna "Preparado para supervisar" para el despliegue seleccionado. Pulse **Configurar supervisores** para continuar.

## Pasos siguientes
{: #cdb-next}

{{site.data.keyword.aios_short}} ahora está listo para que usted [configure supervisores para sus despliegues](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
