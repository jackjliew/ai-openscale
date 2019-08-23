---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Infrastructures ML personnalisées
{: #frmwrks-custom}

Vous pouvez utiliser votre infrastructure d'apprentissage automatique personnalisée pour effectuer une journalisation du contenu utile et des retours,
et pour mesurer l'exactitude de performance, la détection de biais à l'exécution, l'explicabilité et la fonction de débiaisement automatique dans {{site.data.keyword.aios_full}}.
L'infrastructure d'apprentissage automatique personnalisée doit être équivalente à {{site.data.keywor.pm_full}}.

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures d'apprentissage automatique personnalisé suivantes :
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Equivalente à {{site.data.keyword.pm_full}} | Classification | Structuré |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

## Ajout d'un moteur d'apprentissage automatique personnalisé à {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

Vous pouvez configurer {{site.data.keyword.aios_short}} pour qu'il fonctionne avec un fournisseur d'apprentissage automatique personnalisé
à l'aide d'une des méthodes suivantes :

- Si c'est la première fois que vous ajoutez un fournisseur d'apprentissage automatique personnalisé à {{site.data.keyword.aios_short}},
vous pouvez utiliser l'interface de configuration. Pour plus d'informations, consultez
[Specifying a custom machine learning instance](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Cette méthode est obligatoire si vous voulez avoir plusieurs fournisseurs. Pour savoir comment effectuer cela par programme, consultez [Lier votre moteur d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Exemples de bloc-notes
{: #frmwrks-custom-smpl-ntbks}

- [Création d'un moteur d'apprentissage automatique personnalisé avec un cluster Kubernetes](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Création d'un magasin de données, surveillance du déploiement de modèle et analyse des données](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Explorer plus avant
{: #frmwrks-custom-mediumblogs}

[Surveiller un moteur d'apprentissage automatique personnalisé avec Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}

## Moteur d'apprentissage automatique personnalisé
{: #fmrk-workaround-customengine}

Un moteur d'apprentissage automatique personnalisé fournit l'infrastructure et l'hébergement pour les modèles et les applications web d'apprentissage automatique. Pour être supporté par {{site.data.keyword.aios_short}}, il doit respecter les exigences suivantes :

- Exposer deux types de points d'extrémité d'API REST :

   * point d'extrémité de reconnaissance (liste GET des déploiements et détails)
   * points d'extrémité d'évaluation (évaluation en ligne et en temps réel)

- Tous les points d'extrémité doivent être compatibles avec la spécification swagger pour être supportés.

- Le contenu utile d'entrée et la sortie du déploiement doivent être conformes au format de fichier JSON décrit dans la spécification.

Actuellement, seuls les formats `BasicAuth` et `none` sont supportés.
{: Note}

L'exemple suivant présente la spécification des points d'extrémité d'API REST :

![Affichage de la spécification des points d'extrémité d'API REST du document swagger](images/wosdeployments.png)


L'exemple suivant montre le format d'un contenu utile d'entrée :

![Exemple de contenu utile d'entrée](images/wosinputdata.png)


## Dans quels cas faut-il utiliser un moteur d'apprentissage automatique personnalisé ?
{: #fmrk-workaround-enging-choice}

L'utilisation d'un moteur d'apprentissage automatique personnalisé est recommandée dans les situations suivantes :

- Vous n'utilisez aucun produit tout prêt pour vos modèles d'apprentissage automatique. Vous venez de développer votre propre système. {{site.data.keyword.aios_short}} n'offre, et n'offrira, aucune prise en charge directe dans ce cas.
- Le moteur tiers que vous utilisez n'est pas encore supporté par {{site.data.keyword.aios_short}}. Dans ce cas, vous pouvez envisager de développer un moteur d'apprentissage automatique personnalisé qui encapsulera vos déploiements initiaux ou natifs.

## Spécification d'une instance de service ML personnalisé
{: #co-connect}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de service. Votre instance de service est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

## Connecter votre instance de service personnalisé
{: #co-config}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance de service. Vous pouvez connecter un service personnalisé

1.  Dans l'onglet **Configurer**, cliquez sur **Fournisseurs d'apprentissage automatique** dans le volet de navigation.

   ![L'écran de sélection du fournisseur d'apprentissage automatique est affiché, avec un carreau pour chaque moteur d'apprentissage automatique accepté](images/wos-machine-learning-providers-selection.png)

2. Cliquez sur le bouton **Ajouter un fournisseur d'apprentissage automatique** puis sur le carreau **Environnement personnalisé**.

   ![Ecran de configuration du fournisseur d'apprentissage automatique personnalisé avec des champs pour les identifiants, le nom de l'instance et sa description](images/ml-custom-provider.png)

3. Entrez un nom et une description pour votre fournisseur d'apprentissage automatique personnalisé, puis cliquez sur **Suivant**. 

4. Choisissez entre vous connecter à vos déploiements [en demandant leur liste](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) et
vous connecter [en entrant individuellement les points d'extrémité d'évaluation](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![Ecran de connexion aux déploiements avec des options pour demander la liste des déploiements ou entrer un point d'extrémité d'évaluation spécifique](images/ml-custom-connect-deployments.png)
    
5. Cliquez sur **Suivant**.

### Demande de la liste des déploiements
{: #co-config-request-list}

1. Si vous avez sélectionné le carreau **Demande de la liste des déploiements**, entrez vos identifiants et le point d'extrémité d'API, puis cliquez sur **Enregistrer**.

   ![écran de liste des déploiements avec des champs pour entrer les identifiants du service et un point d'extrémité d'API](images/connect-custom-cred.png)

2. Après avoir sauvegardé votre installation d'apprentissage automatique, retournez au **Tableau de bord**, cliquez sur l'onglet **Analyses**, puis sur le bouton **Ajouter au tableau de bord**.

3. Sélectionnez un déploiement dans la liste et cliquez sur **Configurer**.

Vous êtes maintenant prêt à configurer les moniteurs.

### Fourniture de points d'extrémité d'évaluation individuels
{: #co-config-scoring-endpoints}

1. Si vous avez sélectionné le carreau **Saisie des points d'extrémité d'évaluation individuels**, entrez vos identifiants pour le point d'extrémité d'API, puis cliquez sur **Enregistrer**.

2. Après avoir sauvegardé votre installation d'apprentissage automatique, retournez au **Tableau de bord**, cliquez sur l'onglet **Analyses**, puis sur le bouton **Ajouter au tableau de bord**.

3. Cliquez sur le bouton **Ajouter un point d'extrémité**.

4. Dans le menu déroulant, sélectionnez l'environnement personnalisé, tapez le nom du déploiement et le point d'extrémité d'API, puis cliquez sur **Enregistrer**.

Vous êtes maintenant prêt à configurer les moniteurs.

### Fonctionnement
{: #co-works}

L'image suivante montre le support de l'environnement personnalisé :

![Affichage du graphique de travaux personnalisé. Il fournit des zones pour l'environnement personnalisé avec l'API client et l'API Watson OpenScale](images/custom-how-works.png)

Vous pouvez également consulter les liens suivants :

[API de journalisation du contenu utile {{site.data.keyword.aios_short}}](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[API de déploiement personnalisé](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[SDK de liaison du client Python](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[Utilisation du moteur d'apprentissage automatique personnalisé](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[SDK Python pour IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **Critères d'entrée pour que le modèle supporte les moniteurs**

  Votre modèle doit prendre en entrée un vecteur de caractéristique, qui est fondamentalement une collection de zones nommées avec leur valeur
(incluant les zones dont le biais est surveillé) :

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  Dans cet exemple, `“age”` pourrait être une zone dont quelqu'un évalue l'équité.

  Si l'entrée est un tenseur/matrice,
qui est transformé à partir de l'espace de caractéristiques d'entrée
(ce qui est souvent le cas dans l'apprentissage en profondeur à partir de texte ou d'images),
le modèle ne peut pas être traité par la plateforme {{site.data.keyword.aios_short}} dans l'édition actuelle. Par extension, les modèles d'apprentissage en profondeur avec des entrées texte ou images ne peuvent pas être traités pour la détection et l'atténuation de biais.

  En outre, des données de formation doivent être chargées pour prendre en charge l'explicabilité.

  Pour l'explicabilité sur du texte, le texte complet doit faire partie des caractéristiques. L'explicabilité sur les images pour un modèle personnalisé n'est pas prise en charge dans l'édition actuelle.
  {: note}

- **Critères de sortie pour que le modèle supporte les moniteurs**

  Votre modèle doit sortir le vecteur de caractéristique d'entrée avec les probabilités de prévision de diverses de ses classes.

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  Dans cet exemple, `"personal”` et `“camping”` sont les classes possibles,
et les scores de chaque sortie d'évaluation sont affectés aux deux classes. S'il manque les probabilités de prévision, la détection de biais fonctionnera mais pas le débiais automatique.

  La sortie d'évaluation précédente doit être accessible depuis un point d'extrémité d'évaluation actif que {{site.data.keyword.aios_short}} peut appeler par REST. Pour AzureML, SageMaker et {{site.data.keyword.pm_full}}, {{site.data.keyword.aios_short}} se connecte directement aux points d'extrémité d'évaluation natifs
(donc vous n'avez pas à vous inquiéter de l'implémentation de la spécification d'évaluation).

## Exemples de moteur d'apprentissage automatique personnalisé
{: #fmrk-workaround-cstmmlsengex}

Utilisez les exemples suivants pour configurer votre propre moteur d'apprentissage automatique personnalisé.
{: shortdesc}

### Python et Flask
{: #fmrk-workaround-pandflask}

L'[exemple de moteur d'apprentissage automatique personnalisé
publié sur git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
utilise Python et Flask pour servir le modèle scikit-learn.

Le [fichier README](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external} explique
comment déployer l'application en local pour des tests ainsi que comme application cf sur IBM Cloud. L'implémentation des points d'extrémité d'API REST se trouve dans le
[fichier app.py](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py){: external}.

### Node.js
{: #fmrk-workaround-nodejs}

Vous trouverez également un exemple de moteur d'apprentissage automatique personnalisé
écrit en [Node.js ici](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs){: external}.

### Schéma de code end2end
{: #fmrk-workaround-e2ecode}

[Schéma de code](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale){: external}
présentant un exemple end2end de déploiement de moteur personnalisé et d'intégration à {{site.data.keyword.aios_short}}.

## Journalisation du contenu utile avec le moteur d'apprentissage automatique personnalisé
{: #cml-cusconfig}

### Lier votre moteur d'apprentissage automatique personnalisé
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

### Activer la journalisation du contenu utile
{: #cml-cusenlog}

- Activer la journalisation du contenu utile dans l'abonnement

    ```python
    subscription.payload_logging.enable()
    ```

- Obtenir les détails de la journalisation

    ```python
    subscription.payload_logging.get_details()
    ```

Pour plus d'informations, consultez [Journalisation du contenu utile](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

### Evaluation et journalisation du contenu utile
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


## Etapes suivantes
{: #fmrk-workaround-nxt-steps-over}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).

Implémentez votre propre solution en utilisant l'un de ces
[Exemples d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).
