---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Criação de log de carga útil e de feedback no {{site.data.keyword.aios_short}}
{: #cdb-payload}

Para o {{site.data.keyword.aios_short}}, todas as transações que vão para os modelos implementados devem ser registradas como registros de carga útil no data mart do {{site.data.keyword.aios_short}}. As cargas úteis de entrada e de saída (solicitações e respostas) precisam estar no formato requerido pelo {{site.data.keyword.aios_short}}, conforme descrito nas especificações.
{: shortdesc}

O {{site.data.keyword.aios_short}} suporta a criação de log de carga útil e de feedback por meio dos métodos a seguir:

- [Usando o cliente Python](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [Usando a API de REST](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [Automaticamente para provedores de aprendizado de máquina suportados](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## Registrando a carga útil com o Python SDK
{: #cdb-payload-log-pythonsdk}

Para obter um exemplo de código de trabalho integral, consulte o bloco de notas de amostra [AI Openscale e o mecanismo de ML customizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb).

A amostra de código a seguir mostra como registrar a carga útil usando o Python SDK:

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

### Visualizando a tabela de criação de log de carga útil

É possível visualizar o conteúdo de sua tabela de criação de log de carga útil, conectando diretamente ao banco de dados ou usando o SDK do Python, que é mostrado na saída de amostra a seguir. 

![Saída de amostra do SDK do Python da tabela de criação de log de carga útil](images/wosntbok.png)


## Registrando a carga útil com a API de REST
{: #cdb-payload-log-rest-api}

A amostra de código a seguir mostra como registrar a carga útil usando a API de REST:

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



## Próximos passos
{: #cdb-payload-nxt-stps}

Para obter mais informações, consulte [Criação de log de carga útil](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API)/publishScoringPayload){: external}


