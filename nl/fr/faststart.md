---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, getting started, tutorial, understanding, fast start

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

# Tutoriel de configuration interactif
{: #gs-obj}

Dans ce tutoriel, vous effectuez les opérations suivantes :

- [Mettre à disposition des services d'apprentissage automatique et de stockage {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps).
- [Définir un projet Watson Studio et créer, former et déployer un modèle d'apprentissage automatique](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup).
- [Configurer et explorer la confiance, la transparence et l'explicabilité de votre modèle](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios).

## Mettez à disposition les services {{site.data.keyword.Bluemix_notm}} requis
{: #gs-prps}

En plus de {{site.data.keyword.aios_short}}, il vous faut pour effectuer ce tutoriel les comptes et services suivants.

**Important** :
pour des performances optimales, il est recommandé de créer les services nécessaires dans la même région
que {{site.data.keyword.aios_short}}. Pour connaître les sites disponibles pour {{site.data.keyword.aios_short}},
voir [Disponibilité du service](/docs/resources?topic=resources-services_region).

1.  Connectez-vous à votre [compte {{site.data.keyword.Bluemix_notm}}](https://{DomainName}){: external} avec votre {{site.data.keyword.ibmid}}.
1.  Pour chacun des services suivants qui n'est pas encore associé à votre compte, créez une instance en cliquant sur le lien,
en donnant un nom au service, en sélectionnant le forfait **Lite** (gratuit) et en cliquant sur le bouton **Créer** :

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Définissez un projet Watson Studio
{: #gs-setup}

1.  Connectez-vous à votre [compte Watson Studio](https://dataplatform.ibm.com/){: external} et commencez par créer un nouveau projet. Sélectionnez **Nouveau projet**.

    ![Création d'un projet Watson Studio](images/studio_create_proj.png)

1.  Sélectionnez le carreau **Standard**.

    ![Sélection d'un projet Watson Studio standard](images/studio_create_standard.png)

1.  Donnez à votre projet un nom et une description,
assurez-vous que le service Object Storage créé à l'étape précédente soit sélectionné dans le menu **Stockage**
et cliquez sur **Créer**.

### Associez vos services {{site.data.keyword.Bluemix_notm}} à votre projet Watson
{: #gs-assoc}

1.  Ouvrez votre projet Watson Studio et sélectionnez l'onglet **Paramètres**. Dans la section **Services associés**, cliquez sur **Ajouter un service** puis sur **Watson**.

    ![Ajout du service Watson](images/add_watson_service.png)

1.  Cliquez sur le lien **Ajouter** dans le carreau **Machine Learning**.
2.  Dans l'onglet **Existant**, cliquez dans la liste déroulante **Instance de service existante** sur le service créé précédemment.
3. Cliquez sur **Sélectionner**.

### Ajoutez le modèle `Credit Risk`
{: #gs-addmod}

1.  Dans {{site.data.keyword.DSX}}, sélectionnez l'onglet **Actifs** de votre projet,
faites défiler jusqu'à la section **Modèles Watson Machine Learning**
et cliquez sur le bouton **Nouveau modèle Watson Machine Learning**.

1.  Dans la section **Sélectionner un type de modèle**,
sélectionnez **Dans l'exemple** et le modèle `Credit Risk`, puis cliquez sur **Créer**.

    ![Formulaire de nouveau bloc-notes](images/credit-sample-model.png)

### Déployez le modèle `Credit Risk`
{: #gs-depmod}

1.  Sur la page du modèle `Credit Risk`, cliquez sur l'onglet **Déploiements** puis sur **Ajouter un déploiement**.
1.  Entrez `credit-risk-deploy` comme nom du déploiement et sélectionnez le type de déploiement **Service web**.
1.  Cliquez sur **Enregistrer**.

## Configurez {{site.data.keyword.aios_short}}
{: #gs-confaios}

### Mettez à disposition {{site.data.keyword.aios_short}}
{: hide-dashboard}
{: #gs-provaios}

1.  [Mettez à disposition une nouvelle instance de service {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/openscale.png)

2.  Donnez un nom à votre service, sélectionnez le **forfait Lite** et cliquez sur **Créer**.

### Connectez {{site.data.keyword.aios_short}} à votre modèle d'apprentissage automatique
{: #gs-ctmod}

Maintenant que le modèle d'apprentissage automatique est déployé,
vous pouvez configurer {{site.data.keyword.aios_short}}
pour garantir la fiabilité et la transparence de vos modèles.

1.  Sélectionnez l'onglet **Gérer** de votre instance de {{site.data.keyword.aios_short}}
et cliquez sur le bouton **Lancer une application**. La page de démonstration **Bienvenue dans {{site.data.keyword.aios_short}}** s'ouvre.
2. Pour ce tutoriel, cliquez sur **Non merci**, puis sur **Commencer**.

1.  Cliquez sur le carreau **Watson Machine Learning**.

1.  Pour ce tutoriel, sélectionnez votre instance d'{{site.data.keyword.pm_full}} dans le menu et cliquez sur **Suivant**.

    Vous pouvez aussi sélectionner un autre emplacement de {{site.data.keyword.pm_short}}. Pour plus d'information, voir
[Indication d'une instance de service {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-wml-connect).
    {: note}

    ![Définition de l'instance de {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

1.  Vous pouvez maintenant sélectionner les modèles déployés qui seront surveillés par {{site.data.keyword.aios_short}}. Sélectionnez le modèle que vous avez créé et déployé et cliquez sur **Suivant**.

    ![Sélection des modèles déployés](images/gs-set-deploy0.png)

1.  Ensuite, vous devez choisir une base de données. Vous avez deux options : la base de données gratuite ou une base de données existante ou nouvelle. Pour ce tutoriel, sélectionnez le carreau **Utiliser la base de données gratuite hébergée par {{site.data.keyword.aios_short}}**.

    La base de données gratuite comporte des limitations importantes. Il s'agit d'une base de données hébergée à laquelle vous n'avez pas accès séparément. Elle vous donne l'accès {{site.data.keyword.aios_short}} à votre base de données et à vos données. Elle n'est pas en conformité avec le RGPD. Pour plus de détails sur chacune de ces options, voir la rubrique [Indication d'une base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db). La base de données existante peut être une base de données PostgreSQL ou Db2.
    {: tip}

    ![Sélection de la base de données](images/gs-set-lite-db2.png)

1.  Vérifiez le récapitulatif et cliquez sur **Enregistrer**. Confirmez et, quand vous y êtes invité, cliquez sur le bouton **Poursuivre la configuration**.

    Un ID de magasin de données est également indiqué ; c'est la même chose qu'un ID d'instance {{site.data.keyword.aios_short}}.
    {: tip}

    ![Vérification du récapitulatif](images/gs-setup-summary4.png)

1.  Votre écran peut ressembler à la capture d'écran suivante. Comme vous utiliserez l'interface graphique pour évaluer vos données,
cliquez simplement sur le bouton **Configurer les moniteurs** pour terminer cette configuration.

    ![Code de demande d'évaluation](images/gs-config-send-scoring.png)

### Fournissez un ensemble d'exemples de données à votre modèle
{: #gs-samp}

Pour pouvoir configurer vos moniteurs, vous devez générer au moins une demande d'évaluation de votre modèle afin de générer une journalisation de contenu qu'ils puissent consommer. Dans cette section, vous allez fournir des exemples de données sous la forme d'un fichier JSON pour générer une demande d'évaluation.

1.  Téléchargez le fichier
[credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  Dans l'onglet **Déploiements** de votre projet Watson Studio, cliquez sur le lien **credit-risk-deploy** puis sur l'onglet **Test** et sélectionnez l'icône d'entrée JSON.

    ![Test JSON](images/json_test02.png)

1.  Maintenant, ouvrez le fichier `credit_payload_data.json` que vous avez téléchargé et copiez le contenu dans la zone JSON de l'onglet **Test**. Cliquez sur le bouton **Prévoir** pour envoyer des contenus de formation à votre modèle et les évaluer.

    ![Prévision JSON](images/json_test03.png)

### Préparation de la surveillance
{: #gs-prepmon}

1.  Maintenant, dans l'instance de {{site.data.keyword.aios_short}}, sélectionnez votre déploiement et cliquez sur **Commencer**.

    ![Sélection du déploiement](images/config-select-deploy2.png)

1.  Spécifiez la fonction qui contient la réponse que le modèle prévoira (en d'autres termes, dans votre base de données, la colonne de la table qui contient les libellés ou les valeurs de prévision ). Ici, comme le modèle prévoit le risque de crédit, sélectionnez la colonne **Risk** et cliquez sur **Suivant**.

    ![Préparation de la surveillance](images/config-prep-monitor.png)

1.  Vous allez ensuite fournir des informations sur votre modèle et vos données de formation. Cliquez sur **Suivant**.

    ![Préparation de l'explication](images/config-what-monitor.png)

1.  Dans le menu **Type de données**,
sélectionnez **Numérique/catégoriel** comme type de données analysé par votre déploiement et cliquez sur **Suivant**.

    ![Sélection du type d'entrée](images/config-input-monitor.png)

1.  Pour les données numériques ou catégorielles, vous devez fournir des informations sur les données de formation de votre modèle pour configurer les moniteurs. Sélectionnez **Configurer les moniteurs manuellement** pour fournir les informations de connexion à vos données de formation.

    ![Sélection du type de configuration](images/config-manual-monitor.png)

1.  Le type d'algorithme est important pour surveiller les métriques du modèle, comme l'exactitude. Comme la prévision que le modèle peut faire est "Risque" ou "Aucun risque", sélectionnez le
[type d'algorithme](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) **Classification binaire** ;
cliquez ensuite sur **Suivant**.

    ![Binaire](images/binary.png)

1.  L'emplacement des exemples de données est prérenseigné sur l'écran suivant. Sélectionnez **Suivant** pour continuer.

    ![Indication de l'emplacement Db2 de la page des données de formation](images/gs-config-train-db2-monitor.png)

1.  Le schéma et la table sont également prérenseignés. Cliquez sur **Suivant** pour continuer.

    ![Indication de l'emplacement Db2 du schéma et de la table de formation](images/gs-fair-config-table-db2.png)

1.  Maintenant, vous devez spécifier la fonction qui contient la ou les réponses que le modèle prévoira
(en d'autres termes, dans votre base de données, la colonne de la table qui contient les valeurs de prévision (libellés)). Ici, comme le modèle prévoira le risque de crédit, sélectionnez la colonne **Risk** et cliquez sur **Suivant**.

    Votre base de données de formation contient les valeurs que vous avez fournies pour former votre modèle.
    {: note}

    ![Entrée de libellé de prévision](images/gs-config-label.png)

1.  Sélectionnez les colonnes utilisées pour la formation du modèle. Il s'agit des données attendues par votre déploiement de modèle dans une demande. Toutes les colonnes de données sauf `_training` sont des entrées du modèle. Sélectionnez toutes les autres entrées et cliquez sur **Suivant**.

    ![Entrées d'explicabilité](images/explain_inputs1.png)

1.  Pour les données catégorielles, vous devez identifier les colonnes qui contiennent maintenant des entiers mais contenaient initialement des valeurs texte. Sélectionnez les valeurs indiquées ici.

    ![Entrées d'explicabilité](images/config_categories.png)

1.  Vérifiez le récapitulatif de vos sélections et cliquez sur **Enregistrer** puis sur **OK**.

### Configurez la surveillance de l'équité
{: #gs-cfgfair}

1.  Cliquez sur **Equité**.

1.  Lisez l'explication de l'équité et cliquez sur **Suivant**. Pour plus d'information, voir [Equité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

1.  Vous pouvez maintenant choisir les fonctions à surveiller pour l'équité. Pour chaque fonction que vous sélectionnez,
{{site.data.keyword.aios_short}} surveillera la propension du modèle déployé à donner un résultat favorable pour un groupe sur l'autre. Dans cet exemple, nous surveillerons les fonctions **Sex** et **Age**.

    Les fonctions sont surveillées individuellement, mais n'importe quel débiaisement corrigera simultanément les problèmes de toutes. Cliquez sur les carreaux **Sex** et **Age**, puis sur **Suivant**.

1.  {{site.data.keyword.aios_short}} détecte le biais sur un groupe surveillé par rapport à un groupe de référence. Pour la fonction **Sex**, ajoutez la valeur `male` (masculin) au **Groupe de référence**
et la valeur `female` (féminin) au **Groupe surveillé**, puis cliquez sur **Suivant**.

    Le modèle sera marqué comme biaisé pour le **Sex** si les taux de prévision Risque pour le groupe surveillé diffèrent de ceux pour le groupe de référence. Ainsi, s'il prévoit un risque pour les clients hommes 60 % du temps, et pour les clients femmes 20 % du temps, il est biaisé.

    ![Groupes de sexe](images/gender_groups1.png)

1.  Affectez un seuil d'équité pour le **Sexe**. Le tableau de bord des opérations affiche une alerte si l'équité dépasse le seuil défini. Définissez le seuil à 90 % puis cliquez sur **Suivant**.

1.  Pour la fonction **Age**, ajoutez les valeurs `26-74` au **Groupe de référence**
et les valeurs `19-25` au **Groupe surveillé**, puis cliquez sur **Suivant**.

    Comme avec le **Sex**, le modèle sera marqué comme biaisé pour l'**Age**
si les taux de prévision Risque pour le groupe surveillé diffèrent de ceux pour le groupe de référence. Ainsi, si les clients de 26 à 74 ans ont une prévision Risque à un taux différent de ceux de 19 à 25 ans, le modèle est biaisé.

    ![Groupes BP](images/age_groups.png)

1.  Définissez le seuil pour l'**Age** à 90 % et cliquez sur **Suivant**.

1.  Faites glisser les valeurs de la zone **Valeurs des données de formation**
aux zones **Valeurs favorables** et **Valeurs défavorables**. Pour ce tutoriel, la valeur favorable est **Aucun risque** et la valeur défavorable, **Risque**. Cliquez sur **Suivant**.

    {{site.data.keyword.aios_short}} détecte automatiquement la colonne de la base de données de journalisation de contenu qui contient les valeurs de prévision
et elle présente celles-ci dans la zone **Valeurs des données de formation**. Votre base de données de formation contient les valeurs que vous avez fournies pour la formation de votre modèle,
tandis que la base de données de journalisation de contenu contient les données de commentaires collectées lors de l'exécution du modèle,
que vous pouvez éventuellement utiliser pour reformer et redéployer le modèle.
    {: note}

    ![Valeurs positive et négative](images/pos_and_neg2.png)

1.  Réglez la taille d'échantillon minimale à 100 à l'aide du curseur puis cliquez sur **Suivant**.

    ![Taille minimale](images/gs-fair-config-sample.png)

    Pour ce tutoriel, la taille minimale d'échantillon est définie à 100. Normalement, une taille plus grande est recommandée pour ne pas fausser les résultats.
    {: note}

1.  Vérifiez vos choix et cliquez sur **Enregistrer** puis sur **OK**.

    ![Récapitulatif de la configuration](images/fair-summary.png)

    La fenêtre suivante apparaît ; elle indique un noeud final d'évaluation biaisé. Comme ce tutoriel utilise l'interface graphique et non l'interface ligne de commande pour l'évaluation des données, cliquez sur **OK** pour continuer.

    ![API de débiaisement](images/gs-insight-debias-api.png)

### Configurez la surveillance de l'exactitude
{: #gs-cfgac}

1.  Cliquez sur **Exactitude**.

1.  Lisez l'explication de l'exactitude et cliquez sur **Suivant**. Pour plus d'information, voir [Exactitude](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

1.  Définissez le seuil d'alerte d'exactitude à 90 % et cliquez sur **Suivant**.

1.  Sur l'écran suivant, réglez la taille d'échantillon minimale à 10 à l'aide du curseur puis cliquez sur **Suivant**.

    Pour ce tutoriel, la taille minimale d'échantillon a été définie à 10. Normalement, une taille plus grande est recommandée pour ne pas fausser les résultats.
    {: note}

1.  Pour la taille d'échantillon maximale, utilisez 10000. Cliquez sur **Suivant**.

1.  Vérifiez vos choix et cliquez sur **Enregistrer** puis sur **OK**.

1.  Pour finir, une option vous est proposée d'ajouter des données de commentaires ; ce sujet est abordé à la section suivante. Pour l'instant, fermez la fenêtre en cliquant sur **OK**, sans cliquer sur le bouton **Ajouter des données de commentaires**.

    Pour plus de détails, voir [Configuration du moniteur d'exactitude](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config).

## Fournissez un ensemble d'exemples de données de commentaires à votre modèle
{: #gs-smpfeed}

Pour permettre la surveillance de l'exactitude, vous devez fournir à votre modèle des données de commentaires. Les données d'exactitude n'apparaîtront pas dans le tableau de bord tant que ce ne sera pas fait. Vous pouvez générer les demandes en même temps en ajoutant des exemples de données de commentaires au modèle pour l'évaluation. Pour cette tâche, vous allez télécharger un fichier CSV contenant des exemples de données de commentaires.

1.  Téléchargez le fichier
[credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv).

1.  Dans {{site.data.keyword.aios_short}}, cliquez sur l'onglet **Analyses**.

    ![Analyses](images/insight-dash-tab.png)

1.  Cliquez sur le carreau de votre modèle déployé.

    ![Onglet Analyses - aucune donnée](images/gs-insight-overview.png)

1.  Cliquez ensuite sur l'icône d'édition pour modifier la configuration de déploiement.

    ![L'icône d'édition s'affiche](images/gs-insight-edit-icon.png)

1.  Dans le panneau latéral Récapitulatif, cliquez sur le bouton **Ajouter des données de commentaires**
et sélectionnez le fichier `credit_feedback_data.csv` que vous avez téléchargé. Sélectionnez le délimiteur **Virgule (,)** et cliquez sur **OK**.

    La taille de fichier est actuellement limitée à 8 Mo.
    {: note}

    ![Délimiteur d'exactitude](images/accuracy-delimit.png)

    L'ajout du fichier CSV fournit des données de commentaires au modèle.

    ![Panneau Récapitulatif](images/gs-insight-summary-panel-2.png)

## Affichage des résultats
{: #gs-viewres}

Une fois que vous avez configuré la surveillance de l'exactitude, le contrôle d'exactitude s'exécute au bout d'une heure. Dans un système de production, cela permet au tableau de bord d'accumuler des données de commentaires. Pour ce tutoriel, vous voudrez probablement déclencher le contrôle d'exactitude manuellement après avoir ajouté vos données de commentaires,
pour pouvoir voir les résultats dans le tableau de bord **Analyses**.

Pour voir le résultat immédiatement, sélectionnez un déploiement sur la page **Analyses** et cliquez sur le bouton **Vérifier l'équité maintenant** ou **Vérifier la qualité maintenant**.

### Affichez les analyses de votre déploiement
{: #gs-viewin}

1. Dans le [tableau de bord {{site.data.keyword.aios_short}}](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external},
cliquez sur l'onglet **Analyses**.

  ![Analyses](images/insight-dash-tab.png)

1. Affichez la page Analyses pour voir une vue d'ensemble des métriques de vos modèles déployés. Vous voyez des alertes pour les métriques d'équité ou d'exactitude qui dépassent le seuil de 90 %.

  Les métriques d'équité et d'exactitude peuvent mettre jusqu'à une heure pour apparaître.
  {: tip}

  ![Vue d'ensemble des analyses](images/insight-overview.png)

### Affichez les données de surveillance de votre déploiement
{: #gs-viewmon}

1.  Sélectionnez un déploiement en cliquant sur le carreau correspondant sur la page Analyses. Les données de surveillance du déploiement s'affichent. Remarque : Après le téléchargement du fichier .csv de commentaires,
il se peut que les données d'équité ou d'exactitude ne soient pas mises à jour. Pour voir le résultat immédiatement, cliquez sur le bouton **Vérifier l'équité maintenant** ou **Vérifier la qualité maintenant**.
1.  Faites glisser le marqueur sur le graphique
pour sélectionner les données correspondant à la période sur laquelle vous avez exécuté les exemples de données et les exemples de données de commentaires. Cliquez ensuite sur **Afficher les détails**.

    ![Surveiller les données](images/insight-monitor-data.png)

1.  Ensuite, examinez les graphiques correspondant aux données que vous avez surveillées. Pour cet exemple,
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

1.  S'affiche la liste des transactions qui ont contribué au biais sur la dernière heure. Pour obtenir une explication plus détaillée d'une transaction particulière,
cliquez sur **Expliquer** dans la colonne **ACTION**.

    ![Liste des transactions](images/transaction_list_cr.png)
    
1.  L'explication de la manière dont le modèle est parvenu à sa conclusion apparaît. Elle inclut la confiance du modèle, les facteurs qui ont contribué au niveau de confiance et les colonnes fournies.

    ![Affichage d'une transaction](images/view_transaction1.png)

## Informations connexes
{: #wos-info}

- Pour découvrir ce que sont les biais, voir [Equité](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor).
- Pour savoir si votre modèle prévoit bien les résultats, voir [Exactitude](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- Pour savoir comment interpréter les graphes, les données et les transactions, voir [Surveillance de l'équité, du nombre moyen de demandes par minute et de l'exactitude](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).
