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

# Nutzdatenprotokollierung mit der angepassten Machine Learning-Engine
{: #cml-cusconfig}

## Bindung für angepasste Machine Learning-Engine erstellen
{: #cml-cusbind}

- Eine Nicht-{{site.data.keyword.pm_full}}-Engine wird als 'Angepasst' gebunden, was bedeutet, dass nur die Metadaten gebunden werden und somit keine direkte Integration mit dem Nicht-{{site.data.keyword.pm_full}}-Service besteht. Mit der Methode `client.data_mart.bindings.add` können Sie mehr als eine Machine Learning-Engine an {{site.data.keyword.aios_short}} binden.

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Sie können Ihre Servicebindung mit dem folgenden Befehl anzeigen:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Generische ML-Bindung](images/ml-generic-bind.png)

## Angepasstes Abonnement
{: #cml-cussub}

- Abonnement hinzufügen

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- Abonnementliste abrufen

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

## Nutzdatenprotokollierung aktivieren
{: #cml-cusenlog}

- Nutzdatenprotokollierung im Abonnement aktivieren

    ```python
    subscription.payload_logging.enable()
    ```

- Protokollierungsdetails abrufen

    ```python
    subscription.payload_logging.get_details()
    ```

Weitere Informationen finden Sie in [Nutzdatenprotokollierung]().

## Scoring und Nutzdatenprotokollierung
{: #cml-cusscore}

- Führen Sie ein Scoring für Ihr Modell durch. Ein ausführliches Beispiel enthält das [Notebook für IBM {{site.data.keyword.aios_full}} & angepasste ML-Engines](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}.

- Anforderung und Antwort in der Nutzdatenprotokollierungstabelle speichern

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **Hinweis**: Für andere Sprachen als Python können Sie die Nutzdatenprotokollierung auch direkt über eine REST-API durchführen.

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

