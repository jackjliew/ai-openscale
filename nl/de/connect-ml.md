---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Nutzdatenprotokollierung für andere Serviceinstanzen als die Watson Machine Learning-Serviceinstanz
{: #cml-connect}

Wenn Ihr AI-Modell in einer anderen Engine für Machine Learning als Watson Machine Learning (WML) bereitgestellt wird, müssen Sie die Nutzdatenprotokollierung für die externe Machine Learning-Engine mit einem Python-Client ermöglichen.
{: shortdesc}

Umfassendere Informationen finden Sie in der [Dokumentation für {{site.data.keyword.aios_short}} Python-Clients ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://ai-openscale-python-client.mybluemix.net/){: new_window} und in den Beispielnotebooks für den {{site.data.keyword.aios_short}} Python-Client, die Teil der [{{site.data.keyword.aios_short}}-Lernprogramme ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: new_window} sind.

## Vorbereitende Schritte
{: #cml-prereq}

Zur Überwachung der Verzerrung für Ihr Modell müssen Sie die Trainingsdaten Ihres Modells in Db2 oder Cloud Object Storage bereitstellen. Erklärbarkeit und Genauigkeit werden für Python-Funktionen nicht unterstützt. Weitere Informationen zu den Trainingsdaten finden Sie unter [Warum muss {{site.data.keyword.aios_short}} auf meine Trainingsdaten zugreifen?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- {{site.data.keyword.aios_short}} importieren und initialisieren

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  Berechtigungsnachweise können durch Ausführen der Schritte im Abschnitt "[Berechtigungsnachweise erstellen](/docs/services/ai-openscale?topic=ai-openscale-cred-create)" erstellt bzw. ermittelt werden.

- Schemanamen in Ihrer PostgreSQL-Datenbank erstellen

- Datamart einrichten

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## Mit der angepassten Machine Learning-Engine arbeiten
{: #cml-cusconfig}

### Angepasste Machine Learning-Engine binden
{: #cml-cusbind}

- Die Bindung einer Machine Learning-Engine, bei der es sich nicht um eine WML-Engine handelt, erfolgt als 'angepasst', was bedeutet, dass es sich lediglich um Metadaten handelt und keine direkte Integration mit dem Nicht-WML-Service besteht.

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

### Angepasstes Abonnement
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

### Nutzdatenprotokollierung aktivieren
{: #cml-cusenlog}

- Nutzdatenprotokollierung im Abonnement aktivieren

    ```python
    subscription.payload_logging.enable()
    ```

- Protokollierungsdetails abrufen

    ```python
    subscription.payload_logging.get_details()
    ```

### Scoring und Nutzdatenprotokollierung
{: #cml-cusscore}

- Führen Sie ein Scoring für Ihr Modell durch. Ein ausführliches Beispiel enthält das [IBM Notizbuch für {{site.data.keyword.aios_full}} & für angepasste ML-Engines ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

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

## Mit der Microsoft Azure Machine Learning-Engine arbeiten
{: #cml-azconfig}

### Microsoft Azure Machine Learning-Engine binden
{: #cml-azbind}

- Die Bindung einer Machine Learning-Engine, bei der es sich nicht um eine WML-Engine handelt, erfolgt als 'angepasst', was bedeutet, dass es sich lediglich um Metadaten handelt und keine direkte Integration mit dem Nicht-WML-Service besteht.

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Sie können Ihre Servicebindung mit dem folgenden Befehl anzeigen:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure Machine Learning-Bindung](images/ml-azure-bind.png)

### Microsoft Azure Machine Learning-Abonnement hinzufügen
{: #cml-azsub}

- Abonnement hinzufügen

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Abonnementliste abrufen

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Nutzdatenprotokollierung aktivieren
{: #cml-azenlog}

- Nutzdatenprotokollierung im Abonnement aktivieren

    ```python
    subscription.payload_logging.enable()
    ```

- Protokollierungsdetails abrufen

    ```python
    subscription.payload_logging.get_details()
    ```

### Scoring und Nutzdatenprotokollierung
{: #cml-azscore}

- Führen Sie ein Scoring für Ihr Modell durch. Ein vollständiges Beispiel enthält das [Notizbuch 'Mit der Azure Machine Learning Studio Engine arbeiten' ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

- Anforderung und Antwort in der Nutzdatenprotokollierungstabelle speichern:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

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

## Mit der Amazon SageMaker Machine Learning-Engine arbeiten
{: #cml-smconfig}

### Amazon SageMaker Machine Learning-Engine binden
{: #cml-smbind}

- Die Bindung einer Machine Learning-Engine, bei der es sich nicht um eine WML-Engine handelt, erfolgt als 'angepasst', was bedeutet, dass es sich lediglich um Metadaten handelt und keine direkte Integration mit dem Nicht-WML-Service besteht.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Sie können Ihre Servicebindung mit dem folgenden Befehl anzeigen:

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker Machine Learning-Bindung](images/ml-sagemaker-bind.png)

### Amazon SageMaker Machine Learning-Abonnement hinzufügen
{: #cml-smsub}

- Abonnement hinzufügen

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Abonnementliste abrufen

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Nutzdatenprotokollierung aktivieren
{: #cml-smenlog}

- Nutzdatenprotokollierung im Abonnement aktivieren

    ```python
    subscription.payload_logging.enable()
    ```

- Protokollierungsdetails abrufen

    ```python
    subscription.payload_logging.get_details()
    ```

### Scoring und Nutzdatenprotokollierung
{: #cml-smscore}

- Führen Sie ein Scoring für Ihr Modell durch. Ein vollständiges Beispiel enthält das [Notizbuch 'Mit der SageMaker Machine Learning-Engine arbeiten' ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

- Anforderung und Antwort in der Nutzdatenprotokollierungstabelle speichern:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

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

## Weitere Schritte
{: #cml-next}

- Wenn Sie mit dem {{site.data.keyword.aios_short}}-Client fortfahren möchten, finden Sie entsprechende Informationen in [Datenbank angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-db).

- Wenn Sie mit der Python-Befehlsbibliothek fortfahren möchten, entnehmen Sie die entsprechenden Informationen der [Dokumentation für Python-Clients ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://ai-openscale-python-client.mybluemix.net/){: new_window}.
