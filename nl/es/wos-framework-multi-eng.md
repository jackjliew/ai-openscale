---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: multiple engines, non-Watson, machine learning, frameworks, provision

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

# Soporte para varios motores de aprendizaje automático
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} da soporte a varios motores de aprendizaje automático en una única instancia. Puede suministrarlos mediante la configuración del panel de control de {{site.data.keyword.aios_short}} o el [SDK de Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).
{: shortdesc}

Cuando configuró por primera vez {{site.data.keyword.aios_short}}, es posible que utilizara la interfaz de usuario o la opción de configuración
automática para suministrar el primer motor de aprendizaje automático. Añadir motores de aprendizaje automático requiere que se utilice la pestaña de configuración en el panel de control de {{site.data.keyword.aios_short}} o el SDK de Python.

## Utilización del panel de control para añadir proveedores
{: #fmrk-workaround-multmleng-dashboard}

1. Una vez que haya abierto {{site.data.keyword.aios_short}}, desde la pestaña **Configurar**, pulse los botones **Añadir proveedores de aprendizaje automático**.

   ![Se muestra el botón Añadir proveedores en la ventana de proveedores de aprendizaje automático](images/wos-configure-multi-providers.png)

2. Pulse el mosaico del proveedor que desee añadir y pulse **Siguiente**.

   ![Se muestra la pantalla de selección de proveedores de aprendizaje automático](images/wos-machine-learning-providers-selection.png)

3. Especifique la información necesaria, como las credenciales, y pulse **Guardar**.

Una vez que ha guardado la configuración, se le ofrece la opción de ir al panel de control, elegir los despliegues o configurar los supervisores.

## Edición de proveedores de aprendizaje automático
{: #fmrk-workaround-editingproviders-dashboard}

¿Necesita editar un proveedor de aprendizaje automático? Pulse el menú de mosaicos ![Icono del menú de mosaicos](images/v-three-dots.png) y a continuación pulse **Ver y editar detalles**.

   ![Se muestra la opción para ver y editar los proveedores de aprendizaje automático](images/wos-machine-learning-providers-edit.png)

## Adición de proveedores de aprendizaje automático mediante el método de enlace del SDK de Python
{: #fmrk-workaround-multmleng-binding}

Puede enlazar más de un motor de aprendizaje automático a {{site.data.keyword.aios_short}} utilizando el método de la API de Python API `client.data_mart.bindings.add`. 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- Para enlazar el motor de aprendizaje automático de {{site.data.keyword.pm_full}}, ejecute el mandato siguiente:

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- Para enlazar el motor de aprendizaje automático de Azure ML Studio, ejecute el mandato siguiente:

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon Sagemaker
{: #fmrk-workaround-multmleng-binding-aws}

- Para enlazar el motor de aprendizaje automático de AWS Sagemaker, ejecute el mandato siguiente:

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

### Microsoft Azure ML Service
{: #fmrk-workaround-multmleng-binding-azureservice}

- Para enlazar el motor de aprendizaje automático de Azure ML Service, ejecute el mandato siguiente:

  `binding_uid_4 = client.data_mart.bindings.add('My Azure ML Service engine', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### Elaboración de una lista de proveedores de aprendizaje automático
{: #fmrk-workaround-multmleng-binding-list}

Para ver una lista de todos los enlaces, ejecute el método `list`:

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | My Azure ML Service engine | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tabla 1. Enlaces de servicio" caption-side="top"}


Para obtener información sobre los motores de aprendizaje automático específicos, consulte los temas siguientes:

- [Enlazar el motor de aprendizaje automático
personalizado](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind).
- [Enlazar el motor de aprendizaje automático de Microsoft Azure Studio](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [Enlazar el mtor de aprendizaje automático de Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [Enlazar el motor de aprendizaje automático de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


Para ver un ejemplo práctico de un cuaderno real, consulte [los cuadernos de ejemplo de {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

