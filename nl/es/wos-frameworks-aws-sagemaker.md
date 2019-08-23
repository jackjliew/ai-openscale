---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Infraestructuras de Amazon SageMaker
{: #frmwrks-aws-sage}

Puede utilizar Amazon SageMaker para realizar el registro de carga útil y el registro de opiniones, y para medir la exactitud del rendimiento, la detección de sesgos en tiempo de ejecución, la explicabilidad y la función de eliminación automática de sesgo en {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} da completo soporte a las siguientes infraestructuras de Amazon SageMaker:
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Nativa | Clasificación | Estructurados |
| Nativa | Regresión<sup>1</sup> | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

<sup>1</sup>El soporte de la regresión no incluye la magnitud de la desviación.

## Adición de Amazon SageMaker a {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

Puede configurar {{site.data.keyword.aios_short}} para que funcione con Amazon SageMaker utilizando uno de los métodos siguientes:

- Si es la primera vez que añade un proveedor de aprendizaje automático a {{site.data.keyword.aios_short}}, puede utilizar la interfaz de configuración. Para obtener más información, consulte [Especificación de una instancia de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Debe utilizar este método si desea tener más de un proveedor. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de aprendizaje automático de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Cuadernos de ejemplo
{: #frmwrks-aws-sage-smpl-ntbks}

Los cuadernos siguientes muestran cómo trabajar con Amazon SageMaker:

- [Creación y despliegue de un modelo de predicción de riesgo crediticio](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Creación de la despensa de datos, supervisión del despliegue del modelo y análisis de datos](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## Especificación de una instancia de servicio de Amazon SageMaker ML
{: #csm-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de servicio de Amazon SageMaker. La instancia de servicio de Amazon SageMaker es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de aprendizaje automático de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

### Conecte su instancia de servicio de Amazon SageMaker
{: #csm-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de servicio de Amazon SageMaker.

1.  En la pestaña **Configurar**, en el panel de navegación, pulse **Proveedores de aprendizaje automático**.

    ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

1.  Pulse el botón **Añadir proveedor de aprendizaje automático** y, a continuación, pulse el mosaico **Amazon SageMaker**.

    ![Especificar las credenciales de servicio de Amazon SageMaker](images/connect-sage-cred.png)

1.  Especifique y guarde sus credenciales:

    - ID de clave de acceso: el ID de clave de acceso de AWS, `aws_access_key_id`, que verifica quién es y autentica y autoriza las llamadas que realiza a AWS.
    - Clave de acceso secreta: su clave de acceso secreta de AWS, `aws_secret_access_key`, que se requiere para verificar quién es y para autenticar y autorizar las llamadas que realiza a AWS.
    - Región: especifique la región donde se ha creado su ID de clave de acceso. Las claves se almacenan y utilizan en la región en la que se han creado y no se pueden transferir a otra región. 

1.  {{site.data.keyword.aios_short}} lista sus modelos desplegados; seleccione los que desee supervisar.

## Registro de carga útil con el motor de aprendizaje automático de Amazon SageMaker
{: #cml-smconfig}

### Enlazar el motor de aprendizaje automático de Amazon SageMaker
{: #cml-smbind}

- Un motor que no es {{site.data.keyword.pm_full}} está enlazado como Personalizado, lo que significa que sólo son metadatos; no hay ninguna
integración directa con el servicio no {{site.data.keyword.pm_full}}.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Puede ver el enlace de servicio con el mandato siguiente:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Enlace de aprendizaje automático de SageMaker](images/ml-sagemaker-bind.png)

### AÑadir suscripción de aprendizaje automático de Amazon SageMaker
{: #cml-smsub}

- Añadir suscripción

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
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
{: #cml-smenlog}

- Habilitar el registro de carga útil en la suscripción

    ```python
    subscription.payload_logging.enable()
    ```

- Obtener detalles de registro

    ```python
    subscription.payload_logging.get_details()
    ```

### Puntuación y registro de carga útil
{: #cml-smscore}

- Puntúe el modelo. Para ver un ejemplo completo, consulte el [cuaderno Trabajar con el motor de aprendizaje automático de SageMaker](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}.


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
{: #csm-next}

- {{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [Supervisar el aprendizaje automático de Sagemaker con Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
