---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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

# Tutoriel sur le SDK Python (avancé)
{: #crt-ov}

## Scénario
{: #crt-scenario}

Les organismes de prêt classiques cherchent à
élargir leur portefeuille numérique de services financiers à un public plus vaste et plus diversifié,
ce qui nécessite une nouvelle approche de la modélisation du risque de crédit. Leurs équipes de science des données s'appuient actuellement sur des techniques de modélisation standard,
comme les arbres de décision et la régression logistique,
qui fonctionnent bien pour des ensembles de données modérés, et font des recommandations qui peuvent être facilement expliquées. Cela répond aux exigences réglementaires selon lesquelles les décisions de prêt doivent être transparentes et explicables.

Pour offrir un accès au crédit à une population plus vaste et plus risquée,
les antécédents de crédit des demandeurs doivent s'étendre au-delà du crédit traditionnel,
comme les prêts hypothécaires et les prêts automobiles,
à d'autres sources de crédit comme les antécédents de paiement des services publics (eau, électricité, etc.) et des forfaits de téléphonie mobile,
ainsi qu'à la formation et au fonctions occupées. Ces nouvelles sources de données sont prometteuses
mais elles introduisent également un risque en augmentant la probabilité de corrélations inattendues
introduisant un biais en fonction de l'âge, du sexe ou d'autres traits personnels du demandeur.

Les techniques de science des données les plus adaptées à ces ensembles de données divers,
telles que le gradient d'arbres et les réseaux neuronaux, peuvent générer des modèles de risque très exacts, mais à un coût. De tels modèles "boîte noire" génèrent des prévisions opaques qui doivent d'une façon ou d'une autre devenir transparentes,
pour garantir l'approbation réglementaire, par exemple quant à l'article 22 du RGPD (règlement général sur la protection des données)
ou à la loi fédérale américaine FCRA (Fair Credit Reporting Act) gérée par le Consumer Financial Protection Bureau.

Le modèle de risque de crédit fourni dans ce tutoriel utilise un ensemble de données de formation contenant 20 attributs sur chaque demandeur de prêt. Deux de ces attributs, l'âge et le sexe, peuvent être testés quant au biais. Ce tutoriel se concentrera sur le biais par rapport à ces deux attributs. Pour plus d'informations sur les données de formation, voir [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

{{site.data.keyword.aios_short}}
surveillera la propension du modèle déployé à donner un résultat favorable ("aucun risque") pour un groupe (le groupe de référence) sur un autre (le groupe surveillé). Dans ce tutoriel, le groupe surveillé est celui des `femmes` pour le sexe, et `18 à 25 ans` pour l'âge.

## Conditions requises
{: #crt-prereqs}

Ce tutoriel utilise un bloc-notes Jupyter qui doit être exécuté dans un projet Watson Studio, en utilisant un environnement d'exécution "Python 3.5 avec Spark". Il nécessite des identifiants de service pour les services {{site.data.keyword.cloud_notm}} suivants :

- Cloud Object Storage (pour stocker votre projet Watson Studio)
- {{site.data.keyword.aios_short}}
- Watson Machine Learning
- (Facultatif) Databases for PostgreSQL ou Db2 Warehouse

Le bloc-notes Jupyter formera, créera et déploiera un modèle de risque de crédit allemand,
il configurera {{site.data.keyword.aios_short}} pour surveiller ce déploiement,
et il fournira sept jours d'enregistrements et de mesures à afficher dans le tableau de bord Analyses de {{site.data.keyword.aios_short}}. Vous pouvez également configurer le modèle pour un apprentissage continu avec Watson Studio et Spark.

## Introduction
{: #crt-intro}

Dans ce tutoriel, vous allez :

- Mettre à disposition des services d'apprentissage automatique et de stockage {{site.data.keyword.cloud_notm}}
- Définir un projet Watson Studio et exécuter un bloc-notes Python pour créer, former et déployer un modèle d'apprentissage automatique
- Exécuter un bloc-notes Python pour créer un magasin de données, configurer les moniteurs de performances, d'exactitude et d'équité, et créer des données à surveiller
- Afficher les résultats dans l'onglet Analyses de {{site.data.keyword.aios_short}}

## Mettez à disposition les services {{site.data.keyword.cloud_notm}}
{: #crt-services}

Connectez-vous à votre [compte {{site.data.keyword.cloud_notm}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window} avec votre {{site.data.keyword.ibmid}}. Lors de la mise à disposition des services, en particulier si vous utilisez Db2 Warehouse, vérifiez que l'organisation et l'espace sélectionnés sont les mêmes pour tous les services.

### Créez un compte {{site.data.keyword.DSX}}
{: #crt-wstudio}

- Si vous n'en avez pas déjà une associée à votre compte, [créez une instance de {{site.data.keyword.DSX}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/watson-studio){: new_window} :

  ![Watson Studio](images/watson_studio.png)

- Donnez un nom à votre service, choisissez le forfait Lite (gratuit) et cliquez sur le bouton **Créer**.

### Mettez à disposition un service {{site.data.keyword.cos_full_notm}}
{: #crt-cos}

- Si vous n'en avez pas déjà un associé à votre compte, [mettez à disposition un service {{site.data.keyword.cos_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} :

  ![Object Storage](images/object_storage.png)

- Donnez un nom à votre service, choisissez le forfait Lite (gratuit) et cliquez sur le bouton **Créer**.

### Mettez à disposition un service {{site.data.keyword.pm_full}}
{: #crt-wml}

- Si vous n'en avez pas déjà une associée à votre compte, [mettez à disposition une instance de {{site.data.keyword.pm_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/machine-learning){: new_window} :

  ![Machine Learning](images/machine_learning.png)

- Donnez un nom à votre service, choisissez le forfait Lite (gratuit) et cliquez sur le bouton **Créer**.

### (Facultatif) Mettez à disposition un service Databases for PostgreSQL ou DB2 Warehouse
{: #crt-db2}

Si vous avez un compte {{site.data.keyword.cloud_notm}} payant,
vous pouvez mettre à disposition un service `Databases for PostgreSQL` ou `Db2 Warehouse`
pour profiter pleinement de l'intégration avec {{site.data.keyword.DSX}} et des services d'apprentissage continu. Si vous choisissez de ne pas mettre à disposition un service payant,
vous pouvez utiliser le stockage PostgreSQL interne gratuit
avec {{site.data.keyword.aios_short}}, mais vous ne pourrez pas configurer l'apprentissage continu pour votre modèle.

- Si vous n'en avez pas déjà un associé à votre compte,
[mettez à disposition un service Databases for PostgreSQL
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/databases-for-postgresql)
ou [un service Db2 Warehouse
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/db2-warehouse) :

  ![DB for Postgres](images/dbpostgres.png)

  ![Db2 Warehouse](images/db2_warehouse.png)

- Donnez un nom à votre service, choisissez le forfait Standard (Databases for PostgreSQL) ou le forfait Entry (Db2 Warehouse) et cliquez sur le bouton **Créer**.

## Définissez un projet {{site.data.keyword.DSX}}
{: #crt-set-wstudio}

- Connectez-vous à votre compte [{{site.data.keyword.DSX}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.ibm.com/){: new_window}. Cliquez sur {{site.data.keyword.avatar}} et vérifiez que le compte que vous utilisez est bien celui que vous avez utilisé pour créer vos services {{site.data.keyword.cloud_notm}} :

  ![Même compte](images/same_account.png)

- Dans {{site.data.keyword.DSX}}, commencez par créer un nouveau projet. Sélectionnez "Créer un projet" :

  ![Création d'un projet Watson Studio](images/studio_create_proj.png)

- Sélectionnez le carreau **Standard** pour créer le projet :

  ![Sélection d'un projet Watson Studio standard](images/studio_create_standard.png)

- Donnez à votre projet un nom et une description,
assurez-vous que le service Cloud Object Storage que vous avez créé soit sélectionné dans la liste déroulante **Stockage**
et cliquez sur **Créer**.

## Créez et déployez un modèle {{site.data.keyword.pm_short}}
{: #crt-make-model}

### Ajoutez le bloc-notes `Working with Watson Machine Learning` à votre projet {{site.data.keyword.DSX}}
{: #crt-add-notebook}

- Téléchargez le fichier suivant :

    - [Working with Watson Machine Learning
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Dans l'onglet **Actifs** de votre projet {{site.data.keyword.DSX}},
cliquez sur le bouton **Ajouter au projet** et sélectionnez **Bloc-notes** dans la liste déroulante :

  ![Ajout d'une connexion](images/add_notebook.png)

- Sélectionnez **A partir d'un fichier** :

  ![Formulaire de nouveau bloc-notes](images/new_notebook_name.png)

- Cliquez ensuite sur le bouton **Choisir un fichier** et sélectionnez le fichier de bloc-notes "german_credit_lab.ipynb" que vous avez téléchargé :

  ![Formulaire de nouveau bloc-notes](images/new_notebook_name2a.png)

- Dans la section **Sélectionner l'environnement d'exécution**, choisissez un environnement Python 3.5 avec l'option Spark :

- Cliquez sur **Créer un bloc-notes**.

### Editez et exécutez le bloc-notes `Working with Watson Machine Learning`
{: #crt-edit-notebook}

Le bloc-notes `Working with Watson Machine Learning` contient des instructions détaillées pour chaque étape du code Python que vous allez exécutez. Au fur et à mesure que vous avancerez, prenez le temps de comprendre ce que fait chaque commande.
{: tip}

- Dans l'onglet **Actifs** de votre projet Watson Studio,
cliquez sur l'icône **Editer** en regard du bloc-notes `Working with Watson Machine Learning` afin d'éditer celui-ci.

- Dans la section "Provision services and configure credentials", effectuez les modifications suivantes :

    - Créez, copiez et collez une clé d'API {{site.data.keyword.cloud_notm}} en suivant les instructions.

    - Remplacez les identifiants du service Watson Machine Learning (WML) par ceux que vous avez créés.

    - Remplacez les identifiants de base de données par ceux que vous avez créés pour Databases for PostgreSQL.

    - Si vous avez configuré {{site.data.keyword.aios_short}}
pour l'utilisation d'une base de données PostgreSQL interne gratuite comme magasin de données,
vous pouvez passer à un nouveau magasin de données utilisant votre service Databases for PostgreSQL. Pour supprimer votre ancienne configuration PostgreSQL et en créer une nouvelle, définissez la variable KEEP_MY_INTERNAL_POSTGRES à `False`.

        Le bloc-notes supprimera le magasin de données PostgreSQL interne existant et créera un nouveau magasin de données avec les identifiants de base de données fournis. **Aucune migration de données n'aura lieu**.
        {: important}

- Une fois que vous avez mis à disposition vos services et entré vos identifiants, le bloc-notes est prêt à s'exécuter. Cliquez sur l'élément de menu **Noyau** et sélectionnez **Redémarrer et effacer la sortie** dans le menu :

  ![Redémarrer et effacer](images/restart_and_clear.png)

- Maintenant, exécutez chaque étape du bloc-notes en séquence. Notez ce qui se passe à chaque étape, comme indiqué. Effectuez toutes les étapes, jusqu'à celles de la section "Additional data to help debugging" incluses.

Le résultat net est que vous aurez créé, formé et déployé
dans votre instance de service {{site.data.keyword.aios_short}} le modèle **Spark German Risk Deployment**. {{site.data.keyword.aios_short}} sera configuré pour vérifier le biais du modèle par rapport au sexe (ici, Féminin) ou à l'âge (ici, 18 à 25 ans).

## Affichage des résultats
{: #crt-view-results}

### Affichez les analyses de votre déploiement
{: #crt-view-insights}

Dans le [tableau de bord {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window},
cliquez sur l'onglet **Analyses** :

  ![Analyses](images/insight-dash-tab.png)

La page Analyses fournit une vue d'ensemble des métriques de vos modèles déployés. Vous voyez des alertes pour les métriques d'équité ou d'exactitude passées sous le seuil défini lors de l'exécution du bloc-notes. Les données et paramètres utilisés dans ce tutoriel auront créé des métriques d'exactitude et d'équité similaires à celles présentées ici.

  ![Vue d'ensemble des analyses](images/insight-overview-adv-tutorial-2.png)

### Affichez les données de surveillance de votre déploiement
{: #crt-view-mon-data}

1. Pour afficher les détails de la surveillance, cliquez sur le carreau correspondant au déploiement sur la page **Analyses**. Les données de surveillance du déploiement s'affichent. 
2. Faites glisser le marqueur sur le graphique
pour sélectionner les données d'une fenêtre d'une heure spécifique. 
3. Cliquez sur le lien **Afficher les détails**.

  ![Données de surveillance](images/insight-monitor-data2.png)

Vous pouvez maintenant examiner les graphiques des données que vous avez surveillées. Pour cet exemple, vous pouvez voir que pour la fonction "Sex", le groupe `female`
a obtenu le résultat favorable "Aucun risque" moins (68 %) que le groupe `male` (78 %).

  ![Vue d'ensemble des analyses](images/insight-review-charts2.png)

### Affichez l'explicabilité d'une transaction du modèle
{: #crt-view-explain}

Pour chaque déploiement, vous pouvez voir les données d'explicabilité des différentes transactions.

Si vous savez déjà quelle transaction vous voulez afficher, vous pouvez la rechercher rapidement avec son ID. Après avoir cliqué sur le carreau du déploiement,
cliquez sur l'icône **Expliquer une transaction**
![Onglet Expliquer une transaction](images/insight-transact-tab.png) dans le navigateur,
entrez l'ID de la transaction et appuyez sur **Entrée**.
{: tip}

Si vous utilisez la version légère interne de PostgreSQL, vous ne pourrez peut-être pas récupérer vos identifiants de base de données. Cela peut vous empêcher de voir les transactions.
{: note}

1. Dans les graphiques des dernières données biaisées, cliquez sur le bouton **Afficher les transactions**.

  ![Afficher les transactions](images/view_transactions.png)

  La liste des transactions où le déploiement a agi de manière biaisée s'affiche. 
  
2. Sélectionnez une des transactions et, dans la colonne **ACTION**, cliquez sur le lien **Expliquer**.

  ![Liste des transactions](images/transaction_list_cr.png)

Vous obtenez une explication de la façon dont le modèle est parvenu à sa conclusion,
avec la confiance, les facteurs qui ont contribué au niveau de confiance et les attributs fournis.

  ![Affichage d'une transaction](images/view_transaction_cr.png)
  
## Etapes suivantes
{: #crt-next-steps}

- Apprenez-en plus sur [l'affichage et l'interprétation des données](/docs/services/ai-openscale?topic=ai-openscale-it-ov)
et sur la [surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
