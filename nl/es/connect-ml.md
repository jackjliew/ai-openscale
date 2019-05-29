---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: payload, non-Watson, machine learning, services, subscription

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Registro de carga útil para instancias de servicio que no sea Watson Machine Learning
{: #cml-connect}

Si el modelo de inteligencia artificial se despliega en un motor de aprendizaje automático que no es Watson Machine Learning (WML), debe habilitar el registro de carga útil para el motor de aprendizaje automático externo con un cliente Python.
{: shortdesc}

Consulte información más completa en la [documentación del cliente Python de {{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://ai-openscale-python-client.mybluemix.net/){: new_window} y en los cuadernos de cliente Python de {{site.data.keyword.aios_short}} que forman parte de las guías de aprendizaje de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: new_window}.

## Antes de empezar
{: #cml-prereq}

Deberá tener los datos de entrenamiento del modelo disponibles en Db2 o Cloud Object Storage para supervisar si el modelo está sesgado. La explicabilidad y la exactitud no están soportadas para las funciones Python. Para obtener más información sobre los datos de entrenamiento, consulte [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

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

### Enlace su motor de aprendizaje automático personalizado
{: #cml-cusbind}

- Un motor no WML se enlaza como personalizado, lo que significa que es sólo metadatos, no hay ninguna integración directa con el servicio no WML.

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

### Puntuación y registro de carga útil
{: #cml-cusscore}

- Puntúe el modelo. Para ver un ejemplo completo, consulte [IBM {{site.data.keyword.aios_full}} & Cuaderno del motor de aprendizaje automático personalizado ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

- Almacene la solicitud y respuesta en la tabla de registro de carga útil

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **Nota**: Para los lenguajes que no sean Python, también puede realizar directamente el registro de carga útil, mediante una API REST.

    ```json
    token_endpoint = "https://iam.bluemix.net/identity/token"
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

## Trabajar con el motor de aprendizaje automático de Microsoft Azure
{: #cml-azconfig}

### Enlazar el motor de aprendizaje automático de MS Azure
{: #cml-azbind}

- Un motor no WML se enlaza como personalizado, lo que significa que es sólo metadatos, no hay ninguna integración directa con el servicio no WML.

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

- Puntúe el modelo. Para ver un ejemplo completo, consulte [Trabajar con el cuaderno del motor de Azure Machine Learning Studio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

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
    token_endpoint = "https://iam.bluemix.net/identity/token"
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

### Enlazar el motor de aprendizaje automático de AWS SageMaker
{: #cml-smbind}

- Un motor no WML se enlaza como personalizado, lo que significa que es sólo metadatos, no hay ninguna integración directa con el servicio no WML.

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

- Puntúe el modelo. Para ver un ejemplo completo, consulte [Trabajar con el cuaderno del motor de aprendizaje automático de SageMaker ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

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
    token_endpoint = "https://iam.bluemix.net/identity/token"
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

- Para continuar con la biblioteca de mandatos de Python, consulte la [documentación del cliente Python ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://ai-openscale-python-client.mybluemix.net/){: new_window}.
