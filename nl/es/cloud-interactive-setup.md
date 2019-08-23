---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, fast start

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

# Guía de aprendizaje de configuración interactiva
{: #gs-obj}

En esta guía de aprendizaje, aprenderá a suministrar los servicios de {{site.data.keyword.Bluemix_notm}} necesarios, a configurar un proyecto y a desplegar un modelo de ejemplo en Watson Studio, y a configurar supervisores en {{site.data.keyword.aios_short}}.
{: shortdesc}

1. [Suministrar servicios de aprendizaje automático y almacenamiento de {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps).
2. [Configurar un proyecto de Watson Studio y crear, entrenar y desplegar un modelo de aprendizaje automático](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup).
3. [Configurar y explorar confianza, transparencia y
explicabilidad para el modelo](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios).

## Suministrar servicios de {{site.data.keyword.Bluemix_notm}} de requisito previo
{: #gs-prps}

Además de {{site.data.keyword.aios_short}}, para completar esta guía de aprendizaje, necesita las cuentas y servicios siguientes.

**Importante**: Para obtener el mejor rendimiento, se recomienda que los servicios de requisito previo se creen en la misma región
que {{site.data.keyword.aios_short}}. Para ver las ubicaciones disponibles para {{site.data.keyword.aios_short}}, consulte
[Disponibilidad de servicios](/docs/resources?topic=resources-services_region){: external}.

1.  Inicie una sesión en su cuenta de [{{site.data.keyword.Bluemix_notm}} ](https://{DomainName}){: external}
con {{site.data.keyword.ibmid}}.
1.  Para cada uno de los servicios siguientes que todavía no ha asociado a su cuenta, cree una instancia pulsando el enlace, asignando un nombre al
servicio, seleccionando el plan (gratuito) **Lite** y pulsando el botón **Crear**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Configurar un proyecto de Watson Studio
{: #gs-setup}

1.  Inicie la sesión en la cuenta de [Watson Studio](https://dataplatform.ibm.com/){: external} y empiece creando un nuevo
proyecto. Pulse **Crear un proyecto**.

    ![Crear proyecto de Watson Studio](images/studio_create_proj.png)

1.  Pulse el mosaico **Crear un proyecto vacío**.
1.  Dé un nombre y una descripción al proyecto, asegúrese de que el servicio de Object Storage que ha creado en el paso anterior esté seleccionado
en el menú **Storage** y pulse **Crear**.

### Asocie los servicios de {{site.data.keyword.Bluemix_notm}} con el proyecto de Watson
{: #gs-assoc}

1.  Abra el proyecto de Watson Studio y seleccione la pestaña **Valores**. En la sección **Servicios asociados**, pulse **Añadir servicio** y, a continuación, pulse **Watson**.

    ![Añadir servicio de Watson](images/add_watson_service.png)

1.  Pulse el enlace **Añadir** en el mosaico **Machine Learning**.
2.  En la pestaña **Existente**, en el menú desplegable **Instancia de servicio existente**, pulse el servicio
que ha creado anteriormente.
3. Pulse **Seleccionar**.

### Añada el modelo `Riesgo crediticio`
{: #gs-addmod}

1.  En {{site.data.keyword.DSX}}, seleccione la pestaña **Activos** del proyecto, desplácese a la sección
**Modelos de aprendizaje automático de Watson** y pulse el botón **Nuevo modelo de aprendizaje automático de Watson**.

1.  En la sección **Seleccionar tipo de modelo**, seleccione **Del ejemplo** y el `Riesgo
crediticio` y, a continuación, pulse **Crear**.

    ![Se muestra el mosaico de riesgo crediticio](images/credit-sample-model.png)

### Despliegue el modelo `Riesgo crediticio`
{: #gs-depmod}

1.  En la página de modelo `Riesgo crediticio`, pulse la pestaña **Despliegues** y, a continuación, pulse
**Añadir despliegue**.
1.  Especifique `credit-risk-deploy` como nombre del despliegue y seleccione el tipo de despliegue **Servicio web**.
1.  Pulse **Guardar**.

## Configure {{site.data.keyword.aios_short}}
{: #gs-confaios}

Ahora que el modelo de aprendizaje automático se ha desplegado, puede configurar {{site.data.keyword.aios_short}} para garantizar la confianza y transparencia con sus modelos.

### Suministro de {{site.data.keyword.aios_short}}
{: #gs-provaios}

1.  [Suministre una nueva instancia de servicio de {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  Proporcione un nombre a su servicio, seleccione el **Plan Lite** y pulse **Crear**.

1.  Seleccione la pestaña **Gestionar** de la instancia de {{site.data.keyword.aios_short}} y pulse el botón **Iniciar aplicación**. Se
abrirá la página de demostración **Bienvenido a {{site.data.keyword.aios_short}}**.
2. Para esta guía de aprendizaje, pulse **No, gracias**.

### Seleccionar una base de datos
{: #gs-db-choice}

A continuación, debe elegir una base de datos. Tiene dos opciones: la base de datos gratuita o una base de datos nueva o existente.

2. Para esta guía de aprendizaje, seleccione el mosaico **Utilizar la base de datos del plan Lite gratuito**.

   La base de datos gratuita tiene algunas limitaciones importantes. Es una base de datos alojada que no le proporciona acceso individual a ella. Proporciona a {{site.data.keyword.aios_short}} acceso a su base de datos y sus datos. No es compatible con el GDPR. Consulte toda la información detallada sobre cada una de estas opciones en el tema [Especificación de una base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db). La base de datos existente puede ser una base de datos PostgreSQL o una base de datos Db2.
    {: tip}

   ![Seleccionar base de datos](images/gs-set-lite-db2.png)

1.  Revise los datos de resumen y pulse **Guardar**. Confirme y, cuando se le solicite, pulse el botón **Continuar con la configuración**.

    Se lista también un ID de despensa de datos, que coincide con el ID de instancia de {{site.data.keyword.aios_short}}.
    {: tip}

    ![Vista de resumen](images/gs-setup-summary4.png)

1.  Su pantalla podría ser similar a la siguiente captura de pantalla. Puesto que utilizará un método de la GUI para puntuar sus datos, seleccione simplemente el botón **Configurar supervisores** para completar esta configuración.

    ![Código de solicitud de puntuación](images/gs-config-send-scoring.png)

### Conecte {{site.data.keyword.aios_short}} al modelo de aprendizaje automático
{: #gs-ctmod}


1.  Pulse el mosaico **Watson Machine Learning** y a continuación **Guardar**.

1.  Para esta guía de aprendizaje, seleccione la instancia de {{site.data.keyword.pm_full}} en el menú y pulse
**Siguiente**.

    También tiene la opción de seleccionar una ubicación de {{site.data.keyword.pm_short}} distinta. Consulte [Especificación de una instancia de servicio de {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-wml-connect) para obtener información adicional.
    {: note}

    ![Establecer instancia de {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

Ahora puede seleccionar los modelos desplegados que supervisará {{site.data.keyword.aios_short}}.


### Proporcione un conjunto de datos de ejemplo al modelo
{: #gs-samp}

Para configurar sus supervisores, primero debe generar al menos una solicitud de puntuación para el modelo a fin de generar registro de carga útil que puedan consumir los supervisores. En esta sección, proporcionará datos de ejemplo a Watson Studio en forma de un archivo JSON para generar una solicitud de puntuación.

1.  Descargue el archivo
[credit_payloadload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  En la pestaña **Despliegues** del proyecto de Watson Studio, pulse el enlace **credit-risk-deploy** **Probar** y seleccione el icono de entrada de JSON.

    ![Prueba de JSON](images/json_test02.png)

1.  Ahora, abra el archivo `credit_payload_data.json` que ha descargado y copie el contenido en el campo JSON de la pestaña **Probar**. Pulse el botón **Predecir** para enviar y puntuar cargas útiles de entrenamiento al modelo.

    ![Predicción de JSON](images/json_test03.png)

## Pasos siguientes
{: #gs-next-steps-config}

Continúe con esta guía de aprendizaje completando los pasos siguientes:

1. [Prepare los supervisores para el despliegue](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy).

   Para preparar los supervisores, debe seleccionar uno de los modelos desplegados y añadirlo al panel de control. En la pestaña **Detalles**, pulse un mosaico de despliegue o pulse el botón **Añadir a panel de control** para seleccionar un modelo desplegado y pulse **Configurar**.

2. [Configure el registro de carga útil](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data).

   En la sección **Registro de carga útil**, debe especificar el tipo de entrada.

3. [Configure los detalles del modelo](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets).

   En la sección **Detalles del modelo**, debe registrar los detalles del modelo. Para esta guía de aprendizaje, seleccione **Configurar manualmente supervisores**.

4. [Configure la supervisión de calidad](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

   En la sección **Calidad**, establezca el umbral de alerta de calidad y los tamaños de ejemplo.

5. [Configure la supervisión de equidad](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

   En la sección **Equidad**, elija las características que desea supervisar para la equidad. Para cada característica que seleccione, {{site.data.keyword.aios_short}} supervisará la propensión del modelo desplegado a un resultado favorable para un grupo sobre otro. Aunque las características se supervisan individualmente, el sesgo corrige los problemas de todas las características a la vez.

6. [Configure el supervisor de detección de desviación](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

   En la sección **Desviación** puede configurar un modelo de detección de desviación.
   
5. [Proporcione un conjunto de datos de opinión de ejemplo al modelo](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv).

   Para habilitar la supervisión de la calidad, debe proporcionar al modelo datos de opinión. Hasta que no se hace esto, los datos de calidad no aparecerán en el panel de control. Puede generar todas las solicitudes a la vez añadiendo datos de opinión de muestra al modelo para la puntuación. Para esta tarea, descargará un archivo CSV que contiene datos de opinión de muestra.

6. [Obtenga los detalles](/docs/services/ai-openscale?topic=ai-openscale-io-ov).

   La comprobación de exactitud se ejecuta una hora después de haber configurado la supervisión de la exactitud. En un sistema de producción, esto tiene sentido, ya que el panel de control puede acumular datos de opinión. Para los fines de esta guía de aprendizaje, probablemente deseará desencadenar manualmente la comprobación de exactitud después de añadir los datos de opinión, de manera que pueda ver los resultados en el panel de control **Detalles**.

   Para comprobar inmediatamente el resultado, en la página **Detalles**, seleccione un despliegue, pulse una de las métricas de **Calidad** y a continuación pulse **Comprobar calidad ahora**.
