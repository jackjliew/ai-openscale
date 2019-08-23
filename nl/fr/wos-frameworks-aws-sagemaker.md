---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Infrastructures Amazon SageMaker
{: #frmwrks-aws-sage}

Vous pouvez utiliser Amazon SageMaker pour effectuer une journalisation du contenu utile et des retours,
et pour mesurer l'exactitude de performance, la détection de biais à l'exécution, l'explicabilité et la fonction de débiaisement automatique dans {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures Amazon SageMaker suivantes :
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Native | Classification | Structuré |
| Native | Régression<sup>1</sup> | Structuré |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

<sup>1</sup>La prise en charge des modèles de régression n'inclut pas l'ampleur de la dérive.

## Ajout d'Amazon SageMaker à {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

Vous pouvez configurer {{site.data.keyword.aios_short}} pour qu'il fonctionne avec Amazon SageMaker
à l'aide d'une des méthodes suivantes :

- Si c'est la première fois que vous ajoutez un fournisseur d'apprentissage automatique à {{site.data.keyword.aios_short}},
vous pouvez utiliser l'interface de configuration. Pour plus d'informations, consultez
[Spécification d'une instance Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Cette méthode est obligatoire si vous voulez avoir plusieurs fournisseurs. Pour savoir comment effectuer cela par programme, consultez [Lier votre moteur d'apprentissage automatique Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Exemples de bloc-notes
{: #frmwrks-aws-sage-smpl-ntbks}

Les bloc-notes suivants montrent comment utiliser Amazon SageMaker :

- [Création et déploiement du modèle de prévision de risque de crédit](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Création d'un magasin de données, surveillance du déploiement de modèle et analyse des données](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## Spécification d'une instance de service Amazon SageMaker ML
{: #csm-connect}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de service Amazon SageMaker. Votre instance de service Amazon SageMaker est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Pour savoir comment effectuer cela par programme, consultez [Lier votre moteur d'apprentissage automatique Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

### Connectez votre instance de service Amazon SageMaker
{: #csm-config}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance de service Amazon SageMaker.

1.  Dans l'onglet **Configurer**, cliquez sur **Fournisseurs d'apprentissage automatique** dans le volet de navigation.

    ![L'écran de sélection du fournisseur d'apprentissage automatique est affiché, avec un carreau pour chaque moteur d'apprentissage automatique accepté](images/wos-machine-learning-providers-selection.png)

1.  Cliquez sur le bouton **Ajouter un fournisseur d'apprentissage automatique** puis sur le carreau **Amazon SageMaker**.

    ![Entrée des identifiants du service Amazon SageMaker](images/connect-sage-cred.png)

1.  Entrez et sauvegardez vos identifiants :

    - ID clé d'accès : votre ID clé d'accès AWS, `aws_access_key_id`,
qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à AWS.
    - Clé d'accès secrète : votre clé d'accès secrète AWS, `aws_secret_access_key`,
qui est nécessaire pour vérifier qui vous êtes et pour authentifier et autoriser les appels que vous faites à AWS.
    - Région : entrez la région où votre ID clé d'accès a été créé. Les clés sont stockées et utilisées dans la région dans laquelle elles ont été créées et elles ne peuvent pas être transférées dans une autre région. 

1.  {{site.data.keyword.aios_short}} affiche vos modèles déployés ; sélectionnez ceux que vous voulez surveiller.

## Journalisation du contenu utile avec le moteur d'apprentissage automatique Amazon SageMaker
{: #cml-smconfig}

### Lier votre moteur d'apprentissage automatique Amazon SageMaker
{: #cml-smbind}

- Un moteur non-{{site.data.keyword.pm_full}} se lie comme personnalisé,
ce qui signifie qu'il s'agit seulement de métadonnées ; il n'y a pas d'intégration directe avec le service non-{{site.data.keyword.pm_full}}.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('Mon moteur SageMaker', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

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

### Activer la journalisation du contenu utile
{: #cml-smenlog}

- Activer la journalisation du contenu utile dans l'abonnement

    ```python
    subscription.payload_logging.enable()
    ```

- Obtenir les détails de la journalisation

    ```python
    subscription.payload_logging.get_details()
    ```

### Evaluation et journalisation du contenu utile
{: #cml-smscore}

- Evaluez votre modèle. Pour un exemple complet, consultez le
[bloc-notes
Working with SageMaker Machine Learning Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}.


- Stocker la demande et la réponse dans la table de journalisation du contenu utile :

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

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

## Etapes suivantes
{: #csm-next}

- {{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [Surveiller l'apprentissage automatique Sagemaker avec Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
