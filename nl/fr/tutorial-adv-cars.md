---

title: Fiabilité et transparence pour vos modèles d'apprentissage automatique avec {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

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

# Tutoriel (avancé)
{: #tadv-tutorial-advanced}

## Scénario
{: #tadv-scenario}

Une société de location de voitures a recueilli des données de retour sur la satisfaction de la clientèle. Le modèle présenté utilise ces données pour prévoir un plan d'action à suivre avec chaque client, par exemple lui donner un bon pour sa prochaine location.

Le modèle utilise les zones de données client ID (numéro d'identification), GENDER (sexe), STATUS (état civil : célibataire ou marié), CHILDREN (nombre d'enfants),
AGE, CUSTOMER STATUS (état du client : actif ou inactif), CAR OWNER (propriétaire d'une voiture : oui ou non), CUSTOMER SERVICE (service client : commentaire),
SATISFACTION (satisfait ou non satisfait) et BUSINESS AREA (domaine professionnel : produits ou services)
pour prévoir une valeur parmi quatre (NA, bon, surclassement gratuit, prise de véhicule sur demande) pour la zone de données ACTION.

## Conditions requises
{: #tadv-prereqs}

Pour effectuer ce tutoriel, il vous faudra :

- Un [compte Watson Studio
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.ibm.com/){: new_window}.
- Un [compte {{site.data.keyword.cloud_notm}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window}.

Au cours du tutoriel, vous mettrez à disposition les services {{site.data.keyword.cloud_notm}} Lite (gratuits) suivants :

- Machine Learning
- Apache Spark
- Object Storage

Vous mettrez également à disposition le service {{site.data.keyword.cloud_notm}} **payant** suivant :

- PostgreSQL

  Un crédit {{site.data.keyword.cloud_notm}} de 200 $ peut être obtenu en passant à un compte payant avec une carte de crédit. Si vous avez déjà un compte payant, vous recevrez un remboursement unique de 16 $ du coût de votre premier Go de stockage, pour un mois.
  {: tip}

La base de données PostgreSQL et l'instance de Watson Machine Learning doivent être déployées dans le même compte {{site.data.keyword.cloud_notm}}.
{: important}

Si vous avez déjà mis à disposition les services nécessaires, par exemple si vous avez effectué l'autre tutoriel,
passez à [Définissez un projet Watson Studio](#tadv-setup-ws) plus bas.

## Introduction
{: #tadv-intro}

Dans ce tutoriel, vous allez :

- Mettre à disposition des services d'apprentissage automatique et de stockage {{site.data.keyword.cloud_notm}}
- Définir un projet Watson Studio et exécuter un bloc-notes Python pour créer, former et déployer un modèle d'apprentissage automatique
- Exécuter un bloc-notes Python pour créer un magasin de données, configurer les moniteurs de performances, d'exactitude et d'équité, et créer des données à surveiller
- Afficher les résultats dans l'onglet Analyses de {{site.data.keyword.aios_short}}

## Mettez à disposition les services {{site.data.keyword.cloud_notm}}
{: #tadv-svcs}

Connectez-vous à votre [compte {{site.data.keyword.cloud_notm}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window} avec votre IBMid. Lors de la mise à disposition des services, en particulier dans le cas d'Apache Spark, d'Object Storage et de Db2 Warehouse,
vérifiez que l'organisation et l'espace sélectionnés sont les mêmes pour tous les services.

### Créez un compte Watson Studio
{: #tadv-stac}

- Si vous n'en avez pas déjà une associée à votre compte, [créez une instance de Watson Studio
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/watson-studio){: new_window} :

  ![Watson Studio](images/watson_studio.png)

- Donnez un nom à votre service, choisissez le forfait Lite (gratuit) et cliquez sur le bouton **Créer**.

### Mettez à disposition un service Machine Learning
{: #tadv-pml}

- Si vous n'en avez pas déjà une associée à votre compte, [mettez à disposition une instance de Watson Machine Learning
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/machine-learning){: new_window} :

  ![Machine Learning](images/machine_learning.png)

- Donnez un nom à votre service, choisissez le forfait Lite (gratuit) et cliquez sur le bouton **Créer**.

- Notez les identifiants du service Machine Learning. Dans votre instance d'apprentissage automatique, cliquez sur le lien **Données d'identification du service** sur le côté gauche de la page. Nommez l'identifiant et cliquez sur **Ajouter**. Ensuite, dans la liste des identifiants, cliquez sur **Afficher l'identifiant** et copiez les identifiants pour utilisation ultérieure.

### Mettez à disposition un service Spark
{: #tadv-ps}

- Si vous n'en avez pas déjà un associé à votre compte, [mettez à disposition un service Spark
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/apache-spark){: new_window} :

  ![Apache Spark](images/spark.png)

- Affectez un nom à votre service, choisissez le forfait Lite (gratuit) et cliquez sur le bouton **Créer**.

- Notez les identifiants de service de votre instance de Spark. Ouvrez celle-ci et cliquez sur **Données d'identification du service** dans le menu de gauche. Cliquez sur le bouton **Nouvel identifiant**, nommez vos identifiants et cliquez sur **Ajouter**. Ensuite, cliquez sur le lien **Afficher les identifiants** en regard du jeu que vous venez de créer et copiez ces identifiants pour utilisation ultérieure.

### Mettez à disposition un service Object Storage
{: #tadv-pos}

- Si vous n'en avez pas déjà un associé à votre compte, [mettez à disposition un service Object Storage
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} :

  ![Object Storage](images/object_storage.png)

- Donnez un nom à votre service, choisissez le forfait Lite (gratuit) et cliquez sur le bouton **Créer**.

### Mettez à disposition un service PostgreSQL payant
{: #tadv-ppgs}

- Si vous n'en avez pas déjà un associé à votre compte, [mettez à disposition un service PostgreSQL payant
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window}.

  ![Compose for PostgreSQL](images/postgres.png)

- Donnez un nom à votre service, choisissez le forfait Standard et cliquez sur le bouton **Créer**.

  Un crédit {{site.data.keyword.cloud_notm}} de 200 $ peut être obtenu en passant à un compte payant avec une carte de crédit. Si vous avez déjà un compte payant, vous recevrez un remboursement unique de 16 $ du coût de votre premier Go de stockage, pour un mois.
  {: tip}

- Notez les identifiants de service de votre instance de PostgreSQL. Ouvrez votre instance de PostgreSQL existante (ou nouvelle) et cliquez sur **Données d'identification du service** dans le menu de gauche. Cliquez sur le bouton **Nouvel identifiant**, nommez vos identifiants et cliquez sur **Ajouter**. Ensuite, cliquez sur le lien **Afficher les identifiants** en regard du jeu que vous venez de créer et copiez ces identifiants pour utilisation ultérieure.

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![Définissez le type de données manuellement](images/data-type-manual.png)

- Les données de formation devraient maintenant s'afficher correctement en colonnes. Cliquez sur **Suivant** pour continuer, puis sur **Commencer le chargement** pour charger les données.

--->

## Définissez un projet Watson Studio
{: #tadv-setup-ws}

- Connectez-vous à votre [compte Watson Studio
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.ibm.com/){: new_window}. Cliquez sur l'icône d'avatar de compte en haut à droite et vérifiez que le compte que vous utilisez
est bien celui que vous avez utilisé pour créer vos services {{site.data.keyword.cloud_notm}} :

  ![Même compte](images/same_account.png)

- Dans Watson Studio, commencez par créer un nouveau projet. Sélectionnez "Créer un projet" :

  ![Création d'un projet Watson Studio](images/studio_create_proj.png)

- Sélectionnez le carreau **Standard** pour créer le projet :

  ![Sélection d'un projet Watson Studio standard](images/studio_create_standard.png)

- Donnez à votre projet un nom et une description,
assurez-vous que le service Object Storage créé à l'étape précédente soit sélectionné dans la liste déroulante **Stockage**
et cliquez sur **Créer**.

### Associez vos services {{site.data.keyword.cloud_notm}} à votre projet Watson
{: #tadv-acsw}

- Ouvrez votre projet Watson Studio et sélectionnez l'onglet **Paramètres**. Dans la section **Services associés**, cliquez sur la liste déroulante **Ajouter un service**
et sélectionnez **Watson**:

  ![Ajout du service Watson](images/add_watson_service.png)

- Cliquez sur le lien **Ajouter** sur le carreau **Machine Learning**
et sélectionnez l'onglet **Existant**. Choisissez le service créé dans la section précédente dans la liste déroulante **Instance de service existante**
et cliquez sur **Sélectionner**.

- Dans l'onglet des paramètres de projet, sélectionnez à nouveau **Ajouter un service** et choisissez **Spark** dans la liste déroulante. Dans l'onglet **Existant**, choisissez le service Spark que vous avez créé et cliquez sur **Sélectionner**.

## Créez et déployez un modèle d'apprentissage automatique
{: #tadv-deploy-ml}

### Ajoutez le bloc-notes `CARS4U Action Recommendation - model` à votre projet Watson Studio

- Téléchargez le fichier suivant :

    - [CARS4U Action Recommendation - model
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- Dans l'onglet **Actifs** de votre projet Watson Studio,
cliquez sur le bouton **Ajouter au projet** et sélectionnez **Bloc-notes** dans la liste déroulante :

  ![Ajout d'une connexion](images/add_notebook.png)

- Sélectionnez **A partir d'un fichier** :

  ![Formulaire de nouveau bloc-notes](images/new_notebook_name.png)

- Cliquez ensuite sur le bouton **Choisir un fichier** et sélectionnez le fichier "CARS4U Action Recommendation - model" que vous avez téléchargé :

  ![Formulaire de nouveau bloc-notes](images/new_notebook_name2.png)

- Dans la section **Sélectionner l'environnement d'exécution**, choisissez l'instance de Spark que vous avez créée précédemment dans la liste déroulante :

  ![Environnement d'exécution Spark](images/spark_runtime.png)

- Cliquez sur **Créer un bloc-notes**.

### Editez et exécutez le bloc-notes `CARS4U Action Recommendation - model`
{: #tadv-ern}

Le bloc-notes `CARS4U Action Recommendation - model` contient des instructions détaillées pour chaque étape du code Python que vous allez exécutez. Au fur et à mesure que vous avancerez, prenez le temps de comprendre ce que fait chaque commande.
{: tip}

- Dans l'onglet **Actifs** de votre projet Watson Studio,
cliquez sur l'icône **Editer** en regard du bloc-notes `CARS4U Action Recommendation - model` afin d'éditer celui-ci.

- Dans la section 2.2, "Upload data to PostgreSQL database", remplacez les identifiants du service Postgres par ceux que vous avez créés à la section précédente.

- Dans la section 4, "Store the model in the repository", sous **TIP**,
remplacez les identifiants Watson Machine Learning par ceux que vous avez créés à la section précédente.

- Une fois que vous avez entré vos identifiants, le bloc-notes est prêt à s'exécuter. Cliquez sur l'élément de menu **Noyau** et sélectionnez **Redémarrer et exécuter tout** dans le menu :

  ![Redémarrer et exécuter](images/restart_and_run.png)

  Cela créera, formera et déploiera le modèle **CARS4U - Action Recommendation Model** dans votre projet. Vous pouvez vérifier que le modèle est bien déployé en sélectionnant l'onglet **Déploiements** de votre projet Watson Studio
et en cliquant sur le lien **CARS4U - Area and Action Model Deployment**.

## Configurez {{site.data.keyword.aios_short}}
{: #tadv-config-aios}

### Mettez à disposition {{site.data.keyword.aios_short}}
{: #tadv-paios}

- Si vous n'avez pas encore mis à disposition une instance de {{site.data.keyword.aios_short}},
cliquez sur le lien **Catalogue** dans votre compte {{site.data.keyword.cloud_notm}} et filtrez sur "OpenScale". Sélectionnez le carreau de {{site.data.keyword.aios_short}}.

<!---
  ![{{site.data.keyword.aios_short}}](images/openscale.png)
--->

- Donnez un nom à votre service, sélectionnez le forfait Lite et cliquez sur **Créer**.

### Connectez {{site.data.keyword.aios_short}} à votre modèle d'apprentissage automatique
{: #tadv-cmlm}

Comme le modèle d'apprentissage automatique est déployé,
vous pouvez configurer {{site.data.keyword.aios_short}} pour garantir la fiabilité et la transparence de vos modèles. Sélectionnez l'onglet **Gérer** de votre instance de {{site.data.keyword.aios_short}}
et cliquez sur le bouton **Lancer une application**. La page Initiation à {{site.data.keyword.aios_full}} s'ouvre ; cliquez sur **Commencer**.

- Sélectionnez le carreau "Watson Machine Learning" et cliquez sur **Suivant**.

  ![Définition de l'instance de WML](images/gs-wml-default.png)

- Sélectionnez votre instance de Watson Machine Learning dans la liste déroulante et cliquez sur **Suivant**.

  ![Définition de l'instance de WML](images/gs-set-wml.png)

- Vous pouvez maintenant sélectionner les modèles déployés qui seront surveillés par {{site.data.keyword.aios_short}}. Cochez le modèle que vous avez créé et déployé et cliquez sur **Suivant** pour valider :

  ![Sélection des modèles déployés](images/gs-set-deploy.png)

- Ensuite, vous devez choisir une base de données PostgreSQL. Vous avez deux options : la base de données gratuite du forfait Lite, ou une base de données existante ou nouvelle. Pour ce tutoriel, sélectionnez le carreau **Utiliser une base de données existante ou en acheter une nouvelle**.

    ![Sélection d'une base de données](images/gs-set-lite-db1.png)

  Pour plus de détails sur chacune de ces options,
voir la rubrique [Indication d'une base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
  {: note}

- Lorsque vous sélectionnez l'option "Utiliser une base de données existante ou en acheter une nouvelle",
{{site.data.keyword.aios_short}} recherche dans votre compte {{site.data.keyword.cloud_notm}}
votre base de données Compose for PostgreSQL existante.

  Sélectionnez le schéma "magasin de données" dans le menu déroulant **Schéma**.

  ![Sélection d'une base de données](images/gs-set-schema1.png)

- Après avoir sélectionné la base de données et le schéma, cliquez sur **Suivant**
pour vérifier le récapitulatif, puis sur **Enregistrer**.

  ![Sélection d'une base de données](images/gs-setup-summary3.png)

  Lorsque vous y êtes invité, cliquez sur **Revenir au tableau de bord**.

## Créez un magasin de données et configurez les moniteurs de performances, d'exactitude et d'équité
{: #tadv-config-monitors}

### Ajoutez le bloc-notes `{{site.data.keyword.aios_short}} and Watson ML engine` à votre projet Watson Studio
{: #tadv-aomn}

Le bloc-notes `{{site.data.keyword.aios_short}} and Watson ML engine`
contient des instructions détaillées pour chaque étape du code Python que vous allez exécutez. Au fur et à mesure que vous avancerez, prenez le temps de comprendre ce que fait chaque commande.
{: tip}

- Téléchargez le fichier suivant :

    - [{{site.data.keyword.aios_short}} and Watson ML engine
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Dans l'onglet **Actifs** de votre projet Watson Studio,
cliquez sur le bouton **Ajouter au projet** et sélectionnez **Bloc-notes** dans la liste déroulante :

  ![Ajout d'une connexion](images/add_notebook.png)

- Sélectionnez **A partir d'un fichier** :

  ![Formulaire de nouveau bloc-notes](images/new_notebook_name.png)

- Cliquez ensuite sur le bouton **Choisir un fichier** et sélectionnez le fichier "{{site.data.keyword.aios_short}} and Watson ML engine"
que vous avez téléchargé :

  ![Formulaire de nouveau bloc-notes](images/new_notebook_name3.png)

- Dans la section **Sélectionner l'environnement d'exécution**, choisissez l'instance de Spark que vous avez créée précédemment dans la liste déroulante :

  ![Environnement d'exécution Spark](images/spark_runtime.png)

- Cliquez sur **Créer un bloc-notes**.

### Editez et exécutez le bloc-notes `{{site.data.keyword.aios_short}} and Watson ML engine`
{: #tadv-eromn}

- Dans l'onglet **Actifs** de votre projet Watson Studio,
cliquez sur l'icône **Editer** en regard du bloc-notes `{{site.data.keyword.aios_short}} and Watson ML engine` afin d'éditer celui-ci.

- Dans la section 1.1, "Installation and authentication":

    - Sous **ACTION: Get instance_id (GUID) and apikey**, suivez les instructions pour obtenir vos identifiants. Remplacez les `aios_credentials` par les vôtres.

    - Ensuite, dans **ACTION: Add your Watson Machine Learning credentials here**,
remplacez les identifiants Watson Machine Learning par ceux que vous avez créés précédemment.

    - Enfin, sous **ACTION: Add your PostgreSQL credentials here**,
remplacez les identifiants Postgres par ceux que vous avez créés précédemment.

- Une fois que vous avez entré vos identifiants, le bloc-notes est prêt à s'exécuter. Cliquez sur l'élément de menu **Noyau** et sélectionnez **Redémarrer et exécuter tout** dans le menu :

  ![Redémarrer et exécuter](images/restart_and_run.png)

  Cela configurera votre magasin de données, permettra la journalisation du contenu,
configurera et évaluera les moniteurs de performances, d'exactitude et d'équité,
et fournira ces métriques à votre instance de {{site.data.keyword.aios_short}}.

## Affichage des résultats
{: #tadv-results}

### Affichez les analyses de votre déploiement
{: #tadv-vide}

Dans le [tableau de bord {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window},
cliquez sur l'onglet **Analyses** :

  ![Analyses](images/insight-dash-tab.png)

La page Analyses fournit une vue d'ensemble des métriques de vos modèles déployés. Vous voyez des alertes pour les métriques d'équité ou d'exactitude passées sous le seuil défini lors de l'exécution du bloc-notes (70 %). Les données et paramètres utilisés dans ce tutoriel auront créé des métriques d'exactitude et d'équité similaires à celles présentées ici.

  ![Vue d'ensemble des analyses](images/insight-overview-adv-tutorial.png)

### Affichez les données de surveillance de votre déploiement
{: #tadv-vmdd}

Sélectionnez un déploiement en cliquant sur le carreau correspondant sur la page Analyses. Les données de surveillance du déploiement s'affichent. Faites glisser le marqueur sur le graphique
pour sélectionner les données correspondant à la période sur laquelle vous avez exécuté le bloc-notes. Sélectionnez ensuite le lien **Afficher les détails**.

  ![Données de surveillance](images/insight-monitor-data1.png)

Vous pouvez maintenant examiner les graphiques des données que vous avez surveillées. Pour cet exemple,
vous pouvez sélectionner "Children" ou "Gender" dans la liste déroulante **Fonction**
pour voir les détails sur les données surveillées.

  ![Vue d'ensemble des analyses](images/insight-review-charts1.png)

<!---

### Affichez l'explicabilité d'une transaction du modèle
{: #tadv-vemt}

Cliquez sur le bouton **Afficher les transactions** dans les graphiques des données que vous avez surveillées.

  ![Afficher les transactions](images/view_transactions.png)

  La liste des transactions de la dernière heure écoulée s'affiche. Copiez un des ID de transaction.

  ![Liste des transactions](images/transaction_list.png)

Dans le [tableau de bord de {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window},
cliquez sur l'onglet **Explicabilité** :

  ![Explicabilité](images/explainability.png)

Collez l'ID de transaction que vous avez copié dans la zone de recherche et appuyez sur **Retour** sur votre clavier. Vous obtenez une explication de la façon dont le modèle est parvenu à sa conclusion,
avec la confiance, les facteurs qui ont contribué au niveau de confiance et les attributs fournis.

  ![Afficher la transaction](images/view_transaction1.png)

--->

## Etapes suivantes
{: #tadv-next}

- Apprenez-en plus sur [l'affichage et l'interprétation des données](/docs/services/ai-openscale?topic=ai-openscale-it-ov)
et sur la [surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
