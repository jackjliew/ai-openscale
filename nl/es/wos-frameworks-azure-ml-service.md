---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Infraestructuras de Microsoft Azure ML Service
{: #frmwrks-azure-service}

Puede utilizar Microsoft Azure ML Service para realizar el registro de carga útil y el registro de opiniones, y para medir la exactitud del rendimiento, la detección de sesgos en tiempo de ejecución, la explicabilidad y la función de eliminación automática de sesgo en {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} da soporte completo a las siguientes infraestructuras de Microsoft Azure Machine Learning Service:
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Nativa | Clasificación | Estructurados |
| scikit-learn | Clasificación | Estructurados |
| scikit-learn | Regresión | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

## Adición de Microsoft Azure ML Service a {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

Puede configurar {{site.data.keyword.aios_short}} para que funcione con Microsoft Azure ML Service utilizando uno de los métodos siguientes:

- Si es la primera vez que añade un proveedor de aprendizaje automático a {{site.data.keyword.aios_short}}, puede utilizar la interfaz de configuración. Para obtener más información, consulte [Especificación de una instancia de Microsoft Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice).
- También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Debe utilizar este método si desea tener más de un proveedor. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de Microsoft Azure Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).


{{site.data.keyword.aios_short}} llama a distintos puntos finales REST necesarios para interactuar con Azure ML Service. Para ello, debe enlazar Azure Machine Learning Service {{site.data.keyword.aios_short}}.

1. Cree un principal de Azure Active Directory Service.
2. Especifique los detalles de las credenciales al añadir el enlace de servicio de Azure ML Service, mediante la interfaz de usuario o el SDK de Python de {{site.data.keyword.aios_short}}.

## Requisitos de los archivos de solicitud y respuesta JSON
{: #frmwrks-azureservice-JSON}

Para que {{site.data.keyword.aios_short}} funcione con Azure ML Service, los despliegues de servicio web que cree deben cumplir determinados requisitos. Los despliegues de servicio web que cree deben aceptar solicitudes JSON y devolver respuestas JSON, según los requisitos que se describen a continuación.

### Formato de solicitud JSON de servicio web necesario
{: #frmwrks-azureservice-JSON-sample-request}

- El cuerpo de la solicitud de API REST debe ser un documento JSON que contenga una sola matriz JSON de objetos JSON
- El nombre de la matriz JSON debe ser `"input"`.
- Cada objeto JSON sólo puede incluir pares de clave-valor simples, donde los valores sólo pueden ser una serie, un número, `true`, `false` o `null`
- Los valores no pueden ser un objeto o matriz JSON
- Todos los objetos JSON de la matriz deben tener especificadas las mismas claves (y por lo tanto número de claves), independientemente de si hay o no un valor distinto de `null` disponible


El siguiente archivo JSON de ejemplo cumple los requisitos anteriores y se puede utilizar como plantilla para crear sus propios archivos de solicitud JSON:


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### Formato de respuesta JSON de servicio web necesario
{: #frmwrks-azureservice-JSON-sample-response}

Tome nota de las consideraciones siguientes al crear un archivo de respuesta JSON:

- El cuerpo de respuesta de API REST debe ser un documento JSON que contenga una matriz JSON de objetos JSON
- El nombre de la matriz JSON debe ser `"output"`.
- Cada objeto JSON puede incluir sólo pares de clave-valor, donde los valores pueden ser una serie, un número, `true`, `false`, `null` o una matriz que no contenga otros objetos o matrices JSON
- Los valores no pueden ser un objeto JSON
- Todos los objetos JSON de la matriz deben tener especificadas las mismas claves (y número de claves), independientemente de si hay valores distintos de `null` disponibles
- Para modelos de clasificación: el servicio web debe devolver una matriz de probabilidades para cada clase y la ordenación de las probabilidades debe ser coherente para cada objeto JSON de la matriz
  - Ejemplo: supongamos que tiene un modelo de clasificación binaria que predice el riesgo crediticio, donde las clases son `Riesgo` o `Sin riesgo`
  - Para cada resultado devuelto en la matriz "output", los objetos deben contener un par de clave-valor que incluya las probabilidades en un orden fijo, de la forma siguiente:
  
  <code>"output": [{"Probabilidades puntuadas": [<i>Probabilidad de "Riesgo",Probabilidad de "Sin riesgo"</i>]}, {"Probabilidades puntuadas": [<i>Probabilidad de "Riesgo",Probabilidad de "Sin riesgo"</i>]}]</code>

Para ser coherentes con las herramientas visuales de Azure ML utilizadas en Azure ML Studio y Azure ML Service, se recomienda utilizar los siguientes nombres de clave, aunque no es necesario:

- el nombre de clave `"Etiquetas puntuadas"` para la clave de salida que indica el valor previsto del modelo
- el nombre de clave `"Probabilidades puntuadas"` para la clave de salida que indica una matriz de probabilidades para cada clase

El siguiente archivo JSON de ejemplo cumple los requisitos anteriores y se puede utilizar como plantilla para crear sus propios archivos de respuesta JSON:


```JSON
{
  "output": [
    {
      "Etiquetas puntuadas": "Sin riesgo",
      "Probabilidades puntuadas": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Etiquetas puntuadas": "Sin riesgo",
      "Probabilidades puntuadas": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## Cuadernos de ejemplo
{: #frmwrks-azureservice-smpl-ntbks}

Los siguientes cuadernos muestran cómo trabajar con Microsoft Azure ML Service:

- [Ejemplos de puntuación de modelos de MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## Especificación de una instancia de Microsoft Azure ML Service
{: #connect-azureservice}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de Microsoft Azure ML Service. La instancia de Azure ML Service es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de aprendizaje automático de Microsoft Azure Service](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Conecte su instancia de Azure ML Service
{: #ca-connect}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de Azure ML Service.

1.  En la pestaña **Configurar**, en el panel de navegación, pulse **Proveedores de aprendizaje automático**.
1.  Pulse el botón **Añadir proveedor de aprendizaje automático** y, a continuación, pulse el mosaico **Microsoft Azure ML Service**.
1.  Especifique y guarde sus credenciales:

    - ID de cliente: el valor de serie real del ID de cliente, que verifica quién es y autentica y autoriza las llamadas que realiza a Azure Service.
    - Secreto de cliente: el valor de serie real del secreto, que verifica quién es y autentica y autoriza las llamadas que realiza a Azure Service.
    - Inquilino: el ID de inquilino correspondiente a su organización y que es una instancia dedicada de Azure AD. Para encontrar el ID de inquilino, pase el puntero del ratón por el nombre de cuenta para obtener el ID de inquilino o directorio, o bien seleccione Azure Active Directory > Propiedades > ID de directorio en el portal de Azure.
    - ID de suscripción: las credenciales de suscripción identifican de forma exclusiva su suscripción de Microsoft Azure. El ID de suscripción forma parte del URI para cada llamada de servicio.

    Consulte [Cómo utilizar el
portal para crear una entidad de servicio y una aplicación de Azure AD que puedan acceder a recursos](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} para ver instrucciones sobre
cómo obtener sus credenciales de Microsoft Azure.
    {: note}

1.  {{site.data.keyword.aios_short}} lista sus modelos desplegados; seleccione los que desee supervisar y pulse **Configurar**.

Ha seleccionado correctamente los despliegues.

## Registro de carga útil con el motor de Microsoft Azure ML Service
{: #cml-azsrvconfig}

### Enlazar el motor de Microsoft Azure ML Service
{: #cml-azsrvbind}

Un motor que no es {{site.data.keyword.pm_full}} está enlazado como Personalizado, lo que significa que sólo son metadatos; no hay ninguna
integración directa con el servicio no {{site.data.keyword.pm_full}}.
   
```
AZURE_ENGINE_CREDENTIALS = {
"client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
}

binding_uid = client.data_mart.bindings.add('My Azure ML Service engine', AzureMachineLearningServiceInstance(AZURE_ENGINE_CREDENTIALS))


bindings_details = client.data_mart.bindings.get_details()
```
{: codeblock}

Puede ver el enlace de servicio con el mandato siguiente:

```
client.data_mart.bindings.list()
```
{: codeblock}

Salida de ejemplo:

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### Añadir suscripción de Microsoft Azure ML Service
{: #cml-azsrvsub}

Añadir suscripción

```
client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
```
{: codeblock}

Obtener lista de suscripciones

```
subscriptions = client.data_mart.subscriptions.get_details()

subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
```
{: codeblock}

### Habilitar registro de carga útil
{: #cml-azsrvenlog}

Habilitar el registro de carga útil en la suscripción

```
subscription.payload_logging.enable()
```
{: codeblock}

Obtener detalles de registro

```
subscription.payload_logging.get_details()
```
{: codeblock}

### Puntuación y registro de carga útil
{: #cml-azsrvscore}

Puntúe el modelo. Para ver un ejemplo completo, consulte el [cuaderno Trabajar con el motor de Azure Machine Learning Service](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

Almacene la solicitud y respuesta en la tabla de registro de carga útil:

```
records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

subscription.payload_logging.store(records=records_list)
```
{: codeblock}
{: python}
   
Para los lenguajes que no sean Python, también puede realizar directamente el registro de carga útil, mediante una API REST.
   
```
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
{: codeblock}
{: json}


```
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
{: codeblock}



## Pasos siguientes
{: #ca-next}

-{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [¿En qué se diferencia el aprendizaje automático de Azure de Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

