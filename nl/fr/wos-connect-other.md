---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# Spécification d'une instance de service ML personnalisé
{: #co-connect}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de service. Votre instance de service est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

## Connecter votre instance de service personnalisé
{: #co-config}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance de service. Vous pouvez connecter un service personnalisé

1. Dans l'onglet **Configurer**, cliquez sur **Fournisseur d'apprentissage automatique**.
Selon votre environnement, tous les fournisseurs suivants peuvent ne pas être affichés :

   ![L'écran de sélection du fournisseur d'apprentissage automatique est affiché, avec un carreau pour chaque moteur d'apprentissage automatique accepté](images/wos-machine-learning-providers-selection.png)

2. Sélectionnez le carreau **Environnement personnalisé**.

   ![écran de configuration du fournisseur d'apprentissage automatique personnalisé avec des champs pour les identifiants, le nom de l'instance et sa description](images/ml-custom-provider.png)

1.  Entrez et sauvegardez vos identifiants :

    - Nom d'utilisateur : nom d'utilisateur de votre fournisseur d'apprentissage automatique personnalisé.
    - Mot de passe : mot de passe de votre fournisseur d'apprentissage automatique personnalisé.
    - Nom d'instance du fournisseur de services : nom spécifique attribué à ce fournisseur de services.
    - Description : (facultatif) votre description en langage ordinaire de cette instance du fournisseur de services. Si vous avez des environnements de production et de test, c'est un bon endroit pour indiquer ces informations.

4. Choisissez entre vous connecter à vos déploiements [en demandant leur liste](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) et
vous connecter [en entrant individuellement les points d'extrémité d'évaluation](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![Sélection de Custom](images/ml-custom-connect-deployments.png)
    
5. Cliquez sur **Suivant**.

### Demande de la liste des déploiements
{: #co-config-request-list}

1. Si vous avez sélectionné le carreau **Demande de la liste des déploiements**, entrez vos identifiants et le point d'extrémité d'API, puis cliquez sur **Enregistrer**.

   ![Entrée des identifiants du service](images/connect-custom-cred.png)

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

![Fonctionnement du service personnalisé](images/custom-how-works.png)

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

### Etapes suivantes
{: #co-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
