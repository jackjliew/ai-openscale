---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Registrazione payload per istanze di servizio non {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #cml-connect}

Se il modello AI è distribuito in un motore di machine learning diverso da {{site.data.keyword.pm_full}}, è necessario abilitare la registrazione del payload per il motore di machine learning esterno con un client Python.
{: shortdesc}

Consultare informazioni più complete nella [documentazione del client Python{{site.data.keyword.aios_short}} ](http://ai-openscale-python-client.mybluemix.net/){: external} e nei notebook di esempio del client Python {{site.data.keyword.aios_short}} che fanno parte dei [supporti didattici {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}.

## Prima di iniziare
{: #cml-prereq}

Sarà necessario che i dati di training del proprio modello siano disponibili in Db2 o {{site.data.keyword.cos_full}} per monitorare la distorsione per il modello. L'esplicabilità e l'accuratezza non sono supportate per le funzioni Python. Per ulteriori informazioni sui dati di training, consultare [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- Importare e inizializzare {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  È possibile trovare le credenziali seguendo i passi mostrati nell'argomento "[Creazione delle credenziali](/docs/services/ai-openscale?topic=ai-openscale-cred-create)".

- Creare un nome schema nel database PostgreSQL

- Impostare un datamart

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## Gestione del motore di machine learning personalizzato
{: #cml-cusconfig}

### Collegare il motore di machine learning personalizzato
{: #cml-cusbind}

- Un motore non {{site.data.keyword.pm_full}} viene collegato come Personalizzato, che indica che contiene solo metadati; non esiste un'integrazione diretta con il servizio non {{site.data.keyword.pm_full}}. È possibile collegare più di un motore di machine learning a {{site.data.keyword.aios_short}} utilizzando il metodo `client.data_mart.bindings.add`.

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  È possibile visualizzare il bind del servizio con il seguente comando:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Bind ML generico](images/ml-generic-bind.png)

### Aggiungere la sottoscrizione personalizzata
{: #cml-cussub}

- Aggiungere la sottoscrizione

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- Richiamare l'elenco di sottoscrizioni

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Abilitare la registrazione del payload
{: #cml-cusenlog}

- Abilitare la registrazione del payload nella sottoscrizione

    ```python
    subscription.payload_logging.enable()
    ```

- Richiamare i dettagli della registrazione

    ```python
    subscription.payload_logging.get_details()
    ```

Per ulteriori informazioni, consultare [Registrazione payload]().

### Calcolare il punteggio e registrare il payload
{: #cml-cusscore}

- Calcolare il punteggio del modello. Per un esempio completo, consultare il notebook [IBM {{site.data.keyword.aios_full}} & Custom ML Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}.

- Memorizzare la richiesta e la risposta nella tabella di registrazione del payload

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **Nota**: per i linguaggi diversi da Python, è possibile anche eseguire direttamente la registrazione del payload, utilizzando un'API REST.

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

## Gestione del motore di machine learning Microsoft Azure
{: #cml-azconfig}

### Collegare il motore di machine learning Microsoft Azure
{: #cml-azbind}

- Un motore non {{site.data.keyword.pm_full}} viene collegato come Personalizzato, che indica che contiene solo metadati; non esiste un'integrazione diretta con il servizio non {{site.data.keyword.pm_full}}.

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
  È possibile visualizzare il bind del servizio con il seguente comando:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Bind di Azure ML](images/ml-azure-bind.png)

### Aggiungere la sottoscrizione MS Azure ML
{: #cml-azsub}

- Aggiungere la sottoscrizione

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Richiamare l'elenco di sottoscrizioni

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Abilitare la registrazione del payload
{: #cml-azenlog}

- Abilitare la registrazione del payload nella sottoscrizione

    ```python
    subscription.payload_logging.enable()
    ```

- Richiamare i dettagli della registrazione

    ```python
    subscription.payload_logging.get_details()
    ```

### Calcolare il punteggio e registrare il payload
{: #cml-azscore}

- Calcolare il punteggio del modello. Per un esempio completo, consultare il notebook [Working with Azure Machine Learning Studio Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

- Memorizzare la richiesta e la risposta nella tabella di registrazione del payload:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Nota**: per i linguaggi diversi da Python, è possibile anche eseguire direttamente la registrazione del payload, utilizzando un'API REST.

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

## Gestione del motore di machine learning Amazon SageMaker
{: #cml-smconfig}

### Collegare il motore di machine learning Amazon SageMaker
{: #cml-smbind}

- Un motore non {{site.data.keyword.pm_full}} viene collegato come Personalizzato, che indica che contiene solo metadati; non esiste un'integrazione diretta con il servizio non {{site.data.keyword.pm_full}}.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  È possibile visualizzare il bind del servizio con il seguente comando:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Bind di SageMaker ML](images/ml-sagemaker-bind.png)

### Aggiungere la sottoscrizione Amazon SageMaker ML
{: #cml-smsub}

- Aggiungere la sottoscrizione

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Richiamare l'elenco di sottoscrizioni

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Abilitare la registrazione del payload
{: #cml-smenlog}

- Abilitare la registrazione del payload nella sottoscrizione

    ```python
    subscription.payload_logging.enable()
    ```

- Richiamare i dettagli della registrazione

    ```python
    subscription.payload_logging.get_details()
    ```

### Calcolare il punteggio e registrare il payload
{: #cml-smscore}

- Calcolare il punteggio del modello. Per un esempio completo, consultare il notebook [Working with SageMaker Machine Learning Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}.


- Memorizzare la richiesta e la risposta nella tabella di registrazione del payload:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Nota**: per i linguaggi diversi da Python, è possibile anche eseguire direttamente la registrazione del payload, utilizzando un'API REST.

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

## Passi successivi
{: #cml-next}

- Per continuare con il client {{site.data.keyword.aios_short}}, consultare [Specifica di un database](/docs/services/ai-openscale?topic=ai-openscale-connect-db).

- Per continuare con la libreria dei comandi Python, fare riferimento alla [documentazione del client Python](http://ai-openscale-python-client.mybluemix.net/){: external}.
