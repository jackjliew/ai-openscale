---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Infraestructuras de aprendizaje automático personalizadas
{: #frmwrks-custom}

Puede utilizar la infraestructura de aprendizaje automático personalizada para realizar el registro de carga útil y el registro de opiniones, y para medir la exactitud del rendimiento, la detección de sesgos en tiempo de ejecución, la explicabilidad y la función de eliminación automática de sesgo en {{site.data.keyword.aios_full}}. La infraestructura de aprendizaje automático personalizada debe tener equivalencia en {{site.data.keywor.pm_full}}.

{{site.data.keyword.aios_full}} da completo soporte a las siguientes infraestructuras de aprendizaje automático personalizadas:
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Equivalente a {{site.data.keyword.pm_full}} | Clasificación | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

## Adición de un motor de aprendizaje automático personalizado a {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

Puede configurar {{site.data.keyword.aios_short}} para que funcione con un proveedor de aprendizaje automático personalizado utilizando uno de los métodos siguientes:

- Si es la primera vez que está añadiendo un proveedor de aprendizaje automático personalizado a {{site.data.keyword.aios_short}}, puede utilizar la interfaz de configuración. Para obtener más información, consulte [Especificación de una instancia de aprendizaje automático personalizado](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Debe utilizar este método si desea tener más de un proveedor. Para obtener más información sobre cómo realizar esta acción mediante programación, consulte [Enlazar el motor de aprendizaje automático personalizado](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Cuadernos de ejemplo
{: #frmwrks-custom-smpl-ntbks}

- [Creación del motor de aprendizaje automático personalizado utilizando el clúster Kubernetes](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Creación de la despensa de datos, supervisión del despliegue del modelo y análisis de datos](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Explorar más
{: #frmwrks-custom-mediumblogs}

[Supervisar el motor de aprendizaje automático personalizado con Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}

## Motor de aprendizaje automático personalizado
{: #fmrk-workaround-customengine}

Un motor de aprendizaje automático personalizado proporciona las prestaciones de infraestructura y alojamiento para modelos de aprendizaje automático
y aplicaciones web. Los motores de aprendizaje automático personalizados a los que da soporte {{site.data.keyword.aios_short}} deben cumplir los
requisitos siguientes:

- Exponga dos tipos de puntos finales de API REST:

   * punto final de descubrimiento (lista GET de despliegues y detalles)
   * puntos finales de puntuación (puntuación en línea y en tiempo real)

- Todos los puntos finales deben ser compatibles con la especificación de swagger a la que se va a dar soporte.

- La carga útil de entrada y salida a y desde el despliegue deben ser compatibles con el formato de archivo JSON que se describe en la
especificación.

En esta etapa sólo se da soporte a los formatos `BasicAuth` o `none`.
{: Note}

En el ejemplo siguiente se muestra la especificación de puntos finales de la API REST:

![La especificación de puntos finales de la API REST se muestra desde el documento de swagger](images/wosdeployments.png)


En el ejemplo siguiente se muestra el formato de una carga útil de entrada:

![Se muestra el ejemplo de carga útil de entrada](images/wosinputdata.png)


## ¿Cuándo es un motor de aprendizaje automático personalizado la mejor opción para mí?
{: #fmrk-workaround-enging-choice}

Un motor de aprendizaje automático personalizado es la mejor opción cuando se cumplen las situaciones siguientes:

- No está utilizando ninguno de los productos listos para usar disponibles para dar servicio a sus modelos de aprendizaje automático. Para ello, solo debe
desarrollar su propio sistema. No hay ni habrá soporte directo en {{site.data.keyword.aios_short}} para ello.
- {{site.data.keyword.aios_short}} todavía no da soporte al motor de servicio que está utilizando de un proveedor de terceros. En este caso,
considere el desarrollo de un motor de aprendizaje automático personalizado que englobe los despliegues originales o nativos.

## Especifique una instancia de servicio de Machine Learning personalizado
{: #co-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de servicio. La instancia de servicio es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

## Conecte su instancia de servicio personalizado
{: #co-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de servicio. Puede conectar un servicio personalizado.

1.  En la pestaña **Configurar**, en el panel de navegación, pulse **Proveedores de aprendizaje automático**.

   ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

2. Pulse el botón **Añadir proveedor de aprendizaje automático** y, a continuación, pulse el mosaico **Entorno personalizado**.

   ![Se muestra la pantalla de configuración de proveedor de aprendizaje automático personalizado con campos para las credenciales y el nombre y la descripción de la instancia](images/ml-custom-provider.png)

3. Especifique un nombre y una descripción para el proveedor de aprendizaje automático y pulse **Siguiente**. 

4. Elija si desea conectarse a los despliegues [solicitando una lista](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) o [especificando puntos finales de puntuación individuales](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![Se muestra la pantalla para conectar a los despliegues con opciones para solicitar una lista de despliegues o especificar un punto final de puntuación individual](images/ml-custom-connect-deployments.png)
    
5. Pulse **Siguiente**.

### Solicitar la lista de despliegues
{: #co-config-request-list}

1. Si ha seleccionado el mosaico **Solicitar la lista de despliegues**, especifique sus credenciales y punto final de API, y a continuación pulse **Guardar**.

   ![Se muestra la pantalla de lista de despliegues con campos para especificar credenciales de servicio y un punto final de API](images/connect-custom-cred.png)

2. Una vez que haya guardado la configuración de aprendizaje automático, vuelva al **Panel de control**, pulse la pestaña **Detalles** y a continuación pulse el botón **Añadir a panel de control**.

3. Seleccione un despliegue en la lista y pulse **Configurar**.

Ahora está listo para configurar supervisores.

### Proporcionar puntos finales de puntuación individuales
{: #co-config-scoring-endpoints}

1. Si ha seleccionado el mosaico **Especificar puntos finales de puntuación individuales**, especifique sus credenciales para el punto final de API y a continuación pulse **Guardar**.

2. Una vez que haya guardado la configuración de aprendizaje automático, vuelva al **Panel de control**, pulse la pestaña **Detalles** y a continuación pulse el botón **Añadir a panel de control**.

3. Pulse el botón **Añadir punto final**.

4. En el menú desplegable, seleccione el entorno personalizado, especifique el nombre de despliegue y el punto final de API y a continuación pulse **Guardar**.

Ahora está listo para configurar supervisores.

### Cómo funciona
{: #co-works}

La imagen siguiente muestra el soporte de entorno personalizado:

![Se muestra el gráfico Cómo funciona el entorno personalizado. Muestra recuadros para el entorno personalizado con la API de cliente y la API de Watson OpenScale](images/custom-how-works.png)

También puede consultar los enlaces siguientes:

[API de registro de carga útil de {{site.data.keyword.aios_short}}](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[API de despliegue personalizado](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[SDK de enlace de cliente Python](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[Trabajar con el motor de aprendizaje automático personalizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[SDK de Python para IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **Criterios de entrada para que el modelo admita supervisores**

  El modelo debe tomar como entrada un vector de característica, que básicamente es una colección de campos con nombre y sus valores (los campos que se supervisan para comprobar si presentan sesgo son unos de estos campos):

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  En este ejemplo, `“age”` podría ser un campo cuya equidad alguien está evaluando.

  Si la entrada es un tensor o una matriz, que se transforma en el espacio de característica de entrada (lo que a menudo sucede en el aprendizaje profundo de texto o imágenes), la plataforma de {{site.data.keyword.aios_short}} no puede gestionar ese modelo en el release actual. Por extensión, los modelos de aprendizaje profundo con entradas de texto o imágenes no se pueden gestionar para la detección y mitigación de sesgos.

  Además, para permitir la explicabilidad se deben cargar datos de entrenamiento.

  Para la explicabilidad de texto, el texto completo debe ser una de las características. En el release actual no se da soporte a la explicabilidad de imágenes para un modelo personalizado.
  {: note}

- **Criterios de salida para que el modelo admita supervisores**

  El modelo debe generar el vector de característica de entrada junto con las probabilidades de predicción de distintas clases de ese modelo.

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  En este ejemplo, `"personal”` y `“camping”` son las clases posibles, y las puntuaciones de cada salida de puntuación se asignan a ambas clases. Si faltan las probabilidades de predicción, la detección de sesgo funcionará, pero la eliminación automática de sesgo no.

  La salida de puntuación anterior debe ser accesible desde un punto final de puntuación en directo que {{site.data.keyword.aios_short}}
podría llamar mediante REST. Para AzureML, SageMaker y {{site.data.keyword.pm_full}}, {{site.data.keyword.aios_short}} se conecta
directamente a los puntos finales de puntuación nativos, (por lo que no debe preocuparse de implementar la especificación de puntuación).

## Ejemplos de motor de aprendizaje automático personalizado
{: #fmrk-workaround-cstmmlsengex}

Utilice los ejemplos siguientes para configurar su propio motor de aprendizaje automático personalizado.
{: shortdesc}

### Python y flask
{: #fmrk-workaround-pandflask}

El [ejemplo de motor ML
personalizado publicado en git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external} utiliza python y flask para servir al modelo scikit-learn.

El [archivo README](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
describe cómo se puede desplegar la aplicación localmente para fines de pruebas así como la aplicación cf en IBM Cloud. La implementación de puntos finales de API REST se puede encontrar en
[app.py file](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py){: external}.

### Node.js
{: #fmrk-workaround-nodejs}

También puede encontrar el ejemplo del motor de aprendizaje automático personalizado escrito en
[Node.js aquí](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs){: external}.

### Patrón de código End2end
{: #fmrk-workaround-e2ecode}

[Patrón de código](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale){: external} que muestra un
ejemplo end2end de despliegue de motor personalizado e integración con {{site.data.keyword.aios_short}}.

## Registro de carga útil con el motor de aprendizaje automático personalizado
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

Para obtener más información, consulte [Registro de carga útil](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

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


## Pasos siguientes
{: #fmrk-workaround-nxt-steps-over}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).

Implemente su propia solución utilizando uno de estos [ejemplos de aprendizaje automático personalizado](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).
