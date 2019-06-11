---

title: Confianza y transparencia para los modelos de aprendizaje automático con {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Guía de aprendizaje (avanzada)
{: #tadv-tutorial-advanced}

## Escenario
{: #tadv-scenario}

Una empresa de alquiler de coches ha recopilado datos de opinión sobre la satisfacción de los clientes. El modelo presentado utiliza estos datos para predecir una línea de acción para hacer un seguimiento con un cliente, por ejemplo para proporcionar un bono para su siguiente alquiler.

El modelo utiliza los campos de datos de cliente de ID (un número de ID), SEXO, ESTADO (soltero o casado), HIJOS (número), EDAD, ESTADO DEL CLIENTE (activo o inactivo), PROPIETARIO DE VEHÍCULO (sí o no), SERVICIO AL CLIENTE (comentario del cliente), SATISFACCIÓN (satisfecho o no satisfecho) y ÁREA DE NEGOCIO (relacionado con productos o servicios) para predecir uno de cuatro valores (ND, bono, mejora gratuita, recogida bajo demanda) para el campo de datos ACCIÓN.

## Requisitos previos
{: #tadv-prereqs}

Para completar esta guía de aprendizaje, necesitará:

- Una cuenta de [Watson Studio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://dataplatform.ibm.com/){: new_window}.
- Una cuenta de [{{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}){: new_window}.

Durante la guía de aprendizaje, suministrará los siguientes servicios {{site.data.keyword.cloud_notm}} Lite (gratuitos):

- Machine Learning
- Apache Spark
- Object Storage

También suministrará el siguiente servicio {{site.data.keyword.cloud_notm}} **de pago**:

- PostgreSQL

  Se puede obtener un crédito de {{site.data.keyword.cloud_notm}} por valor de 200 dólares si se convierte en una cuenta de pago con una tarjeta de crédito. Si ya tiene una cuenta de pago, recibirá un reembolso único de 16 dólares del coste de su primer GB de almacenamiento, durante un mes.
  {: tip}

La base de datos PostgreSQL y la instancia de {{site.data.keyword.pm_full}} se deben desplegar en la misma cuenta de {{site.data.keyword.cloud_notm}}.
{: important}

Si ya ha suministrado los servicios necesarios, por ejemplo, si ha completado la otra guía de aprendizaje, siga con [Configurar un proyecto de Watson Studio](#tadv-setup-ws) a continuación.

## Introducción
{: #tadv-intro}

En esta guía de aprendizaje, aprenderá a:

- Suministrar aprendizaje automático y servicios de almacenamiento de {{site.data.keyword.cloud_notm}}
- Configurar un proyecto de Watson Studio y ejecutar un cuaderno Python para crear, entrenar y desplegar un modelo de aprendizaje automático
- Ejecutar un cuaderno Python para crear una despensa de datos, configurar supervisores de rendimiento, exactitud y equidad y crear datos para supervisar
- Ver los resultados en la pestaña Detalles de {{site.data.keyword.aios_short}}

## Suministre servicios de {{site.data.keyword.cloud_notm}}
{: #tadv-svcs}

Inicie sesión en la cuenta de [{{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}){: new_window} con su ID de IBM. Al suministrar servicios, especialmente en el caso de Apache Spark, Object Storage y Db2 Warehouse, compruebe que su organización y espacio seleccionados son los mismos para todos los servicios.

### Cree una cuenta de Watson Studio
{: #tadv-stac}

- [Cree una instancia de Watson Studio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/watson-studio){: new_window} si no tiene aún una asociada con la cuenta:

  ![Watson Studio](images/watson_studio.png)

- Dé un nombre al servicio, elija el plan Lite (gratuito) y pulse el botón **Crear**.

### Suministre un servicio de Machine Learning
{: #tadv-pml}

- [Suministre una instancia de Watson Machine Learning ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/machine-learning){: new_window} si no tiene aún una asociada con la cuenta:

  ![Machine Learning](images/machine_learning.png)

- Dé un nombre al servicio, elija el plan Lite (gratuito) y pulse el botón **Crear**.

- Anote las credenciales del servicio de Machine Learning. En su instancia de Machine Learning, pulse el enlace **Credenciales de servicio** en el lado izquierdo de la página. Dé un nombre a la credencial y pulse **Añadir**. A continuación, en la lista de credenciales, pulse **Ver credencial** y copie las credenciales para utilizarlas posteriormente.

### Suministre un servicio de Spark
{: #tadv-ps}

- [Suministre un servicio de Spark ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/apache-spark){: new_window}si no tiene aún uno asociado con la cuenta:

  ![Apache Spark](images/spark.png)

- Asigne un nombre al servicio, elija el plan Lite (gratuito) y pulse el botón **Crear**.

- Anote las credenciales del servicio de la instancia de Spark. Abra la instancia de Spark y pulse en **Credenciales de servicio** en el menú de la izquierda. Pulse el botón **Nueva credencial**, dé nombre a sus credenciales y pulse **Añadir**. A continuación, pulse el enlace **Ver credenciales** junto al conjunto que acaba de crear y copie estas credenciales para utilizarlas posteriormente.

### Suministre un servicio de Object Storage
{: #tadv-pos}

- [Suministre un servicio de Object Storage ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} si no tiene aún uno asociado con su cuenta:

  ![Object Storage](images/object_storage.png)

- Dé un nombre al servicio, elija el plan Lite (gratuito) y pulse el botón **Crear**.

### Suministre un servicio de PostgreSQL de pago
{: #tadv-ppgs}

- [Suministre un servicio de PostgreSQL de pago ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window} si no tiene aún uno asociado con la cuenta.

  ![Compose for PostgreSQL](images/postgres.png)

- Dé un nombre al servicio, elija el plan Standard y pulse el botón **Crear**.

  Se puede obtener un crédito de {{site.data.keyword.cloud_notm}} por valor de 200 dólares si se convierte en una cuenta de pago con una tarjeta de crédito. Si ya tiene una cuenta de pago, recibirá un reembolso único de 16 dólares del coste de su primer GB de almacenamiento, durante un mes.
  {: tip}

- Anote las credenciales del servicio de la instancia de PostgreSQL. Abra la instancia existente, o que acaba de crear, de PostgreSQL y pulse en **Credenciales de servicio** en el menú de la izquierda. Pulse el botón **Nueva credencial**, dé nombre a sus credenciales y pulse **Añadir**. A continuación, pulse el enlace **Ver credenciales** junto al conjunto que acaba de crear y copie estas credenciales para utilizarlas posteriormente.

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![Establezca manualmente el tipo de datos](images/data-type-manual.png)

- Los datos de entrenamiento ahora se deberían visualizar correctamente en columnas. Pulse **Siguiente** para continuar y a continuación pulse **Iniciar carga** para cargar los datos.

--->

## Configure un proyecto de Watson Studio
{: #tadv-setup-ws}

- Inicie sesión en su [cuenta de Watson Studio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://dataplatform.ibm.com/){: new_window}. Pulse el icono de avatar de la cuenta en la esquina superior derecha y compruebe que la cuenta que utilice sea la misma cuenta que ha utilizado para crear los servicios de {{site.data.keyword.cloud_notm}}:

  ![Misma cuenta](images/same_account.png)

- En Watson Studio, empiece creando un nuevo proyecto. Seleccione "Crear un proyecto":

  ![Crear proyecto de Watson Studio](images/studio_create_proj.png)

- Seleccione el mosaico **Standard** para crear el proyecto:

  ![Seleccionar proyecto Standard de Watson Studio](images/studio_create_standard.png)

- Dé un nombre y una descripción al proyecto, asegúrese de que el servicio de Object Storage que ha creado en el paso anterior esté seleccionado en el menú desplegable **Storage** y pulse **Crear**.

### Asocie los servicios de {{site.data.keyword.cloud_notm}} con el proyecto de Watson
{: #tadv-acsw}

- Abra el proyecto de Watson Studio y seleccione la pestaña **Valores**. En la sección **Servicios asociados**, pulse el menú desplegable **Añadir servicio** y seleccione **Watson**:

  ![Añadir servicio de Watson](images/add_watson_service.png)

- Pulse el enlace **Añadir** en el mosaico **Machine Learning** y seleccione la pestaña **Existente**. Elija el servicio que ha creado en la sección anterior del menú desplegable **Instancia de servicio existente** y pulse **Seleccionar**.

- En la pestaña de valores del proyecto, seleccione de nuevo **Añadir servicio** y elija **Spark** en el menú desplegable. En la pestaña **Existente**, elija el servicio Spark que ha creado y pulse **Seleccionar**.

## Cree y despliegue un modelo de aprendizaje automático
{: #tadv-deploy-ml}

### Añada el cuaderno `CARS4U Modelo de recomendación de acción` al proyecto de Watson Studio

- Descargue el archivo siguiente:

    - [CARS4U Modelo de recomendación de acción ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- En la pestaña **Activos** del proyecto de Watson Studio, pulse el botón **Añadir a proyecto** y seleccione **Cuaderno** en el menú desplegable:

  ![Añadir conexión](images/add_notebook.png)

- Seleccione **Desde archivo**:

  ![Nuevo formulario de cuaderno](images/new_notebook_name.png)

- A continuación, pulse el botón **Elegir archivo** y seleccione el cuaderno "CARS4U Modelo de recomendación de acción" que ha descargado:

  ![Nuevo formulario de cuaderno](images/new_notebook_name2.png)

- En la sección **Seleccionar tiempo de ejecución**, elija la instancia de Spark que ha creado anteriormente en la lista desplegable:

  ![Tiempo de ejecución de Spark](images/spark_runtime.png)

- Pulse **Crear cuaderno**.

### Edite y ejecute el cuaderno `CARS4U Modelo de recomendación de acción`
{: #tadv-ern}

El cuaderno `CARS4U Modelo de recomendación de acción` contiene instrucciones detalladas para cada paso del código Python que ejecutará. A medida que avance en el cuaderno, dedique algún tiempo a comprender qué hace cada mandato.
{: tip}

- En la pestaña **Activos** del proyecto de Watson Studio, pulse el icono **Editar** junto al cuaderno `CARS4U Modelo de recomendación de acción` para editarlo.

- En la sección 2.2, "Cargar datos a la base de datos de PostgreSQL", reemplace las credenciales de servicio de Postgres con las que ha creado en la sección anterior.

- En la sección 4, "Almacenar el modelo en el repositorio", en **SUGERENCIA**, reemplace las credenciales de Watson Machine Learning con las que ha creado en la sección anterior.

- Una vez que haya especificado sus credenciales, el cuaderno estará listo para ejecutarse. Pulse el elemento de menú **Kernel** y seleccione **Reiniciar y ejecutar todo** en el menú:

  ![Reiniciar y ejecutar](images/restart_and_run.png)

  Esto creará, entrenará y desplegará el cuaderno **CARS4U Modelo de recomendación de acción** en el proyecto. Puede comprobar que el modelo se ha desplegado seleccionando la pestaña **Despliegues** del proyecto de Watson Studio y pulsando el enlace **CARS4U - Despliegue del modelo de acción y área**.

## Configure {{site.data.keyword.aios_short}}
{: #tadv-config-aios}

### Suministre {{site.data.keyword.aios_short}}
{: #tadv-paios}

- Si no ha suministrado ya una instancia de {{site.data.keyword.aios_short}}, pulse el enlace **Catálogo** de la cuenta de {{site.data.keyword.cloud_notm}} y filtre por "OpenScale". Seleccione el mosaico de {{site.data.keyword.aios_short}}.

<!---
  ![{{site.data.keyword.aios_short}}](images/openscale.png)
--->

- Dé un nombre al servicio, seleccione el plan Lite y pulse **Crear**.

### Conecte {{site.data.keyword.aios_short}} al modelo de aprendizaje automático
{: #tadv-cmlm}

Puesto que el modelo de aprendizaje automático se ha desplegado, puede configurar {{site.data.keyword.aios_short}} para garantizar la confianza y transparencia con sus modelos. Seleccione la pestaña **Gestionar** de la instancia de {{site.data.keyword.aios_short}} y pulse el botón **Iniciar aplicación**. Se abre la página Cómo empezar de {{site.data.keyword.aios_full}}; pulse **Empezar**.

- Seleccione el mosaico "Watson Machine Learning" y pulse **Siguiente**.

  ![Establecer instancia de WML](images/gs-wml-default.png)

- Seleccione la instancia de Watson Machine Learning del menú desplegable y pulse **Siguiente**.

  ![Establecer instancia de WML](images/gs-set-wml.png)

- Ahora puede seleccionar qué modelos desplegados supervisará {{site.data.keyword.aios_short}}. Compruebe el modelo que ha creado y desplegado; pulse **Siguiente** para aceptar esto:

  ![Seleccionar modelos desplegados](images/gs-set-deploy.png)

- A continuación, debe elegir una base de datos de PostgreSQL. Tiene dos opciones: la base de datos del plan Lite gratuito o una base de datos nueva o existente. Para esta guía de aprendizaje, seleccione el mosaico **Utilizar una base de datos existente o adquirir una nueva**.

    ![Seleccionar base de datos](images/gs-set-lite-db1.png)

  Consulte toda la información detallada sobre cada una de estas opciones en el tema [Especificación de una base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
  {: note}

- Una vez que haya seleccionado la opción "Utilizar una base de datos existente o adquirir una nueva", {{site.data.keyword.aios_short}} compruebe su cuenta de {{site.data.keyword.cloud_notm}} para localizar la base de datos de Compose for PostgreSQL existente.

  Seleccione el esquema "data_mart" en el menú desplegable **Esquema**.

  ![Seleccionar base de datos](images/gs-set-schema1.png)

- Una vez que haya seleccionado la base de datos y el esquema, pulse **Siguiente** para revisar los datos del resumen y pulse **Guardar**.

  ![Seleccionar base de datos](images/gs-setup-summary3.png)

  Pulse **Ir al panel de control** cuando se le solicite.

## Cree una despensa de datos y configure supervisores de rendimiento, exactitud y equidad
{: #tadv-config-monitors}

### Añada el cuaderno `{{site.data.keyword.aios_short}} y motor de Watson Machine Learning` al proyecto de Watson Studio
{: #tadv-aomn}

El cuaderno `{{site.data.keyword.aios_short}} y motor de Watson Machine Learning` contiene instrucciones detalladas de cada paso del código Python que ejecutará. A medida que avance en el cuaderno, dedique algún tiempo a comprender qué hace cada mandato.
{: tip}

- Descargue el archivo siguiente:

    - [{{site.data.keyword.aios_short}} y motor de Watson Machine Learning ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- En la pestaña **Activos** del proyecto de Watson Studio, pulse el botón **Añadir a proyecto** y seleccione **Cuaderno** en el menú desplegable:

  ![Añadir conexión](images/add_notebook.png)

- Seleccione **Desde archivo**:

  ![Nuevo formulario de cuaderno](images/new_notebook_name.png)

- A continuación, pulse el botón **Elegir archivo** y seleccione el cuaderno "{{site.data.keyword.aios_short}} y motor de Watson Machine Learning" que ha descargado:

  ![Nuevo formulario de cuaderno](images/new_notebook_name3.png)

- En la sección **Seleccionar tiempo de ejecución**, elija la instancia de Spark que ha creado anteriormente en la lista desplegable:

  ![Tiempo de ejecución de Spark](images/spark_runtime.png)

- Pulse **Crear cuaderno**.

### Edite y ejecute el cuaderno `{{site.data.keyword.aios_short}} y motor de Watson Machine Learning`
{: #tadv-eromn}

- En la pestaña **Activos** del proyecto de Watson Studio, pulse el icono **Editar** junto al cuaderno `{{site.data.keyword.aios_short}} y motor de Watson Machine Learning` para editarlo.

- En la sección 1.1, "Instalación y autenticación":

    - En **ACCIÓN: Obtener instance_id (GUID) y apikey**, siga las instrucciones para obtener sus credenciales. Reemplace `aios_credentials` con sus propias credenciales.

    - A continuación, en **ACCIÓN: Añada aquí las credenciales de Watson Machine Learning**, reemplace las credenciales de Watson Machine Learning con las que ha creado anteriormente.

    - Finalmente, en **ACCIÓN: Añada aquí sus credenciales de PostgreSQL**, reemplace las credenciales de Postgres con las que ha creado anteriormente.

- Una vez que haya especificado sus credenciales, el cuaderno estará listo para ejecutarse. Pulse el elemento de menú **Kernel** y seleccione **Reiniciar y ejecutar todo** en el menú:

  ![Reiniciar y ejecutar](images/restart_and_run.png)

  Esto configurará su despensa de datos, habilitará el registro de carga útil, configurará y puntuará los supervisores de rendimiento, exactitud y equidad y proporcionará estas métricas a la instancia de {{site.data.keyword.aios_short}}.

## Visualización de los resultados
{: #tadv-results}

### Vea los detalles de su despliegue
{: #tadv-vide}

Utilizando el panel de control de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, pulse en la pestaña **Detalles**:

  ![Detalles](images/insight-dash-tab.png)

La página Detalles proporciona una descripción general de las métricas para los modelos desplegados. Puede ver fácilmente las alertas de las métricas de Equidad o Exactitud que han caído por debajo del umbral establecido al ejecutar el cuaderno (70%). Los datos y los valores utilizados en esta guía de aprendizaje habrán creado métricas de Exactitud y Equidad similares a las que se muestran aquí.

  ![Descripción general de Detalles](images/insight-overview-adv-tutorial.png)

### Vea los datos de supervisión de su despliegue
{: #tadv-vmdd}

Seleccione un despliegue pulsando el mosaico en la página Detalles. Aparecerán los datos de supervisión de ese despliegue. Deslice el marcador por el gráfico para seleccionar los datos del periodo de tiempo durante el que ha ejecutado el cuaderno. A continuación, seleccione, el enlace **Ver detalles**.

  ![Supervisar datos](images/insight-monitor-data1.png)

Ahora puede revisar en los gráficos los datos que ha supervisado. Para este ejemplo, puede utilizar el menú desplegable **Característica** para seleccionar "Hijos" o "Sexo", para ver detalles sobre los datos supervisados.

  ![Descripción general de Detalles](images/insight-review-charts1.png)

<!---

### Ver explicabilidad de una transacción de modelo
{: #tadv-vemt}

Seleccione el botón **Ver transacciones** de los gráficos para los datos que ha supervisado.

  ![Ver transacciones](images/view_transactions.png)

  se lista una lista de las transacciones de la última hora. Copie uno de los ID de transacción.

  ![Lista de transacciones](images/transaction_list.png)

Utilizando el panel de control de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, pulse en la pestaña **Explicabilidad**:

  ![Explicabilidad](images/explainability.png)

Pegue el valor de ID de transacción que ha copiado en el recuadro de búsqueda y pulse **Retorno** en el teclado. Ahora verá una explicación de cómo el modelo ha llegado a esta conclusión, incluido el grado de seguridad del modelo, los factores que han contribuido al nivel de confianza y los atributos con los que se ha alimentado el modelo.

  ![Ver transacciones](images/view_transaction1.png)

--->

## Pasos siguientes
{: #tadv-next}

- Obtenga más información sobre cómo [ver e interpretar los datos](/docs/services/ai-openscale?topic=ai-openscale-it-ov) y [supervisar la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
