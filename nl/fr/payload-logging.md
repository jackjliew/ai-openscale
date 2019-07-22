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

# Journalisation du contenu et des commentaires dans {{site.data.keyword.aios_short}}
{: #cdb-payload}

Pour {{site.data.keyword.aios_short}}, toutes les transactions
vers les modèles déployés doivent être consignées sous forme d'enregistrements de contenu dans le magasin de données de {{site.data.keyword.aios_short}}.
Les contenus d'entrée et de sortie (demandes et réponses) doivent être dans le format requis
par {{site.data.keyword.aios_short}}, décrit dans les spécifications.
{: shortdesc}

{{site.data.keyword.aios_short}} permet de journaliser le contenu et les commentaires par les méthodes suivantes :

- [Avec le client Python](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-pythonsdk)
- [Avec l'API REST](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload#cdb-payload-log-rest-api)
- [Automatiquement pour les fournisseurs d'apprentissage automatique supportés](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)

## Journalisation du contenu avec le SDK Python
{: #cdb-payload-log-pythonsdk}

Pour un exemple de code fonctionnel complet, voir l'exemple de bloc-notes
[AI Openscale and Custom ML Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb).

L'exemple de code suivant montre comment journaliser le contenu avec le SDK Python :

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

### Prévisualisation de la table de journalisation du contenu

Vous pouvez prévisualiser le contenu de votre table de journalisation de contenu
en vous connectant directement à la base de données ou en utilisant le SDK Python
(exemple de sortie suivant). 

![Exemple de sortie du SDK Python d'une table de journalisation de contenu](images/wosntbok.png)


## Journalisation du contenu avec l'API REST
{: #cdb-payload-log-rest-api}

L'exemple de code suivant montre comment journaliser le contenu avec l'API REST :

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



## Etapes suivantes
{: #cdb-payload-nxt-stps}

Pour plus d'information, voir
[Journalisation du contenu](http://aiopenscale-api.mybluemix.net/#/Payload%20Logging%20(Public%20API)/publishScoringPayload){: external}

