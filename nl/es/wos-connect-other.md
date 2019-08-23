---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# Especifique una instancia de servicio de Machine Learning personalizado
{: #co-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de servicio. La instancia de servicio es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

## Conecte su instancia de servicio personalizado
{: #co-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de servicio. Puede conectar un servicio personalizado.

1. En la pestaña **Configurar**, pulse **Proveedor de aprendizaje automático**. En función de su entorno, es posible que no vea todos los proveedores siguientes:

   ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

2. Seleccione el mosaico **Entorno personalizado**.

   ![Se muestra la pantalla de configuración de proveedor de aprendizaje automático personalizado con campos para las credenciales y el nombre y la descripción de la instancia](images/ml-custom-provider.png)

1.  Especifique y guarde sus credenciales:

    - Nombre de usuario: el nombre de usuario del proveedor de aprendizaje automático personalizado.
    - Contraseña: la contraseña del proveedor de aprendizaje automático personalizado.
    - Nombre de instancia de proveedor de servicio: el nombre específico asignado a este proveedor de servicio.
    - Descripción: (opcional) la descripción en lenguaje sencillo de esta instancia de proveedor de servicio. Si no tiene entornos de producción y de prueba, este sería un buen lugar donde incluir esa información.

4. Elija si desea conectarse a los despliegues [solicitando una lista](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) o [especificando puntos finales de puntuación individuales](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![Seleccionar personalizado](images/ml-custom-connect-deployments.png)
    
5. Pulse **Siguiente**.

### Solicitar la lista de despliegues
{: #co-config-request-list}

1. Si ha seleccionado el mosaico **Solicitar la lista de despliegues**, especifique sus credenciales y punto final de API, y a continuación pulse **Guardar**.

   ![Especificar credenciales de servicio](images/connect-custom-cred.png)

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

![Cómo funciona el entorno personalizado](images/custom-how-works.png)

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

### Pasos siguientes
{: #co-next}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
