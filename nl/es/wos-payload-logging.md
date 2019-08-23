---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests, schema, REST API, API

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

# Registro de carga útil y opinión en {{site.data.keyword.aios_short}}
{: #cdb-payload}

Para {{site.data.keyword.aios_short}}, todas las transacciones destinadas a los modelos desplegados se deben registrar como registros de carga
útil en
la despensa de datos de {{site.data.keyword.aios_short}}. Las cargas útiles de entrada y salida (solicitudes y respuestas) deben tener el formato que requiere {{site.data.keyword.aios_short}}, tal como se describe en las especificaciones. 
{: shortdesc}

{{site.data.keyword.aios_short}} da soporte al registro de carga útil y de opinión mediante los métodos siguientes:

- [Utilización del cliente Python](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [Utilización de la API REST](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [Automáticamente para proveedores de aprendizaje automático soportados](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## Registro de la carga útil con el SDK de Python
{: #cdb-payload-log-pythonsdk}

Para obtener un ejemplo de código de trabajo completo, consulte el
cuaderno de
ejemplo [AI Openscale and Custom ML Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb).

En el ejemplo de código siguiente se muestra cómo registrar la carga útil utilizando el SDK de Python:

```
records_list = [
   PayloadRecord(request=request_data, 
                 response=response_data,
                 response_time=response_time), 
   PayloadRecord(request=request_data,
                 response=response_data,
                 response_time=response_time)]
subscription.payload_logging.store(records=records_list)
```

### Vista previa de la tabla de registro de carga útil

Puede obtener una vista previa del contenido de la tabla de registro de carga útil o bien conectándose directamente a la base de datos o utilizando
el SDK de Python, que se muestra en la salida de ejemplo siguiente. 

![Salida de ejemplo del SDK de Python de la tabla de registro de carga útil](images/wosntbok.png)


## Registro de la carga útil con la API REST
{: #cdb-payload-log-rest-api}

El código de ejemplo siguiente muestra cómo registrar la carga útil utilizando la API REST:

```
PAYLOAD_STORING_HREF_PATTERN ='{}/v1/data_marts/{}/scoring_payloads'
endpoint = PAYLOAD_STORING_HREF_PATTERN.format(
                                AIOS_CREDENTIALS['url'], 
                                AIOS_CREDENTIALS['data_mart_id'])
deployment_uid = subscription.get_details()['entity']['deployments'][0]['deployment_id']
payload = [{'binding_id': binding_uid, 
            'deployment_id': deployment_uid,
            'subscription_id': subscription.uid,
            'scoring_id': scoring_uid,
            'response': response_data,
            'request': request_data}]
headers = {'Authorization': 'Bearer '+ token}
req_response = requests.post(endpoint, 
                             json=payload,
                             headers = headers)
```

## Pasos siguientes

Una vez configurado el registro de carga útil, puede continuar configurando supervisores especificando detalles del modelo. Para obtener más información, consulte [Proporcionar detalles del modelo](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets).

