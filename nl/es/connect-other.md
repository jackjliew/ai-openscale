---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# Especifique una instancia de servicio de Machine Learning personalizado
{: #co-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de servicio. La instancia de servicio es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

## Conecte su instancia de servicio personalizado
{: #co-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de servicio.

1.  En la página de inicio de la herramienta {{site.data.keyword.aios_short}}, pulse **Empezar**.

    ![Página de inicio](images/gs-config-start.png)

2.  Seleccione el mosaico **Personalizado** y pulse **Siguiente**.

    ![Seleccionar personalizado](images/connect-custom.png)

3.  Conéctese a sus despliegues seleccionando una de las opciones:

    ![Seleccionar personalizado](images/connect-custom-deploy.png)

4.  Si ha seleccionado el mosaico "Especificar puntos finales de puntuación", especifique sus credenciales:

    ![Especificar credenciales de servicio](images/connect-custom-cred.png)

5.  Pulse **Siguiente**.

    - Si ha seleccionado el mosaico "Especificar puntos finales de puntuación", debe proporcionar un nombre y un punto final de despliegue:

      ![Especificar credenciales de servicio](images/connect-custom-endpoint.png)

      Pulse **Siguiente**.

    - Si ha seleccionado el mosaico "Solicitar una lista de despliegues", debe proporcionar un nombre de host o dirección IP, y un número de puerto:

      ![Especificar credenciales de servicio](images/connect-custom-apiendpoint.png)

      Pulse **Siguiente**.

      A continuación, seleccione en la lista de despliegues:

      ![Especificar credenciales de servicio](images/connect-custom-apiendpoint2.png)

6.  Revise los despliegues seleccionados.

    ![Especificar credenciales de servicio](images/connect-custom-deploy2.png)

7.  Pulse **Siguiente**.

### Cómo funciona
{: #co-works}

Esta imagen muestra el soporte de entorno personalizado:

![Cómo funciona el entorno personalizado](images/custom-how-works.png)

También puede consultar los enlaces siguientes:

[API de registro de carga útil de AIOS ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[API de despliegue personalizado ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[SDK de enlace de cliente Python ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[Trabajar con el motor de aprendizaje automático personalizado ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[SDK de Python para IBM Watson OpenScale ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

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

  La salida de puntuación anterior debe ser accesible desde un punto final de puntuación en directo que {{site.data.keyword.aios_short}} podría llamar mediante REST. Para AzureML, SageMaker y WML, {{site.data.keyword.aios_short}} se conecta directamente a los puntos finales de puntuación nativos, por lo que no debe preocuparse de implementar la especificación de puntuación

### Pasos siguientes
{: #co-next}

{{site.data.keyword.aios_short}} ahora está listo para que usted [especifique una base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
