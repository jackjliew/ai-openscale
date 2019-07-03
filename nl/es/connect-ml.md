---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: payload, non-Watson, machine learning, services, subscription

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

# Registro de carga útil para instancias de servicio que no sean {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #cml-connect}

Si el modelo de inteligencia artificial se despliega en un motor de aprendizaje automático que no es {{site.data.keyword.pm_full}}, debe habilitar el registro de carga útil para el motor de aprendizaje automático externo con un cliente Python.
{: shortdesc}

Consulte información más completa en la [documentación del cliente Python de {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} y en los cuadernos de cliente Python de {{site.data.keyword.aios_short}} que forman parte de las guías de aprendizaje de [{{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}.

## Antes de empezar
{: #cml-prereq}

Deberá tener los datos de entrenamiento del modelo disponibles en Db2 o {{site.data.keyword.cos_full}} para supervisar si el modelo está sesgado. La explicabilidad y la exactitud no están soportadas para las funciones Python. Para obtener más información sobre los datos de entrenamiento, consulte [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- Importe e inicialice {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  Puede encontrar las credenciales siguiendo los pasos que se muestran en el tema "[Creación de credenciales](/docs/services/ai-openscale?topic=ai-openscale-cred-create)".

- Cree un nombre de esquema en la base de datos PostgreSQL

- Configure una despensa de datos

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## Trabajar con el motor de aprendizaje automático personalizado
{: #cml-cusconfig}

### Enlazar el motor de aprendizaje automático personalizado
{: #cml-cusbind}

- Un motor que no es {{site.data.keyword.pm_full}} está enlazado como Personalizado, lo que significa que sólo son metadatos; no hay ninguna
integración directa con el servicio no {{site.data.keyword.pm_full}}. Puede enlazar más de un motor de aprendizaje automático a
{{site.data.keyword.aios_short}} utilizando el método `client.data_mart.bindings.add`.

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Puede ver el enlace de servicio con el mandato siguiente:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Enlace de aprendizaje automático genérico](images/ml-generic-bind.png)

### Añadir suscripción personalizada
{: #cml-cussub}

- Añadir suscripción

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- Obtener lista de suscripciones

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Habilitar registro de carga útil
{: #cml-cusenlog}

- Habilitar el registro de carga útil en la suscripción

    ```python
    subscription.payload_logging.enable()
    ```

- Obtener detalles de registro

    ```python
    subscription.payload_logging.get_details()
    ```

Para obtener más información, consulte [Registro de carga útil]().

### Puntuación y registro de carga útil
{: #cml-cusscore}

- Puntúe el modelo. Para ver un ejemplo completo, consulte [IBM {{site.data.keyword.aios_full}} & Cuaderno del motor de aprendizaje automático personalizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}.

- Almacene la solicitud y respuesta en la tabla de registro de carga útil

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

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

## Trabajar con el motor de Microsoft Azure Machine Learning
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

    binding_uid = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Puede ver el enlace de servicio con el mandato siguiente:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Enlace de aprendizaje automático de Azure](images/ml-azure-bind.png)

### Añadir suscripción de aprendizaje automático de MS Azure
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

- Puntúe el modelo. Para ver un ejemplo completo, consulte el [cuaderno Trabajar el motor de Azure Machine Learning Studio](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

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

## Trabajar con el motor de aprendizaje automático de Amazon SageMaker
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

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

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
{: #cml-next}

- Para continuar con el cliente de {{site.data.keyword.aios_short}}, consulte
[Especificación de una base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db).

- Para continuar con la biblioteca de mandatos de Python, consulte la [documentación del cliente Python](http://ai-openscale-python-client.mybluemix.net/){: external}.
