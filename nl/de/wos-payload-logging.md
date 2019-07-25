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

# Protokollierung von Nutzdaten und Rückmeldedaten in {{site.data.keyword.aios_short}}
{: #cdb-payload}

Bei {{site.data.keyword.aios_short}} müssen alle Transaktionen, die an die bereitgestellten Modelle gesendet werden, als Nutzdatensätze im {{site.data.keyword.aios_short}}-Datamart protokolliert werden. Die Nutzdaten für die Ein- und die Ausgabe (Anforderungen und Antworten) müssen das für {{site.data.keyword.aios_short}} erforderliche, in den Spezifikationen beschriebene Format aufweisen.
{: shortdesc}

{{site.data.keyword.aios_short}} unterstützt die Protokollierung von Nutzdaten und Rückmeldedaten über die folgenden Methoden:

- [Unter Verwendung des Python-Clients](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [Unter Verwendung der REST-API](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [Automatisch für unterstützte Machine Learning-Anbieter](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## Nutzdaten mit Python-SDK protokollieren
{: #cdb-payload-log-pythonsdk}

Ein Beispiel für vollständigen, funktionsfähigen Code enthält das Beispielnotebook für [AI Openscale und angepasste Machine Learning-Engines](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb).

Das folgende Codebeispiel zeigt, wie die Nutzdaten mit dem Python-SDK protokolliert werden:

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

### Tabelle mit Nutzdatenprotokollierung voranzeigen

Sie können den Inhalt Ihrer Tabelle für Nutzdatenprotokollierung entweder über eine direkte Verbindung zur Datenbank oder mit dem Python-SDK wie in der folgenden Beispielausgabe dargestellt in einer Vorschau anzeigen. 

![Beispielausgabe der Tabelle für Nutzdatenprotokollierung mit dem Python-SDK](images/wosntbok.png)


## Nutzdaten mit REST-API protokollieren
{: #cdb-payload-log-rest-api}

Das folgende Codebeispiel zeigt, wie die Nutzdaten mit der REST-API protokolliert werden:

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



## Weitere Schritte
{: #cdb-payload-nxt-stps}

Weitere Informationen finden Sie unter [Nutzdatenprotokollierung](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API)/publishScoringPayload).{: external}


