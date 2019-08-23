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

# Journalisation du contenu utile avec le moteur d'apprentissage automatique personnalisé
{: #cml-cusconfig}

## Lier votre moteur d'apprentissage automatique personnalisé
{: #cml-cusbind}

- Un moteur non-{{site.data.keyword.pm_full}} se lie comme personnalisé,
ce qui signifie qu'il s'agit seulement de métadonnées ; il n'y a pas d'intégration directe avec le service non-{{site.data.keyword.pm_full}}. Vous pouvez lier plusieurs moteurs d'apprentissage automatique à {{site.data.keyword.aios_short}}
en utilisant la méthode `client.data_mart.bindings.add`.

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Vous pouvez voir votre liaison de service avec la commande suivante :

    ```python
    client.data_mart.bindings.list()
    ```

    ![Liaison ML générique](images/ml-generic-bind.png)

## Ajouter un abonnement personnalisé
{: #cml-cussub}

- Ajouter un abonnement

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- Obtenir la liste des abonnements

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

## Activer la journalisation du contenu utile
{: #cml-cusenlog}

- Activer la journalisation du contenu utile dans l'abonnement

    ```python
    subscription.payload_logging.enable()
    ```

- Obtenir les détails de la journalisation

    ```python
    subscription.payload_logging.get_details()
    ```

Pour plus d'informations, consultez [Journalisation du contenu utile]().

## Evaluation et journalisation du contenu utile
{: #cml-cusscore}

- Evaluez votre modèle. Pour un exemple complet, consultez le
[bloc-notes
IBM {{site.data.keyword.aios_full}} & Custom ML Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}.

- Stocker la demande et la réponse dans la table de journalisation du contenu utile

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **Remarque** : Pour les langages autres que Python, vous pouvez également effectuer la journalisation du contenu utile directement, avec une API REST.

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

