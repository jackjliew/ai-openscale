---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Journalisation du contenu pour les instances de service non-Watson Machine Learning
{: #cml-connect}

Si votre modèle d'AI est déployé dans un moteur d'apprentissage automatique autre que Watson Machine Learning (WML),
vous devez activer la journalisation du contenu pour le moteur d'apprentissage automatique externe avec un client Python.
{: shortdesc}

Pour une information plus complète, voir la
[documentation du client Python {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://ai-openscale-python-client.mybluemix.net/){: new_window}
et les exemples de bloc-notes du client Python {{site.data.keyword.aios_short}}
des
[tutoriels {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: new_window}.

## Avant de commencer
{: #cml-prereq}

Vous devrez avoir les données de formation de votre modèle disponibles dans Db2 ou Cloud Object Storage pour surveiller son biais. L'explicabilité et l'exactitude ne sont pas prises en charge pour les fonctions Python. Pour plus d'informations sur les données de formation, voir [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- Importer et lancer {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  Vous trouverez les identifiants en procédant comme indiqué à la rubrique
"[Création d'identifiants](/docs/services/ai-openscale?topic=ai-openscale-cred-create)".

- Créer un nom de schéma dans votre base de données PostgreSQL

- Configurer un magasin de données

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## Utilisation du moteur d'apprentissage automatique personnalisé
{: #cml-cusconfig}

### Lier votre moteur d'apprentissage automatique personnalisé
{: #cml-cusbind}

- Un moteur non-WML se lie comme personnalisé, ce qui signifie qu'il s'agit seulement de métadonnées ; il n'y a pas d'intégration directe avec le service non-WML.

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

### Ajouter un abonnement personnalisé
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

### Activer la journalisation du contenu
{: #cml-cusenlog}

- Activer la journalisation du contenu dans l'abonnement

    ```python
    subscription.payload_logging.enable()
    ```

- Obtenir les détails de la journalisation

    ```python
    subscription.payload_logging.get_details()
    ```

### Evaluation et journalisation du contenu
{: #cml-cusscore}

- Evaluez votre modèle. Pour un exemple complet, voir le
[bloc-notes
IBM {{site.data.keyword.aios_full}} & Custom ML Engine
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}.

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

- Stocker la demande et la réponse dans la table de journalisation du contenu

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **Remarque** : Pour les langages autres que Python, vous pouvez également effectuer la journalisation du contenu directement, avec une API REST.

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

## Utilisation du moteur d'apprentissage automatique Microsoft Azure
{: #cml-azconfig}

### Lier votre moteur MS Azure ML
{: #cml-azbind}

- Un moteur non-WML se lie comme personnalisé, ce qui signifie qu'il s'agit seulement de métadonnées ; il n'y a pas d'intégration directe avec le service non-WML.

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
  Vous pouvez voir votre liaison de service avec la commande suivante :

    ```python
    client.data_mart.bindings.list()
    ```

    ![Liaison Azure ML](images/ml-azure-bind.png)

### Ajouter un abonnement MS Azure ML
{: #cml-azsub}

- Ajouter un abonnement

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Obtenir la liste des abonnements

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Activer la journalisation du contenu
{: #cml-azenlog}

- Activer la journalisation du contenu dans l'abonnement

    ```python
    subscription.payload_logging.enable()
    ```

- Obtenir les détails de la journalisation

    ```python
    subscription.payload_logging.get_details()
    ```

### Evaluation et journalisation du contenu
{: #cml-azscore}

- Evaluez votre modèle. Pour un exemple complet, voir le
[
bloc-notes Working with Azure Machine Learning Studio Engine
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: new_window}.

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

- Stocker la demande et la réponse dans la table de journalisation du contenu :

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Remarque** : Pour les langages autres que Python, vous pouvez également effectuer la journalisation du contenu directement, avec une API REST.

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

## Utilisation du moteur d'apprentissage automatique Amazon SageMaker
{: #cml-smconfig}

### Lier votre moteur AWS SageMaker ML
{: #cml-smbind}

- Un moteur non-WML se lie comme personnalisé, ce qui signifie qu'il s'agit seulement de métadonnées ; il n'y a pas d'intégration directe avec le service non-WML.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Vous pouvez voir votre liaison de service avec la commande suivante :

    ```python
    client.data_mart.bindings.list()
    ```

    ![Liaison SageMaker ML](images/ml-sagemaker-bind.png)

### Ajouter un abonnement Amazon SageMaker ML
{: #cml-smsub}

- Ajouter un abonnement

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Obtenir la liste des abonnements

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Activer la journalisation du contenu
{: #cml-smenlog}

- Activer la journalisation du contenu dans l'abonnement

    ```python
    subscription.payload_logging.enable()
    ```

- Obtenir les détails de la journalisation

    ```python
    subscription.payload_logging.get_details()
    ```

### Evaluation et journalisation du contenu
{: #cml-smscore}

- Evaluez votre modèle. Pour un exemple complet, voir le
[
bloc-notes Working with SageMaker Machine Learning Engine
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: new_window}.

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

- Stocker la demande et la réponse dans la table de journalisation du contenu :

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Remarque** : Pour les langages autres que Python, vous pouvez également effectuer la journalisation du contenu directement, avec une API REST.

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

## Etapes suivantes
{: #cml-next}

- Pour continuer avec le client {{site.data.keyword.aios_short}}, voir
[Spécification d'une base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db).

- Pour continuer avec la bibliothèque de commandes Python,
voir la [documentation du client Python
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://ai-openscale-python-client.mybluemix.net/){: new_window}.
