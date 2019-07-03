---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

En esta guía de aprendizaje, realice los pasos siguientes:

- [Suministrar servicios de aprendizaje automático y
almacenamiento de {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps).
- [Configurar un proyecto de Watson Studio y crear, entrenar y desplegar un modelo de aprendizaje automático](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup).
- [Configurar y explorar confianza, transparencia y
explicabilidad para el modelo](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios).

## Suministrar servicios de {{site.data.keyword.Bluemix_notm}} de requisito previo
{: #gs-prps}

Además de {{site.data.keyword.aios_short}}, para completar esta guía de aprendizaje, necesita las cuentas y servicios siguientes.

**Importante**: Para obtener el mejor rendimiento, se recomienda que los servicios de requisito previo se creen en la misma región
que {{site.data.keyword.aios_short}}. Para ver las ubicaciones disponibles para {{site.data.keyword.aios_short}}, consulte
[Disponibilidad de servicios](/docs/resources?topic=resources-services_region).

1.  Inicie una sesión en su cuenta de [{{site.data.keyword.Bluemix_notm}} ](https://{DomainName}){: external}
con {{site.data.keyword.ibmid}}.
1.  Para cada uno de los servicios siguientes que todavía no ha asociado a su cuenta, cree una instancia pulsando el enlace, asignando un nombre al
servicio, seleccionando el plan (gratuito) **Lite** y pulsando el botón **Crear**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Configurar un proyecto de Watson Studio
{: #gs-setup}

1.  Inicie la sesión en la cuenta de [Watson Studio](https://dataplatform.ibm.com/){: external} y empiece creando un nuevo
proyecto. Seleccione **Nuevo proyecto**.

    ![Crear proyecto de Watson Studio](images/studio_create_proj.png)

1.  Seleccione el mosaico **Standard**.

    ![Seleccionar proyecto Standard de Watson Studio](images/studio_create_standard.png)

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

    ![Nuevo formulario de cuaderno](images/credit-sample-model.png)

### Despliegue el modelo `Riesgo crediticio`
{: #gs-depmod}

1.  En la página de modelo `Riesgo crediticio`, pulse la pestaña **Despliegues** y, a continuación, pulse
**Añadir despliegue**.
1.  Especifique `credit-risk-deploy` como nombre del despliegue y seleccione el tipo de despliegue **Servicio web**.
1.  Pulse **Guardar**.

## Configure {{site.data.keyword.aios_short}}
{: #gs-confaios}

### Suministro de {{site.data.keyword.aios_short}}
{: hide-dashboard}
{: #gs-provaios}

1.  [Suministre una nueva instancia de servicio de {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/openscale.png)

2.  Proporcione un nombre a su servicio, seleccione el **Plan Lite** y pulse **Crear**.

### Conecte {{site.data.keyword.aios_short}} al modelo de aprendizaje automático
{: #gs-ctmod}

Ahora que el modelo de aprendizaje automático se ha desplegado, puede configurar {{site.data.keyword.aios_short}} para garantizar la confianza y transparencia con sus modelos.

1.  Seleccione la pestaña **Gestionar** de la instancia de {{site.data.keyword.aios_short}} y pulse el botón **Iniciar aplicación**. Se
abrirá la página de demostración **Bienvenido a {{site.data.keyword.aios_short}}**.
2. Para esta guía de aprendizaje, pulse **No gracias** y, a continuación, pulse **Empezar**.

1.  Pulse el mosaico **Watson Machine Learning**.

1.  Para esta guía de aprendizaje, seleccione la instancia de {{site.data.keyword.pm_full}} en el menú y pulse
**Siguiente**.

    También tiene la opción de seleccionar una ubicación de {{site.data.keyword.pm_short}} distinta. Consulte [Especificación de una instancia de servicio de {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-wml-connect) para obtener información adicional.
    {: note}

    ![Establecer instancia de {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

1.  Ahora puede seleccionar los modelos desplegados que supervisará {{site.data.keyword.aios_short}}. Seleccione el modelo que ha creado y desplegado y pulse **Siguiente**.

    ![Seleccionar modelos desplegados](images/gs-set-deploy0.png)

1.  A continuación, debe elegir una base de datos. Tiene dos opciones: la base de datos gratuita o una base de datos nueva o existente. Para esta guía de aprendizaje, seleccione el mosaico **Utilizar la base de datos gratuita alojada por {{site.data.keyword.aios_short}}**.

    La base de datos gratuita tiene algunas limitaciones importantes. Es una base de datos alojada que no le proporciona acceso individual a ella. Proporciona a {{site.data.keyword.aios_short}} acceso a su base de datos y sus datos. No es compatible con el GDPR. Consulte toda la información detallada sobre cada una de estas opciones en el tema [Especificación de una base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db). La base de datos existente puede ser una base de datos PostgreSQL o una base de datos Db2.
    {: tip}

    ![Seleccionar base de datos](images/gs-set-lite-db2.png)

1.  Revise los datos de resumen y pulse **Guardar**. Confirme y, cuando se le solicite, pulse el botón **Continuar con la configuración**.

    Se lista también un ID de despensa de datos, que coincide con el ID de instancia de {{site.data.keyword.aios_short}}.
    {: tip}

    ![Vista de resumen](images/gs-setup-summary4.png)

1.  Su pantalla podría ser similar a la siguiente captura de pantalla. Puesto que utilizará un método de la GUI para puntuar sus datos, seleccione simplemente el botón **Configurar supervisores** para completar esta configuración.

    ![Código de solicitud de puntuación](images/gs-config-send-scoring.png)

### Proporcione un conjunto de datos de ejemplo al modelo
{: #gs-samp}

Para configurar sus supervisores, primero debe generar al menos una solicitud de puntuación para el modelo a fin de generar registro de carga útil que puedan consumir los supervisores. En esta sección, proporcionaremos datos de ejemplo en forma de un archivo JSON para generar una solicitud de puntuación.

1.  Descargue el archivo
[credit_payloadload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  En la pestaña **Despliegues** del proyecto de Watson Studio, pulse el enlace **credit-risk-deploy** **Probar** y seleccione el icono de entrada de JSON.

    ![Prueba de JSON](images/json_test02.png)

1.  Ahora, abra el archivo `credit_payload_data.json` que ha descargado y copie el contenido en el campo JSON de la pestaña **Probar**. Pulse el botón **Predecir** para enviar y puntuar cargas útiles de entrenamiento al modelo.

    ![Predicción de JSON](images/json_test03.png)

### Preparación para la supervisión
{: #gs-prepmon}

1.  Ahora, en la instancia de {{site.data.keyword.aios_short}}, seleccione el despliegue y pulse **Empezar**.

    ![Seleccionar despliegue](images/config-select-deploy2.png)

1.  Especifique la característica que contiene la respuesta que predecirá el modelo. (En la base de datos, ¿qué columna de la tabla contiene las etiquetas o los valores de predicción?) En este caso, el modelo predice el riesgo crediticio, así que seleccione la columna **Riesgo** y pulse **Siguiente**.

    ![Preparar para supervisión](images/config-prep-monitor.png)

1.  A continuación proporcionará información sobre el modelo y los datos de entrenamiento. Pulse **Siguiente**.

    ![Preparar explicación](images/config-what-monitor.png)

1.  En el menú **Tipo de datos**, seleccione **Numérico/categórico** como el tipo de datos que analiza su despliegue, y pulse **Siguiente**.

    ![Seleccionar tipo de entrada](images/config-input-monitor.png)

1.  Para datos numéricos o categóricos, debe proporcionar información sobre los datos de entrenamiento de su modelo para configurar los supervisores. Seleccione **Configurar manualmente los supervisores** para proporcionar información sobre los datos de entrenamiento.

    ![Seleccionar tipo de configuración](images/config-manual-monitor.png)

1.  El tipo de algoritmo es importante para supervisar las métricas del modelo, como por ejemplo la exactitud. Puesto que la predicción del modelo puede ser "Riesgo" o "Sin riesgo", seleccione el [tipo de algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) **Clasificación binaria** y pulse **Siguiente**.

    ![Binario](images/binary.png)

1.  La información de ubicación de los datos de ejemplo está precompletada en la pantalla siguiente. Seleccione **Siguiente** para continuar.

    ![Página Especificar ubicación de Db2 de datos de entrenamiento](images/gs-config-train-db2-monitor.png)

1.  El esquema y la tabla aparecen también precompletados. Pulse **Siguiente** para continuar.

    ![Especificar ubicación de Db2 de la tabla de esquema y entrenamiento](images/gs-fair-config-table-db2.png)

1.  Ahora, debe especificar la característica que contiene las respuestas que predecirá el modelo (en otras palabras, en la base de datos, qué columna de la tabla contiene valores de predicción (etiquetas)). En este caso, el modelo predecirá el riesgo crediticio, así que seleccione la columna **Riesgo** y pulse **Siguiente**.

    La base de datos de entrenamiento tiene los valores que ha proporcionado para entregar su modelo.
    {: note}

    ![Predecir entrada de etiqueta](images/gs-config-label.png)

1.  Seleccione las columnas utilizadas para entregar el modelo. Estos son los datos que el despliegue del modelo espera en una solicitud. Todas las columnas de datos excepto `_training` son entradas para el modelo. Seleccione todas las otras entradas y pulse **Siguiente**.

    ![Entradas de explicabilidad](images/explain_inputs1.png)

1.  Para datos categóricos, debe identificar las columnas que ahora contienen enteros, pero que originalmente contenían valores de texto. Seleccione los valores que se muestran aquí.

    ![Entradas de explicabilidad](images/config_categories.png)

1.  Revise el resumen de las selecciones, pulse **Guardar** y a continuación pulse **Aceptar**.

### Configurar la supervisión de equidad
{: #gs-cfgfair}

1.  Pulse **Equidad**.

1.  Lea sobre la equidad y pulse **Siguiente**. Para obtener más información, consulte [Equidad](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

1.  Ahora puede elegir qué características supervisar para la equidad. Para cada característica que seleccione, {{site.data.keyword.aios_short}} supervisará la propensión del modelo desplegado a un resultado favorable para un grupo sobre otro. En este ejemplo, supervisaremos las características **Sexo** y **Edad**.

    Las características se supervisan individualmente, pero cualquier sesgo corregirá los problemas de todas las características a la vez. Pulse los mosaicos **Sexo** y **Edad** y pulse **Siguiente**.

1.  {{site.data.keyword.aios_short}} sirve para detectar el sesgo para un grupo supervisado en comparación con un grupo de referencia. Para la característica **Sexo**, añada el valor `hombre` al **Grupo de referencia** y el valor `mujer` al **Grupo supervisado** y pulse **Siguiente**.

    El modelo se marcará como sesgado para **Sexo** si las proporciones de predicción de riesgo para el grupo supervisado difieren de las proporciones para el grupo de referencia. Por lo tanto, si el modelo predice Riesgo para los clientes hombre el 60% del tiempo, y para los clientes mujer el 20% del tiempo, está sesgado.

    ![Grupos por sexo](images/gender_groups1.png)

1.  Asigne un umbral de equidad para **Sexo**. El panel de instrumentos de operaciones muestra una alerta si la calificación de
imparcialidad excede el umbral que ha establecido. Establezca el umbral en el 90% y pulse **Siguiente**.

1.  Para la característica **Edad**, añada los valores `26-74` al **Grupo de referencia**, y los valores `19-25` al **Grupo supervisado** y pulse **Siguiente**.

    De la misma forma que con **Sexo**, el modelo se marcará como sesgado para **Edad** si las proporciones de predicción de riesgo para el grupo supervisado difieren de las proporciones para el grupo de referencia. Por lo tanto, si los clientes cuya edad está entre 26 y 74 reciben una predicción de riesgo con una proporción distinta que los clientes cuya edad está entre 19 y 25, el modelo está sesgado.

    ![Grupos de BP](images/age_groups.png)

1.  Establezca el umbral para **Edad** en el 90% y pulse **Siguiente**.

1.  Arrastre y suelte los valores del campo **Valores de datos de entrenamiento** a los campos **Valores favorables** y **Valores desfavorables**. Para esta guía de aprendizaje, el valor favorable es **Sin riesgo** y el valor no favorable es **Riesgo**. Pulse **Siguiente**.

    {{site.data.keyword.aios_short}} detecta automáticamente qué columna de la base de datos de registro de carga útil contiene los valores de predicción, y los presenta en el campo **Valores de datos de entrenamiento**. Tenga en cuenta que mientras que la base de datos de entrenamiento tiene valores que ha proporcionado para entrenar su modelo, la base de datos de registro de carga útil contiene datos de opinión recopilados durante la ejecución del modelo, que a continuación se pueden utilizar para volver a entrenar y desplegar de nuevo el modelo.
    {: note}

    ![Valores positivos y negativos](images/pos_and_neg2.png)

1.  Utilice el graduador para ajustar el tamaño mínimo de la muestra a 100, y a continuación pulse **Siguiente**.

    ![Tamaño mínimo](images/gs-fair-config-sample.png)

    Para esta guía de aprendizaje, el tamaño mínimo de la muestra se establece en 100. Normalmente se recomienda un tamaño mayor de la muestra para garantizar que su tamaño no es demasiado pequeño, lo que podría causar desviaciones en los resultados.
    {: note}

1.  Revise sus opciones, pulse **Guardar** y a continuación **Aceptar**.

    ![Resumen de la configuración](images/fair-summary.png)

    Aparece la ventana siguiente, que proporciona un punto final de puntuación sesgado. Puesto que esta guía de aprendizaje utiliza el método de la GUI y no la CLI para puntuar los datos, para continuar pulse **Aceptar**.

    ![API para eliminar el sesgo](images/gs-insight-debias-api.png)

### Configurar la supervisión de la exactitud
{: #gs-cfgac}

1.  Pulse **Exactitud**.

1.  Lea sobre la exactitud y pulse **Siguiente**. Para obtener más información, consulte [Exactitud](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

1.  Establezca el umbral de alerta de exactitud en 90% y pulse **Siguiente**.

1.  En la pantalla siguiente, utilice el graduador para ajustar el tamaño mínimo de la muestra a 10, y a continuación pulse  **Siguiente**.

    Para esta guía de aprendizaje, el tamaño mínimo de la muestra se ha establecido en 10. Normalmente se recomienda un tamaño mayor de la muestra para garantizar que su tamaño no es demasiado pequeño, lo que podría causar desviaciones en los resultados.
    {: note}

1.  Para el tamaño máximo de la muestra, utilice 10000. Pulse **Siguiente**.

1.  Revise sus opciones, pulse **Guardar** y a continuación **Aceptar**.

1.  Finalmente, se le presenta una opción para añadir datos de opinión, que se tratan en la siguiente sección. Por ahora, cierre la ventana pulsando **Aceptar**, sin pulsar el botón **Añadir datos de opinión**.

    Para obtener más información, consulte [Configuración del supervisor de exactitud](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config).

## Proporcione un conjunto de datos de opinión de muestra al modelo
{: #gs-smpfeed}

Para habilitar la supervisión de la exactitud, debe proporcionar al modelo los datos de opinión. Hasta que no se hace esto, los datos de exactitud no aparecen en el panel de control. Puede generar todas las solicitudes a la vez añadiendo datos de opinión de muestra al modelo para la puntuación. Para esta tarea, descargará un archivo CSV que contiene datos de opinión de muestra.

1.  Descargue el archivo
[credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv).

1.  En {{site.data.keyword.aios_short}}, pulse la pestaña **Detalles**.

    ![Detalles](images/insight-dash-tab.png)

1.  Pulse el mosaico para el modelo desplegado.

    ![Pestaña Detalles - Sin datos](images/gs-insight-overview.png)

1.  A continuación, pulse el icono Editar para editar la configuración de despliegue.

    ![Se muestra el icono Editar](images/gs-insight-edit-icon.png)

1.  En el panel lateral Resumen, pulse el botón **Añadir datos de opinión** y seleccione el archivo `credit_feedback_data.csv` que ha descargado. Seleccione el delimitador **Coma (,)** y a continuación pulse **Aceptar**.

    Los tamaños de archivo están actualmente limitados a 8 MB.
    {: note}

    ![Delimitador de exactitud](images/accuracy-delimit.png)

    La adición del archivo CSV proporciona datos de opinión al modelo.

    ![Panel de resumen](images/gs-insight-summary-panel-2.png)

## Visualización de los resultados
{: #gs-viewres}

La comprobación de exactitud se ejecuta una hora después de haber configurado la supervisión de la exactitud. En un sistema de producción, esto tiene sentido, ya que el panel de control puede acumular datos de opinión. Para los fines de esta guía de aprendizaje, probablemente deseará desencadenar manualmente la comprobación de exactitud después de añadir los datos de opinión, de manera que pueda ver los resultados en el panel de control **Detalles**.

Para comprobar inmediatamente el resultado, en la página **Detalles**, seleccione un despliegue y a continuación pulse el botón **Comprobar equidad ahora** o **Comprobar calidad ahora**.

### Ver detalles del despliegue
{: #gs-viewin}

1. [En el panel de control de {{site.data.keyword.aios_short}}](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external},
pulse la pestaña **Detalles**.

  ![Detalles](images/insight-dash-tab.png)

1. Consulte en la página Detalles una descripción general de las métricas de sus modelos desplegados. Puede ver alteras para métricas de equidad o
exactitud que superan el umbral del 90%.

  Las métricas de Equidad y Exactitud pueden tardar hasta una hora en mostrarse.
  {: tip}

  ![Descripción general de Detalles](images/insight-overview.png)

### Ver datos de supervisión del despliegue
{: #gs-viewmon}

1.  Seleccione un despliegue pulsando el mosaico en la página Detalles. Se muestran los datos de supervisión de ese despliegue. Nota: Después de subir el archivo .csv de opinión, es posible que se encuentre con que los datos de Equidad o Exactitud no se han actualizado. Para comprobar inmediatamente el resultado, pulse el botón **Comprobar equidad ahora** o **Comprobar calidad ahora**.
1.  Deslice el marcador por el gráfico para seleccionar datos del periodo de tiempo durante el que ha ejecutado los datos de muestra y los datos de opinión de muestra. A continuación, pulse **Ver detalles**.

    ![Supervisar datos](images/insight-monitor-data.png)

1.  A continuación, revise en los gráficos los datos que ha supervisado. Para este ejemplo, utilice el menú **Característica** para seleccionar `Edad` o `Sexo` para ver detalles sobre los datos supervisados.

    Consulte [Visualización de datos de una hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) para obtener más información sobre cómo leer estos gráficos.
    {: tip}

    ![Descripción general de Detalles](images/insight-review-charts.png)

### Vea la explicabilidad de una transacción de modelo
{: #gs-viewextx}

1.  Pulse el botón **Ver transacciones** de los gráficos para los datos que ha supervisado.

    ![Ver transacciones](images/view_transactions.png)

1.  Aparece una lista de las transacciones que han contribuido al sesgo durante la última hora. Para ver una explicación más detallada de una transacción determinada, en la columna **ACCIÓN** pulse **Explicar**.

    ![Lista de transacciones](images/transaction_list_cr.png)
    
1.  Se muestra una explicación de cómo el modelo ha llegado a esta conclusión. Esta explicación incluye el grado de seguridad del modelo, los factores que han contribuido al nivel de confianza y las columnas con las que se ha alimentado el modelo.

    ![Ver transacción](images/view_transaction1.png)

## Información relacionada
{: #wos-info}

- Para obtener información sobre sesgos, consulte [Equidad](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor).
- Para obtener información sobre la exactitud con la que el modelo predice los resultados, consulte [Exactitud](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- Para obtener más información sobre cómo interpretar los gráficos, datos y transacciones, consulte [Supervisión de la equidad, solicitudes promedio por minuto y exactitud](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).
