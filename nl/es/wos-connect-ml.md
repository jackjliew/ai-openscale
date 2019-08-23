---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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


## Pasos siguientes
{: #cml-next}

- Para continuar con el cliente de {{site.data.keyword.aios_short}}, consulte [Configuración de la supervisión de exactitud o calidad](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Para continuar con la biblioteca de mandatos de Python, consulte la [documentación del cliente Python](http://ai-openscale-python-client.mybluemix.net/){: external}.
