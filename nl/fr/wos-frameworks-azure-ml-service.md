---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Infrastructures Microsoft Azure ML Service
{: #frmwrks-azure-service}

Vous pouvez utiliser Microsoft Azure ML Service pour effectuer une journalisation du contenu utile et des retours,
et pour mesurer l'exactitude de performance, la détection de biais à l'exécution, l'explicabilité et la fonction de débiaisement automatique dans {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures Microsoft Azure Machine Learning Service suivantes :
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Native | Classification | Structuré |
| scikit-learn | Classification | Structuré |
| scikit-learn | Régression | Structuré |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

## Ajout de Microsoft Azure ML Service à {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

Vous pouvez configurer {{site.data.keyword.aios_short}} pour qu'il fonctionne avec Microsoft Azure ML Service
à l'aide d'une des méthodes suivantes :

- Si c'est la première fois que vous ajoutez un fournisseur d'apprentissage automatique à {{site.data.keyword.aios_short}},
vous pouvez utiliser l'interface de configuration. Pour plus d'informations, consultez
[Spécification d'une instance Microsoft Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice).
- Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Cette méthode est obligatoire si vous voulez avoir plusieurs fournisseurs. Pour savoir comment effectuer cela par programme, consultez [Lier votre moteur d'apprentissage automatique Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).


{{site.data.keyword.aios_short}} appelle différents points d'extrémité REST nécessaires à son interaction avec Azure ML Service. Vous devez pour cela lier Azure Machine Learning Service à {{site.data.keyword.aios_short}}.

1. Créez un principal Azure Active Directory Service.
2. Spécifiez les détails d'identification lorsque vous ajoutez la liaison au service Azure ML Service. Vous pouvez pour cela passer par l'interface utilisateur ou par le SDK Python de {{site.data.keyword.aios_short}}.

## Conditions à remplir par les fichiers de demande et de réponse JSON
{: #frmwrks-azureservice-JSON}

Pour que {{site.data.keyword.aios_short}} fonctionne avec Azure ML Service, les déploiements de service web que vous créez doivent remplir certaines conditions. Ils doivent accepter des demandes JSON et retourner des réponses JSON remplissant les conditions décrites ci-dessous.

### Format à respecter par les demandes JSON envoyées aux services web
{: #frmwrks-azureservice-JSON-sample-request}

- Le corps de la demande envoyée à l'API REST doit être un document JSON contenant un unique tableau JSON d'objets JSON.
- Le tableau JSON doit se nommer `"input"`.
- Chaque objet JSON ne peut inclure que des paires clé-valeur simples, les seules valeurs acceptées étant les chaînes, les nombres et les valeurs `true`, `false` et `null`
- Les valeurs ne peuvent pas elles-mêmes être des objets ou des tableaux JSON.
- Les différents objets du tableau JSON doivent tous avoir les mêmes clés spécifiées (et donc le même nombre de clés). Peu importe qu'une valeur non `null` soit disponible ou non pour chaque clé.


L'exemple de fichier JSON suivant remplit les conditions énoncées ci-dessus. Vous pouvez l'utiliser comme modèle pour créer vos propres fichiers de demande JSON :


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### Format à respecter par les réponses JSON reçues des services web
{: #frmwrks-azureservice-JSON-sample-response}

Tenez compte des points suivants lorsque vous créez un fichier de réponse JSON :

- Le corps de la réponse reçue de l'API REST doit être un document JSON contenant un unique tableau JSON d'objets JSON.
- Le tableau JSON doit se nommer `"output"`.
- Chaque objet JSON ne peut inclure que des paires clé-valeur, les seules valeurs acceptées étant les chaînes, les nombres, les valeurs `true`, `false` et `null` ou des tableaux qui ne contiennent pas d'autres objets ou tableaux JSON.
- Les valeurs ne peuvent pas elles-mêmes être des objets JSON.
- Les différents objets du tableau JSON doivent tous avoir les mêmes clés spécifiées (et donc le même nombre de clés). Peu importe qu'une valeur non `null` soit disponible ou non pour chaque clé.
- Pour les modèles de classification : le service web doit retourner un tableau de probabilités pour chaque classe, et l'ordre des probabilités doit être le même pour les différents objets JSON du tableau
  - Exemple : supposons que vous ayez un modèle de classification binaire qui prédit le risque de crédit, les deux classes possibles étant `Risk` ou `No Risk`
  - Pour chaque résultat retourné dans le tableau "output", les objets doivent contenir une paire clé-valeur incluant les probabilités dans un ordre fixe, sous la forme :
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

Par souci de cohérence vis-à-vis des outils visuels Azure ML utilisés tant dans Azure ML Studio que dans Azure ML Service, il est conseillé (mais pas obligatoire) d'adopter les noms de clé suivants :

- `"Scored Labels"` pour la clé de sortie représentant la valeur prédite du modèle
- `"Scored Probabilities"` pour la clé de sortie représentant le tableau de probabilités de chaque classe

L'exemple de fichier JSON suivant remplit les conditions énoncées ci-dessus. Vous pouvez l'utiliser comme modèle pour créer vos propres fichiers de réponse JSON :


```JSON
{
  "output": [
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## Exemples de bloc-notes
{: #frmwrks-azureservice-smpl-ntbks}

Les bloc-notes suivants montrent comment utiliser Microsoft Azure ML Service :

- [Exemples d'évaluation de modèle MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## Spécification d'une instance Microsoft Azure ML Service
{: #connect-azureservice}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de Microsoft Azure ML Service. Votre instance Azure ML Service est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Pour savoir comment effectuer cela par programme,
consultez [Lier votre moteur d'apprentissage automatique Microsoft Azure Service](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Connectez votre instance Azure ML Service
{: #ca-connect}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance Azure ML Service.

1.  Dans l'onglet **Configurer**, cliquez sur **Fournisseurs d'apprentissage automatique** dans le volet de navigation.
1.  Cliquez sur le bouton **Ajouter un fournisseur d'apprentissage automatique** puis sur le carreau **Microsoft Azure ML Service**.
1.  Entrez et sauvegardez vos identifiants :

    - ID client : chaîne de votre ID client, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Service.
    - Secret client : chaîne du secret, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Service.
    - Locataire : votre ID de locataire correspond à votre organisation et est une instance dédiée d'Azure AD. Pour le trouver, passez la souris sur le nom de votre compte pour obtenir l'ID annuaire / locataire,
ou bien sélectionnez Azure Active Directory > Propriétés > ID annuaire sur le portail Azure.
    - ID d'abonnement : identifiants d'abonnement qui identifient de manière unique votre abonnement à Microsoft Azure. L'ID d'abonnement constitue une partie de l'URI à chaque appel de service.

    Pour savoir comment obtenir vos identifiants Microsoft Azure, consultez la page
[How to:
Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.
    {: note}

1.  {{site.data.keyword.aios_short}} affiche vos modèles déployés ; sélectionnez ceux que vous voulez surveiller et cliquez sur **Configurer**.

Vous avez correctement sélectionné les déploiements.

## Journalisation du contenu utile avec le moteur Microsoft Azure ML Service
{: #cml-azsrvconfig}

### Lier votre moteur Microsoft Azure ML Service
{: #cml-azsrvbind}

Un moteur non-{{site.data.keyword.pm_full}} se lie comme personnalisé,
ce qui signifie qu'il s'agit seulement de métadonnées ; il n'y a pas d'intégration directe avec le service non-{{site.data.keyword.pm_full}}.
   
```
AZURE_ENGINE_CREDENTIALS = {
"client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
}

binding_uid = client.data_mart.bindings.add('Mon moteur Azure ML Service', AzureMachineLearningServiceInstance(AZURE_ENGINE_CREDENTIALS))


bindings_details = client.data_mart.bindings.get_details()
```
{: codeblock}

Vous pouvez voir votre liaison de service avec la commande suivante :

```
client.data_mart.bindings.list()
```
{: codeblock}

Exemple de sortie :

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### Ajouter un abonnement Microsoft Azure ML Service
{: #cml-azsrvsub}

Ajouter un abonnement

```
client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
```
{: codeblock}

Obtenir la liste des abonnements

```
subscriptions = client.data_mart.subscriptions.get_details()

subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
```
{: codeblock}

### Activer la journalisation du contenu utile
{: #cml-azsrvenlog}

Activer la journalisation du contenu utile dans l'abonnement

```
subscription.payload_logging.enable()
```
{: codeblock}

Obtenir les détails de la journalisation

```
subscription.payload_logging.get_details()
```
{: codeblock}

### Evaluation et journalisation du contenu utile
{: #cml-azsrvscore}

Evaluez votre modèle. Pour un exemple complet, consultez le
[bloc-notes
Working with Azure Machine Learning Service Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

Stocker la demande et la réponse dans la table de journalisation du contenu utile :

```
records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

subscription.payload_logging.store(records=records_list)
```
{: codeblock}
{: python}
   
Pour les langages autres que Python, vous pouvez également effectuer la journalisation du contenu utile directement, avec une API REST.
   
```
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
{: codeblock}
{: json}


```
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
{: codeblock}



## Etapes suivantes
{: #ca-next}

- {{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

