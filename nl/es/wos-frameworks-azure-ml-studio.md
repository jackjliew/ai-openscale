---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

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

# Infraestructuras de Microsoft Azure ML Studio
{: #frmwrks-azure}

Puede utilizar Microsoft Azure ML Studio para realizar el registro de carga útil y el registro de opiniones, y para medir la exactitud del rendimiento, la detección de sesgos en tiempo de ejecución, la explicabilidad y la función de eliminación automática de sesgo en {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} da completo soporte a las siguientes infraestructuras de Microsoft Azure Machine Learning Studio:
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Nativa | Clasificación | Estructurados |
| Nativa | Regresión | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

## Adición de Microsoft Azure ML Studio a {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

Puede configurar {{site.data.keyword.aios_short}} para que funcione con Microsoft Azure ML Studio utilizando uno de los métodos siguientes:

- Si es la primera vez que añade un proveedor de aprendizaje automático a {{site.data.keyword.aios_short}}, puede utilizar la interfaz de configuración. Para obtener más información, consulte [Especificación de una instancia de Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Debe utilizar este método si desea tener más de un proveedor. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de Microsoft Azure Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


## Cuadernos de ejemplo
{: #frmwrks-azure-smpl-ntbks}

Los cuadernos siguientes muestran cómo trabajar con Microsoft Azure ML Studio:

- [Creación de la despensa de datos, supervisión del despliegue del modelo y análisis de datos](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Ejemplos de puntuación de modelos de MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Explorar más
{: #frmwrks-azure-mediumblogs}

-[Supervisar aprendizaje automático de Azure con Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [¿En qué se diferencia el aprendizaje automático de Azure de Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Utilizar un modelo de aprendizaje automático de Azure desplegado como un servicio web](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## Especificación de una instancia de Microsoft Azure ML Studio
{: #connect-azure}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de Microsoft Azure ML Studio. La instancia de Azure ML Studio es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de Microsoft Azure Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

### Conecte su instancia de Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de Azure ML Studio.

1.  En la pestaña **Configurar**, en el panel de navegación, pulse **Proveedores de aprendizaje automático**.

    ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

1.  Pulse el botón **Añadir proveedores de aprendizaje automático** y a continuación pulse el mosaico **Microsoft Azure ML Studio**.

    ![Especificar credenciales de Azure ML Studio](images/connect-azure-cred.png)

1.  Especifique y guarde sus credenciales:

    - ID de cliente: el valor de serie real del ID de cliente, que verifica quién es y autentica y autoriza las llamadas que realiza a Azure Studio.
    - Secreto de cliente: el valor de serie real del secreto, que verifica quién es y autentica y autoriza las llamadas que realiza a Azure Studio.
    - Inquilino: el ID de inquilino correspondiente a su organización y que es una instancia dedicada de Azure AD. Para encontrar el ID de inquilino, pase el puntero del ratón por el nombre de cuenta para obtener el ID de inquilino o directorio, o bien seleccione Azure Active Directory > Propiedades > ID de directorio en el portal de Azure.
    - ID de suscripción: las credenciales de suscripción identifican de forma exclusiva su suscripción de Microsoft Azure. El ID de suscripción forma parte del URI para cada llamada de servicio.

    Consulte [Cómo utilizar el
portal para crear una entidad de servicio y una aplicación de Azure AD que puedan acceder a recursos](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} para ver instrucciones sobre
cómo obtener sus credenciales de Microsoft Azure.
    {: note}

1.  {{site.data.keyword.aios_short}} lista sus modelos desplegados; seleccione los que desee supervisar y pulse **Configurar**.

Ha seleccionado correctamente los despliegues.

## Registro de carga útil con el motor de aprendizaje automático de Microsoft Azure
{: #cml-azconfig}

### Enlazar el motor de Microsoft Azure Machine Learning
{: #cml-azbind}

- Un motor que no es {{site.data.keyword.pm_full}} está enlazado como Personalizado, lo que significa que sólo son metadatos; no hay ninguna
integración directa con el servicio no {{site.data.keyword.pm_full}}.

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Puede ver el enlace de servicio con el mandato siguiente:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Enlace de aprendizaje automático de Azure](images/ml-azure-bind.png)

### Añadir suscripción de Microsoft Azure ML Studio
{: #cml-azsub}

- Añadir suscripción

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Obtener lista de suscripciones

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Habilitar registro de carga útil
{: #cml-azenlog}

- Habilitar el registro de carga útil en la suscripción

    ```python
    subscription.payload_logging.enable()
    ```

- Obtener detalles de registro

    ```python
    subscription.payload_logging.get_details()
    ```

### Puntuación y registro de carga útil
{: #cml-azscore}

- Puntúe el modelo. Para ver un ejemplo completo, consulte el [cuaderno Trabajar con el motor de Azure Machine Learning Studio](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

- Almacene la solicitud y respuesta en la tabla de registro de carga útil:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Nota**: Para los lenguajes que no sean Python, también puede realizar directamente el registro de carga útil, mediante una API REST.

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```


## Pasos siguientes
{: #ca-next}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
