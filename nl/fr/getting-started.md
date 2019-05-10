---

title: Fiabilité et transparence pour vos modèles d'apprentissage automatique avec {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: ai, getting started, tutorial, understanding, video

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
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

# Initiation - Tutoriel (de base)
{: #gettingstarted}

{{site.data.keyword.aios_full}} permet aux entreprises d'automatiser et de rendre opérationnel le cycle de vie de l'IA dans les applications métier,
afin de garantir que les modèles sont exempts de biais, qu'ils peuvent être facilement expliqués et compris par les professionnels et qu'ils sont auditables dans les transactions commerciales.
{{site.data.keyword.aios_short}} prend en charge les modèles d'IA construits et exécutés dans les outils et infrastructures de service de modèle de votre choix.
{: shortdesc}

## Présentation
{: #gs-view-demo}

Regardez cette vidéo qui donne une présentation rapide de {{site.data.keyword.aios_short}}.

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Trust and Transparency in AI" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

## Scénario d'utilisation de {{site.data.keyword.aios_short}}
{: #gs-use}

Les organismes de prêt classiques cherchent à
élargir leur portefeuille numérique de services financiers à un public plus vaste et plus diversifié,
ce qui nécessite une nouvelle approche de la modélisation du risque de crédit.
Leurs équipes de science des données s'appuient actuellement sur des techniques de modélisation standard,
comme les arbres de décision et la régression logistique,
qui fonctionnent bien pour des ensembles de données modérés, et font des recommandations qui peuvent être facilement expliquées.
Cela répond aux exigences réglementaires selon lesquelles les décisions de prêt doivent être transparentes et explicables.

Pour offrir un accès au crédit à une population plus vaste et plus risquée,
les antécédents de crédit des demandeurs doivent s'étendre au-delà du crédit traditionnel,
comme les prêts hypothécaires et les prêts automobiles,
à d'autres sources de crédit comme les antécédents de paiement des services publics (eau, électricité, etc.) et des forfaits de téléphonie mobile,
ainsi qu'à la formation et au fonctions occupées.
Ces nouvelles sources de données sont prometteuses
mais elles introduisent également un risque en augmentant la probabilité de corrélations inattendues
introduisant un biais en fonction de l'âge, du sexe ou d'autres traits personnels du demandeur.

Les techniques de science des données les plus adaptées à ces ensembles de données divers,
telles que le gradient d'arbres et les réseaux neuronaux, peuvent générer des modèles de risque très exacts, mais à un coût.
De tels modèles "boîte noire" génèrent des prévisions opaques qui doivent d'une façon ou d'une autre devenir transparentes,
pour garantir l'approbation réglementaire, par exemple quant à l'article 22 du RGPD (règlement général sur la protection des données)
ou à la loi fédérale américaine FCRA (Fair Credit Reporting Act) gérée par le Consumer Financial Protection Bureau.

Le modèle de risque de crédit fourni dans ce tutoriel utilise un ensemble de données de formation contenant 20 attributs sur chaque demandeur de prêt.
Deux de ces attributs, l'âge et le sexe, peuvent être testés quant au biais.
Ce tutoriel se concentrera sur le biais par rapport à ces deux attributs.

{{site.data.keyword.aios_short}}
surveillera la propension du modèle déployé à donner un résultat favorable ("aucun risque") pour un groupe (le groupe de référence) sur un autre (le groupe surveillé).
Dans ce tutoriel, le groupe surveillé est celui des `femmes` pour le sexe, et `19 à 25 ans` pour l'âge.

<!---
### How {{site.data.keyword.aios_short}} can help
{: #gs-how}

- *Identify run-time bias in the model*: The company has established evidence that shows the key factors that should influence which drug is predicted are BP, CHOLESTEROL, K and NA. AGE and SEX do play a role, but they're not as significant when compared to the other indicators. The company suspects that the data coming from patient trials might have suffered from biases of the practitioners for prescribing medications based on SEX and BP. The company wants to constantly monitor for such biases being learned from the data, and flag a suspected bias.

- *Constantly validate the accuracy of the model*: The company routinely evaluates the model prediction by having experts provide their own drug recommendations based on the patient data. The goal is to integrate these manual evaluations as feedback, to tell the model in real time where it might be wrong, and improve it over time.

- *Make the model more trustworthy*: To achieve a successful adoption of its AI assistant, the company received feedback from its customer base of medical practitioners and doctors who said they would not trust the AI model recommendations without understanding the logic behind them.

Each of these issues will be addressed in this tutorial, through the use of {{site.data.keyword.aios_short}}:

- The Fairness monitor will flag SEX and BP biases the model may have
- The Accuracy monitor uses feedback generated by your experts to test the performance of the deployed model, to detect model drift
--->

## Alternate setup option
{: #gs-module}

Instead of completing the following tutorial to explore {{site.data.keyword.aios_short}}, technical users can install a Python module that automates the provisioning and configuration of prerequisite services. This module requires that Python 3 is installed, which includes the pip package management system. For instructions, see, [Installing a Python module to set up {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module).

Additional tutorial links may be found in the [Additional resources](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov) topic.

## Tutorial objectives
{: #gs-obj}

In this tutorial, you will:

- Provision {{site.data.keyword.Bluemix_notm}} machine learning and storage services
- Set up a Watson Studio project, and create, train and deploy a machine learning model
- Configure and explore trust, transparency and explainability for your model

## Provision prerequisite {{site.data.keyword.Bluemix_notm}} services
{: #gs-prps}

In addition to {{site.data.keyword.aios_short}}, to complete this tutorial, you need the following accounts and services.

<!---

Pour le service {{site.data.keyword.composeForPostgreSQL}}, il faut un forfait standard **payant**.
Un crédit {{site.data.keyword.Bluemix_notm}} de 200 $ peut être obtenu en passant à un compte payant avec une carte de crédit.
Si vous avez déjà un compte payant, vous recevrez un remboursement unique de 16 $ du coût de votre premier Go de stockage, pour un mois.
{: tip}

--->

**Important** :
Pour des performances optimales, il est recommandé de créer les services nécessaires dans la même région
que {{site.data.keyword.aios_short}}.
Pour voir les sites disponibles pour {{site.data.keyword.aios_short}}, voir [Disponibilité du service](/docs/resources?topic=resources-services_region).

1.  Connectez-vous à votre compte [{{site.data.keyword.Bluemix_notm}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window}
avec votre {{site.data.keyword.ibmid}}.
1.  Pour chacun des services suivants qui n'est pas encore associé à votre compte, créez une instance en cliquant sur le lien,
en donnant un nom au service, en sélectionnant le forfait **Lite** (gratuit) et en cliquant sur le bouton **Créer** :

    - [Watson Studio
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/watson-studio){: new_window}

      ![Watson Studio](images/watson_studio.png)

    - [Watson Machine Learning
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/machine-learning){: new_window}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window}

      ![Object Storage](images/object_storage.png)

<!---

### Mettez à disposition un service Db2 Warehouse
{: #gs-provdb2}

- [Mettez à disposition un service Db2 Warehouse ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/db2-warehouse){: new_window}
si vous n'en avez pas déjà un associé à votre compte :

  ![Db2 Warehouse](images/db2_warehouse.png)

- Donner un nom à votre service, choisissez le forfait Entry et cliquez sur le bouton **Créer**.

### Téléchargez les données de formation dans Db2 Warehouse
{: #gs-traindb2}

- Téléchargez le fichier [drug_train_data_updated.csv ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/drug_train_data_updated.csv).
Enregistrez-le bien en fichier .CSV.

- Ouvrez votre Db2 Warehouse existant (ou nouveau)
depuis la [console IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window}
et cliquez sur **Gérer** dans le panneau de gauche puis sur le bouton **Ouvrir**.

- Si nécessaire, utilisez vos identifiants Db2 "nom d'utilisateur" et "mot de passe" pour vous connecter à Db2 Warehouse.

- Une fois Db2 Warehouse ouvert, cliquez sur le bouton ** Menu** et sélectionnez **Charger** dans le menu :

  ![Menu Charger](images/db2_load.png)

- Accédez au fichier de données de formation ou glissez-déposez-le dans la zone appropriée du formulaire.
Cliquez sur **Suivant**.
Sélectionnez un schéma dans la liste des cibles de chargement ; il sera généralement d'une forme comme "DASH12345".
Cliquez ensuite sur **Nouvelle table** sur la droite :

  ![Nouvelle table](images/new_table.png)

- Nommez votre table HEART\_DRUG\_TRAINING et cliquez sur le bouton **Créer** :

  ![Création de la nouvelle table](images/new_table_create1.png)

- Cliquez sur **Suivant** pour prévisualiser les données.
Sur l'écran de prévisualisation,
définissez la zone **Séparateur** avec un point-virgule (;) et assurez-vous que l'option **En-tête sur la première ligne** soit cochée :

  ![Séparateur et en-tête](images/separator.png)

- Les données de formation devraient maintenant s'afficher correctement en colonnes.
Cliquez sur **Suivant** pour continuer, puis sur **Commencer le chargement** pour charger les données.

--->

## Définissez un projet Watson Studio
{: #gs-setup}

1.  Connectez-vous à votre [compte Watson Studio
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.ibm.com/){: new_window}
et commencez par créer un nouveau projet.
Sélectionnez **Créer un projet**.

    ![Création d'un projet Watson Studio](images/studio_create_proj.png)

1.  Sélectionnez le carreau **Standard**.

    ![Sélection d'un projet Watson Studio standard](images/studio_create_standard.png)

1.  Donnez à votre projet un nom et une description,
assurez-vous que le service Object Storage créé à l'étape précédente soit sélectionné dans le menu **Stockage**
et cliquez sur **Créer**.

### Associez vos services {{site.data.keyword.Bluemix_notm}} à votre projet Watson
{: #gs-assoc}

1.  Ouvrez votre projet Watson Studio et sélectionnez l'onglet **Paramètres**.
Faites défiler vers le bas jusqu'à la section **Services associés**,
cliquez sur le menu **Ajouter un service** et sélectionnez **Watson**.

    ![Ajout du service Watson](images/add_watson_service.png)

1.  Cliquez sur le lien **Ajouter** sur le carreau **Machine Learning**
et sélectionnez l'onglet **Existant**.
Choisissez le service créé dans la section précédente dans le menu **Instance de service existante**
et cliquez sur **Sélectionner**.

<!---

- Dans l'onglet des paramètres de projet, sélectionnez à nouveau **Ajouter un service** et choisissez **Spark** dans le menu.
Dans l'onglet **Existant**, choisissez le service Spark que vous avez créé et cliquez sur **Sélectionner**.

--->

### Ajoutez le modèle `Credit Risk`
{: #gs-addmod}

1.  Dans Watson Studio, sélectionnez l'onglet **Actifs** de votre projet,
faites défiler vers le bas jusqu'à la section **Modèles Watson Machine Learning**
et cliquez sur le bouton **Nouveau modèle Watson Machine Learning**.

1.  Dans la section **Sélectionner un type de modèle**,
sélectionnez **Dans l'exemple** et le modèle `Credit Risk`, puis cliquez sur **Créer**.

    ![Nouveau formulaire de bloc-notes](images/credit-sample-model.png)

### Déployez le modèle `Credit Risk`
{: #gs-depmod}

1.  Dans votre projet Watson Studio, cliquez sur l'onglet **Actifs**,
faites défiler jusqu'à la section **Modèles Watson Machine Learning**
et cliquez sur le modèle de risque de crédit que vous venez de créer.
2.  Dans la colonne **ACTIONS**,
cliquez sur le menu **Actions** ![icône actions](images/v-three-dots.png) puis sur **Déployer**.
3. Dans l'onglet **Actifs** de votre projet Watson Studio,
faites défiler jusqu'à la section **Modèles Watson Machine Learning** et cliquez sur le modèle `credit-risk` que vous venez de créer.
1.  Cliquez sur l'onglet **Déploiements** puis sur **Ajouter un déploiement**.
1.  Entrez `credit-risk-deploy` comme nom du déploiement et sélectionnez le type de déploiement **Service web**.
1.  Cliquez sur **Enregistrer**.

## Configurez {{site.data.keyword.aios_short}}
{: #gs-confaios}

### Mettez à disposition {{site.data.keyword.aios_short}}
{: hide-dashboard}
{: #gs-provaios}

1.  [Mettez à disposition une nouvelle instance de service {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/watson-openscale){: new_window}

<!---
    ![{{site.data.keyword.aios_short}}](images/openscale.png)
--->

2.  Donnez un nom à votre service, sélectionnez le forfait Lite et cliquez sur **Créer**.

### Connectez {{site.data.keyword.aios_short}} à votre modèle d'apprentissage automatique
{: #gs-ctmod}

Maintenant que le modèle d'apprentissage automatique est déployé,
vous pouvez configurer {{site.data.keyword.aios_short}}
pour garantir la fiabilité et la transparence de vos modèles.

1.  Sélectionnez l'onglet **Gérer** de votre instance de {{site.data.keyword.aios_short}}
et cliquez sur le bouton **Lancer une application**.
La page Initiation à {{site.data.keyword.aios_full}} s'ouvre.
Cliquez sur **Commencer**.

1.  Cliquez sur le carreau **Watson Machine Learning**.

1.  Pour ce tutoriel, sélectionnez votre instance de Watson Machine Learning dans le menu et cliquez sur **Suivant**.

    Vous aussi sélectionner un autre emplacement de Machine Learning.
Pour plus d'information, voir
[Indication d'une instance de service Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-wml-connect).
    {: note}

    ![Définition de l'instance de WML](images/gs-set-wml.png)

1.  Vous pouvez maintenant sélectionner les modèles déployés qui seront surveillés par {{site.data.keyword.aios_short}}.
Sélectionnez le modèle que vous avez créé et déployé et cliquez sur **Suivant**.

    ![Sélection des modèles déployés](images/gs-set-deploy0.png)

1.  Ensuite, vous devez choisir une base de données.
Vous avez deux options : la base de données gratuite du forfait Lite, ou une base de données existante ou nouvelle.
Pour ce tutoriel, sélectionnez le carreau **Utiliser la base de données gratuite du forfait Lite**.

    Pour plus de détails sur chacune de ces options,
voir la rubrique [Indication d'une base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
La base de données existante peut être une base de données PostgreSQL ou Db2.
    {: tip}

    ![Sélection d'une base de données](images/gs-set-lite-db2.png)

1.  Vérifiez le récapitulatif et cliquez sur **Enregistrer**.
Confirmez et, quand vous y êtes invité, cliquez sur le bouton **Poursuivre la configuration**.

    Un ID de magasin de données est également indiqué ; c'est la même chose qu'un ID d'instance {{site.data.keyword.aios_short}}.
    {: tip}

    ![Vérification du récapitulatif](images/gs-setup-summary4.png)

1.  Votre écran peut ressembler à la capture d'écran suivante.
Comme vous utiliserez l'interface graphique pour évaluer vos données,
cliquez simplement sur le bouton **Configurer les moniteurs** pour terminer cette configuration.

    ![Code de demande d'évaluation](images/gs-config-send-scoring.png)

### Fournissez un ensemble d'exemples de données à votre modèle
{: #gs-samp}

Pour pouvoir configurer vos moniteurs, vous devez générer au moins une demande d'évaluation
de votre modèle afin de générer une journalisation de contenu qu'ils puissent consommer.
Dans cette section, vous allez fournir des exemples de données sous la forme d'un fichier JSON pour générer une demande d'évaluation.

1.  Téléchargez le fichier [credit_payload_data.json
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  Dans l'onglet **Déploiements** de votre projet Watson Studio,
cliquez sur le lien **credit-risk-deploy** puis sur l'onglet **Test** et sélectionnez l'icône d'entrée JSON.

    ![Test JSON](images/json_test02.png)

1.  Maintenant, ouvrez le fichier `credit_payload_data.json` que vous avez téléchargé et copiez le contenu dans la zone JSON de l'onglet **Test**.
Cliquez sur le bouton **Prévoir** pour envoyer des contenus de formation à votre modèle et les évaluer.

    ![Prévision JSON](images/json_test03.png)

### Préparation de la surveillance
{: #gs-prepmon}

1.  Maintenant, dans l'instance de {{site.data.keyword.aios_short}}, sélectionnez votre déploiement et cliquez sur **Commencer**.

    ![Sélection du déploiement](images/config-select-deploy2.png)

1.  Sélectionnez le carreau **Préparer la surveillance** et cliquez sur **Commencer**.

    ![Préparation de la surveillance](images/config-prep-monitor.png)

1.  Vous allez ensuite fournir des informations sur votre modèle et vos données de formation.
Cliquez sur **Suivant**.

    ![Préparation de l'explication](images/config-what-monitor.png)

1.  Dans le menu **Type de données**,
sélectionnez **Numérique/catégoriel** comme type de données analysé par votre déploiement et cliquez sur **Suivant**.

    ![Sélection du type d'entrée](images/config-input-monitor.png)

1.  Pour les données numériques ou catégorielles, vous devez fournir des informations sur les données de formation de votre modèle pour configurer les moniteurs.
Sélectionnez **Configurer les moniteurs manuellement** pour fournir les informations de connexion à vos données de formation.

    ![Sélection du type de configuration](images/config-manual-monitor.png)

1.  Le type d'algorithme est important pour surveiller les métriques du modèle, comme l'exactitude.
Comme la prévision que le modèle peut faire est "Risque" ou "Aucun risque", sélectionnez le
[type d'algorithme](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) **Classification binaire** ;
cliquez ensuite sur **Suivant**.

    ![Binaire](images/binary.png)

1.  L'emplacement des exemples de données est prérenseigné sur l'écran suivant.
Sélectionnez **Suivant** pour continuer.

    ![Indication de l'emplacement Db2 de la page des données de formation](images/gs-config-train-db2-monitor.png)

1.  Le schéma et la table sont également prérenseignés.
Cliquez sur **Suivant** pour continuer.

    ![Indication de l'emplacement Db2 du schéma et de la table de formation](images/gs-fair-config-table-db2.png)

1.  Maintenant, vous devez spécifier la fonction qui contient la ou les réponses que le modèle prévoira
(en d'autres termes, dans votre base de données, la colonne de la table qui contient les valeurs de prévision (libellés)).
Ici, comme le modèle prévoira le risque de crédit, sélectionnez la colonne **Risk** et cliquez sur **Suivant**.

    Votre base de données de formation contient les valeurs que vous avez fournies pour former votre modèle.
    {: note}

    ![Entrée de libellé de prévision](images/gs-config-label.png)

1.  Sélectionnez les colonnes utilisées pour la formation du modèle.
Il s'agit des données attendues par votre déploiement de modèle dans une demande.
Toutes les colonnes de données sauf `_training` sont des entrées du modèle.
Sélectionnez toutes les autres entrées et cliquez sur **Suivant**.

    ![Entrées d'explicabilité](images/explain_inputs1.png)

1.  Pour les données catégorielles, vous devez identifier les colonnes qui contiennent maintenant des entiers mais contenaient initialement des valeurs texte.
Sélectionnez les valeurs indiquées ici.

    ![Entrées d'explicabilité](images/config_categories.png)

1.  Vérifiez le récapitulatif de vos sélections et cliquez sur **Enregistrer** puis sur **OK**.

### Configurez la surveillance de l'équité
{: #gs-cfgfair}

1.  Cliquez sur **Equité**.

1.  Lisez l'explication de l'équité et cliquez sur **Suivant**.
Pour plus d'information, voir [Equité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

1.  Vous pouvez maintenant choisir les fonctions à surveiller pour l'équité.
Pour chaque fonction que vous sélectionnez,
{{site.data.keyword.aios_short}} surveillera la propension du modèle déployé à donner un résultat favorable pour un groupe sur l'autre.
Dans cet exemple, nous surveillerons les fonctions **Sex** et **Age**.

    Les fonctions sont surveillées individuellement, mais n'importe quel débiaisement corrigera simultanément les problèmes de toutes.
Cliquez sur les carreaux **Sex** et **Age**, puis sur **Suivant**.

1.  {{site.data.keyword.aios_short}} détecte le biais sur un groupe surveillé par rapport à un groupe de référence.
Pour la fonction **Sex**, ajoutez la valeur `male` (masculin) au **Groupe de référence**
et la valeur `female` (féminin) au **Groupe surveillé**, puis cliquez sur **Suivant**.

    Le modèle sera marqué comme biaisé pour le **Sex** si les taux de prévision Risque pour le groupe surveillé diffèrent de ceux pour le groupe de référence.
Ainsi, s'il prévoit un risque pour les clients hommes 60 % du temps, et pour les clients femmes 20 % du temps, il est biaisé.

    ![Groupes de sexe](images/gender_groups1.png)

1.  Vous pouvez maintenant affecter un seuil d'équité pour le **Sex**.
Vous verrez une alerte sur le tableau de bord des opérations si l'équité passe sous ce seuil.
Définissez le seuil à 90 % puis cliquez sur **Suivant**.

1.  Pour la fonction **Age**, ajoutez les valeurs `26-74` au **Groupe de référence**
et les valeurs `19-25` au **Groupe surveillé**, puis cliquez sur **Suivant**.

    Comme avec le **Sex**, le modèle sera marqué comme biaisé pour l'**Age**
si les taux de prévision Risque pour le groupe surveillé diffèrent de ceux pour le groupe de référence.
Ainsi, si les clients de 26 à 74 ans ont une prévision Risque à un taux différent de ceux de 19 à 25 ans, le modèle est biaisé.

    ![Groupes BP](images/age_groups.png)

1.  Définissez le seuil pour l'**Age** à 90 % et cliquez sur **Suivant**.

1.  Faites glisser les valeurs de la zone **Valeurs des données de formation**
aux zones **Valeurs favorables** et **Valeurs défavorables**.
Pour ce tutoriel, la valeur favorable est **Aucun risque** et la valeur défavorable, **Risque**.
Cliquez sur **Suivant**.

    {{site.data.keyword.aios_short}} détecte automatiquement la colonne de la base de données de journalisation de contenu qui contient les valeurs de prévision
et elle présente celles-ci dans la zone **Valeurs des données de formation**.
Votre base de données de formation contient les valeurs que vous avez fournies pour la formation de votre modèle,
tandis que la base de données de journalisation de contenu contient les données de commentaires collectées lors de l'exécution du modèle,
que vous pouvez éventuellement utiliser pour reformer et redéployer le modèle.
    {: note}

    ![Valeurs positive et négative](images/pos_and_neg2.png)

1.  Réglez la taille d'échantillon minimale à 100 à l'aide du curseur puis cliquez sur **Suivant**.

    ![Taille minimale](images/gs-fair-config-sample.png)

    Pour ce tutoriel, la taille minimale d'échantillon est définie à 100.
Normalement, une taille plus grande est recommandée pour ne pas fausser les résultats.
    {: note}

1.  Vérifiez vos choix et cliquez sur **Enregistrer** puis sur **OK**.

    ![Récapitulatif de la configuration](images/fair-summary.png)

    La fenêtre suivante apparaît ; elle indique un noeud final d'évaluation biaisé.
Comme ce tutoriel utilise l'interface graphique et non l'interface ligne de commande pour l'évaluation des données, cliquez sur **OK** pour continuer.

    ![API de débiaisement](images/gs-insight-debias-api.png)

### Configurez la surveillance de l'exactitude
{: #gs-cfgac}

1.  Cliquez sur **Exactitude**.

1.  Lisez l'explication de l'exactitude et cliquez sur **Suivant**.
Pour plus d'information, voir [Exactitude](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

1.  Définissez le seuil d'alerte d'exactitude à 90 % et cliquez sur **Suivant**.

1.  Sur l'écran suivant, réglez la taille d'échantillon minimale à 10 à l'aide du curseur puis cliquez sur **Suivant**.

    Pour ce tutoriel, la taille minimale d'échantillon a été définie à 10.
Normalement, une taille plus grande est recommandée pour ne pas fausser les résultats.
    {: note}

1.  Pour la taille d'échantillon maximale, utilisez 10000.
Cliquez sur **Suivant**.

1.  Vérifiez vos choix et cliquez sur **Enregistrer** puis sur **OK**.

1.  Pour finir, une option vous est proposée d'ajouter des données de commentaires ; ce sujet est abordé à la section suivante.
Pour l'instant, fermez la fenêtre en cliquant sur **OK**, sans cliquer sur le bouton **Ajouter des données de commentaires**.

    Pour plus de détails, voir [Configuration du moniteur d'exactitude](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config).

## Fournissez un ensemble d'exemples de données de commentaires à votre modèle
{: #gs-smpfeed}

Pour permettre la surveillance de l'exactitude, vous devez fournir à votre modèle des données de commentaires.
Les données d'exactitude n'apparaîtront pas dans le tableau de bord tant que ce ne sera pas fait.
Vous pouvez générer les demandes en même temps en ajoutant des exemples de données de commentaires au modèle pour l'évaluation.
Pour cette tâche, vous allez télécharger un fichier CSV contenant des exemples de données de commentaires.

1.  Téléchargez le fichier
[credit_feedback_data.csv
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv).

1.  Dans {{site.data.keyword.aios_short}}, cliquez sur l'onglet **Analyses**.

    ![Analyses](images/insight-dash-tab.png)

1.  Cliquez sur le carreau de votre modèle déployé.

    ![Onglet Analyses - aucune donnée](images/gs-insight-overview.png)

1.  Cliquez ensuite sur l'icône d'édition pour modifier la configuration de déploiement.

    ![Icône d'édition - côté droit](images/gs-insight-edit-icon.png)

1.  Dans le panneau latéral Récapitulatif, cliquez sur le bouton **Ajouter des données de commentaires**
et sélectionnez le fichier `credit_feedback_data.csv` que vous avez téléchargé.
Sélectionnez le délimiteur **Virgule (,)** et cliquez sur **OK**.

    La taille de fichier est actuellement limitée à 8 Mo.
    {: note}

    ![Délimiteur d'exactitude](images/accuracy-delimit.png)

    L'ajout du fichier CSV fournit des données de commentaires au modèle.

    ![Panneau Récapitulatif](images/gs-insight-summary-panel-2.png)

## Affichage des résultats
{: #gs-viewres}

Une fois que vous avez configuré la surveillance de l'exactitude, le contrôle d'exactitude s'exécute au bout d'une heure.
Dans un système de production, cela permet au tableau de bord d'accumuler des données de commentaires.
Pour ce tutoriel, vous voudrez probablement déclencher le contrôle d'exactitude manuellement après avoir ajouté vos données de commentaires,
pour pouvoir voir les résultats dans le tableau de bord **Analyses**.

Pour voir le résultat immédiatement,
sélectionnez un déploiement sur la page **Analyses**
et cliquez sur le bouton **Vérifier l'équité maintenant** ou **Vérifier l'exactitude maintenant**.

### Affichez les analyses de votre déploiement
{: #gs-viewin}

1. Dans le tableau de bord [{{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window},
cliquez sur l'onglet **Analyses**.

  ![Analyses](images/insight-dash-tab.png)

1. Affichez la page Analyses pour voir une vue d'ensemble des métriques de vos modèles déployés.
Vous voyez des alertes pour les métriques d'équité ou d'exactitude passées sous le seuil de 90 %.

  Les métriques d'équité et d'exactitude peuvent mettre jusqu'à une heure pour apparaître.
  {: tip}

  ![Vue d'ensemble des analyses](images/insight-overview.png)

### Affichez les données de surveillance de votre déploiement
{: #gs-viewmon}

1.  Sélectionnez un déploiement en cliquant sur le carreau correspondant sur la page Analyses.
Les données de surveillance du déploiement s'affichent.
Remarque : Après le téléchargement du fichier .csv de commentaires,
il se peut que les données d'équité ou d'exactitude ne soient pas mises à jour.
Pour voir le résultat immédiatement, cliquez sur le bouton **Vérifier l'équité maintenant** ou **Vérifier l'exactitude maintenant**.
1.  Faites glisser le marqueur sur le graphique
pour sélectionner les données correspondant à la période sur laquelle vous avez exécuté les exemples de données et les exemples de données de commentaires.
Cliquez ensuite sur **Afficher les détails**.

    ![Surveiller les données](images/insight-monitor-data.png)

1.  Ensuite, examinez les graphiques correspondant aux données que vous avez surveillées.
Pour cet exemple,
sélectionnez `Age` ou `Sex` dans le menu **Fonction**
pour voir les détails sur les données surveillées.

    Pour savoir comment lire ces graphiques,
voir [Visualisation des données d'une heure spécifique](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
    {: tip}

    ![Vue d'ensemble des analyses](images/insight-review-charts.png)

### Affichez l'explicabilité d'une transaction du modèle
{: #gs-viewextx}

1.  Cliquez sur le bouton **Afficher les transactions** dans les graphiques des données que vous avez surveillées.

    ![Afficher les transactions](images/view_transactions.png)

1.  S'affiche la liste des transactions qui ont contribué au biais sur la dernière heure.
Pour obtenir une explication plus détaillée d'une transaction particulière,
cliquez sur **Expliquer** dans la colonne **ACTION**.

    ![Liste des transactions](images/transaction_list_cr.png)

1.  L'explication de la manière dont le modèle est parvenu à sa conclusion apparaît.
Elle inclut la confiance du modèle, les facteurs qui ont contribué au niveau de confiance et les colonnes fournies.

    ![Affichage d'une transaction](images/view_transaction1.png)

## Etapes suivantes
{: #gs-next}

- Apprenez-en plus sur [l'affichage et l'interprétation des données](/docs/services/ai-openscale?topic=ai-openscale-it-ov)
et sur la [surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
