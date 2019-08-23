---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

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

# Infrastructures Microsoft Azure ML Studio
{: #frmwrks-azure}

Vous pouvez utiliser Microsoft Azure ML Studio pour effectuer une journalisation du contenu utile et des retours,
et pour mesurer l'exactitude de performance, la détection de biais à l'exécution, l'explicabilité et la fonction de débiaisement automatique dans {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures Microsoft Azure Machine Learning Studio suivantes :
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Native | Classification | Structuré |
| Native | Régression | Structuré |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

## Ajout de Microsoft Azure ML Studio à {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

Vous pouvez configurer {{site.data.keyword.aios_short}} pour qu'il fonctionne avec Microsoft Azure ML Studio
à l'aide d'une des méthodes suivantes :

- Si c'est la première fois que vous ajoutez un fournisseur d'apprentissage automatique à {{site.data.keyword.aios_short}},
vous pouvez utiliser l'interface de configuration. Pour plus d'informations, consultez
[Spécification d'une instance Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Cette méthode est obligatoire si vous voulez avoir plusieurs fournisseurs. Pour savoir comment effectuer cela par programme, consultez [Lier votre moteur d'apprentissage automatique Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


## Exemples de bloc-notes
{: #frmwrks-azure-smpl-ntbks}

Les bloc-notes suivants montrent comment utiliser Microsoft Azure ML Studio :

- [Création d'un magasin de données, surveillance du déploiement de modèle et analyse des données](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Exemples d'évaluation de modèle MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Explorer plus avant
{: #frmwrks-azure-mediumblogs}

-[Surveiller l'apprentissage automatique Azure avec Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Consume an Azure Machine Learning model deployed as a web service](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## Spécification d'une instance Microsoft Azure ML Studio
{: #connect-azure}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de Microsoft Azure ML Studio. Votre instance Azure ML Studio est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Pour savoir comment effectuer cela par programme, consultez [Lier votre moteur d'apprentissage automatique Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

### Connectez votre instance Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance Azure ML Studio.

1.  Dans l'onglet **Configurer**, cliquez sur **Fournisseurs d'apprentissage automatique** dans le volet de navigation.

    ![L'écran de sélection du fournisseur d'apprentissage automatique est affiché, avec un carreau pour chaque moteur d'apprentissage automatique accepté](images/wos-machine-learning-providers-selection.png)

1.  Cliquez sur le bouton **Ajouter un fournisseur d'apprentissage automatique** puis sur le carreau **Microsoft Azure ML Studio**.

    ![Entrée des identifiants Azure ML Studio](images/connect-azure-cred.png)

1.  Entrez et sauvegardez vos identifiants :

    - ID client : chaîne de votre ID client, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Studio.
    - Secret client : chaîne du secret, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Studio.
    - Locataire : votre ID de locataire correspond à votre organisation et est une instance dédiée d'Azure AD. Pour le trouver, passez la souris sur le nom de votre compte pour obtenir l'ID annuaire / locataire,
ou bien sélectionnez Azure Active Directory > Propriétés > ID annuaire sur le portail Azure.
    - ID d'abonnement : identifiants d'abonnement qui identifient de manière unique votre abonnement à Microsoft Azure. L'ID d'abonnement constitue une partie de l'URI à chaque appel de service.

    Pour savoir comment obtenir vos identifiants Microsoft Azure, consultez la page
[How to:
Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.
    {: note}

1.  {{site.data.keyword.aios_short}} affiche vos modèles déployés ; sélectionnez ceux que vous voulez surveiller et cliquez sur **Configurer**.

Vous avez correctement sélectionné les déploiements.

## Journalisation du contenu utile avec le moteur Microsoft Azure Machine Learning Studio
{: #cml-azconfig}

### Lier votre moteur d'apprentissage automatique Microsoft Azure
{: #cml-azbind}

- Un moteur non-{{site.data.keyword.pm_full}} se lie comme personnalisé,
ce qui signifie qu'il s'agit seulement de métadonnées ; il n'y a pas d'intégration directe avec le service non-{{site.data.keyword.pm_full}}.

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid_2 = client.data_mart.bindings.add('Mon moteur Azure ML Studio', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Vous pouvez voir votre liaison de service avec la commande suivante :

    ```python
    client.data_mart.bindings.list()
    ```

    ![Liaison Azure ML](images/ml-azure-bind.png)

### Ajouter un abonnement Microsoft Azure ML Studio
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

### Activer la journalisation du contenu utile
{: #cml-azenlog}

- Activer la journalisation du contenu utile dans l'abonnement

    ```python
    subscription.payload_logging.enable()
    ```

- Obtenir les détails de la journalisation

    ```python
    subscription.payload_logging.get_details()
    ```

### Evaluation et journalisation du contenu utile
{: #cml-azscore}

- Evaluez votre modèle. Pour un exemple complet, consultez le
[bloc-notes
Working with Azure Machine Learning Studio Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

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
{: #ca-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
