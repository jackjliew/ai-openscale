---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

Dans ce tutoriel, vous apprenez à mettre à disposition les services {{site.data.keyword.Bluemix_notm}} requis,
à configurer un projet et déployer un exemple de modèle dans Watson Studio, et à configurer les moniteurs dans {{site.data.keyword.aios_short}}.
{: shortdesc}

1. [Mettre à disposition des services d'apprentissage automatique et de stockage {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps).
2. [Définir un projet Watson Studio et créer, former et déployer un modèle d'apprentissage automatique](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup).
3. [Configurer et explorer la confiance, la transparence et l'explicabilité de votre modèle](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios).

## Mettez à disposition les services {{site.data.keyword.Bluemix_notm}} requis
{: #gs-prps}

En plus de {{site.data.keyword.aios_short}}, il vous faut pour effectuer ce tutoriel les comptes et services suivants.

**Important** :
pour des performances optimales, il est recommandé de créer les services nécessaires dans la même région
que {{site.data.keyword.aios_short}}. Pour connaître les sites disponibles pour {{site.data.keyword.aios_short}}, consultez [Disponibilité du service](/docs/resources?topic=resources-services_region){: external}.

1.  Connectez-vous à votre [compte {{site.data.keyword.Bluemix_notm}}](https://{DomainName}){: external} avec votre {{site.data.keyword.ibmid}}.
1.  Pour chacun des services suivants qui n'est pas encore associé à votre compte, créez une instance en cliquant sur le lien,
en donnant un nom au service, en sélectionnant le forfait **Lite** (gratuit) et en cliquant sur le bouton **Créer** :

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Définissez un projet Watson Studio
{: #gs-setup}

1.  Connectez-vous à votre [compte Watson Studio](https://dataplatform.ibm.com/){: external} et commencez par créer un nouveau projet. Cliquez sur **Créer un projet**.

    ![Création d'un projet Watson Studio](images/studio_create_proj.png)

1.  Cliquez sur le carreau **Créer un projet vide**.
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

    ![le carreau Credit Risk est affiché](images/credit-sample-model.png)

### Déployez le modèle `Credit Risk`
{: #gs-depmod}

1.  Sur la page du modèle `Credit Risk`, cliquez sur l'onglet **Déploiements** puis sur **Ajouter un déploiement**.
1.  Entrez `credit-risk-deploy` comme nom du déploiement et sélectionnez le type de déploiement **Service web**.
1.  Cliquez sur **Enregistrer**.

## Configurez {{site.data.keyword.aios_short}}
{: #gs-confaios}

Maintenant que le modèle d'apprentissage automatique est déployé,
vous pouvez configurer {{site.data.keyword.aios_short}}
pour garantir la fiabilité et la transparence de vos modèles.

### Mettez à disposition {{site.data.keyword.aios_short}}
{: #gs-provaios}

1.  [Mettez à disposition une nouvelle instance de service {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  Donnez un nom à votre service, sélectionnez le **forfait Lite** et cliquez sur **Créer**.

1.  Sélectionnez l'onglet **Gérer** de votre instance de {{site.data.keyword.aios_short}}
et cliquez sur le bouton **Lancer une application**. La page de démonstration **Bienvenue dans {{site.data.keyword.aios_short}}** s'ouvre.
2. Pour ce tutoriel, cliquez sur **Non merci**.

### Sélectionner une base de données
{: #gs-db-choice}

Ensuite, vous devez choisir une base de données. Vous avez deux options : la base de données gratuite ou une base de données existante ou nouvelle.

2. Pour ce tutoriel, sélectionnez le carreau **Utiliser la base de données gratuite du forfait Lite**.

   La base de données gratuite comporte des limitations importantes. Il s'agit d'une base de données hébergée à laquelle vous n'avez pas accès séparément. Elle vous donne l'accès {{site.data.keyword.aios_short}} à votre base de données et à vos données. Elle n'est pas en conformité avec le RGPD. Pour plus de détails sur chacune de ces options, consultez la rubrique [Indication d'une base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db). La base de données existante peut être une base de données PostgreSQL ou Db2.
    {: tip}

   ![Sélection de la base de données](images/gs-set-lite-db2.png)

1.  Vérifiez le récapitulatif et cliquez sur **Enregistrer**. Confirmez et, quand vous y êtes invité, cliquez sur le bouton **Poursuivre la configuration**.

    Un ID de magasin de données est également indiqué ; c'est la même chose qu'un ID d'instance {{site.data.keyword.aios_short}}.
    {: tip}

    ![Vérification du récapitulatif](images/gs-setup-summary4.png)

1.  Votre écran peut ressembler à la capture d'écran suivante. Comme vous utiliserez l'interface graphique pour évaluer vos données,
cliquez simplement sur le bouton **Configurer les moniteurs** pour terminer cette configuration.

    ![Code de demande d'évaluation](images/gs-config-send-scoring.png)

### Connectez {{site.data.keyword.aios_short}} à votre modèle d'apprentissage automatique
{: #gs-ctmod}


1.  Cliquez sur le carreau **Watson Machine Learning**, puis sur **Enregistrer**.

1.  Pour ce tutoriel, sélectionnez votre instance d'{{site.data.keyword.pm_full}} dans le menu et cliquez sur **Suivant**.

    Vous pouvez aussi sélectionner un autre emplacement de {{site.data.keyword.pm_short}}. Pour plus d'informations, consultez
[Indication d'une instance de service {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-wml-connect).
    {: note}

    ![Définition de l'instance de {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

Vous pouvez maintenant sélectionner les modèles déployés qui seront surveillés par {{site.data.keyword.aios_short}}.


### Fournissez un ensemble d'exemples de données à votre modèle
{: #gs-samp}

Pour pouvoir configurer vos moniteurs, vous devez générer au moins une demande d'évaluation de votre modèle afin de générer une journalisation de contenu utile qu'ils puissent consommer.
Dans cette section, vous allez fournir des exemples de données à Watson Studio sous la forme d'un fichier JSON pour générer une demande d'évaluation.

1.  Téléchargez le fichier
[credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  Dans l'onglet **Déploiements** de votre projet Watson Studio, cliquez sur le lien **credit-risk-deploy** puis sur l'onglet **Test** et sélectionnez l'icône d'entrée JSON.

    ![Test JSON](images/json_test02.png)

1.  Maintenant, ouvrez le fichier `credit_payload_data.json` que vous avez téléchargé et copiez le contenu dans la zone JSON de l'onglet **Test**. Cliquez sur le bouton **Prévoir** pour envoyer des contenus utiles de formation à votre modèle et les évaluer.

    ![Prévision JSON](images/json_test03.png)

## Etapes suivantes
{: #gs-next-steps-config}

Continuez ce tutoriel en effectuant les étapes suivantes :

1. [Préparez les moniteurs pour le déploiement](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy).

   Pour préparer les moniteurs, vous devez sélectionner l'un des modèles déployés et l'ajouter au tableau de bord.
Dans l'onglet **Analyses**, cliquez sur un carreau de déploiement ou sur le bouton **Ajouter au tableau de bord**
pour sélectionner un modèle déployé, puis sur **Configurer**.

2. [Configurez la journalisation du contenu utile](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data).

   Dans la section **Journalisation du contenu utile**, vous devez spécifier le type d'entrée.

3. [Configurez les détails du modèle](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets).

   Dans la section **Détails du modèle**, vous devez enregistrer les détails du modèle.
Pour ce tutoriel, sélectionnez **Configurer les moniteurs manuellement**.

4. [Configurez la surveillance de la qualité](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

   Dans la section **Qualité**, vous définissez le seuil d'alerte de qualité et la taille des échantillons.

5. [Configurez la surveillance de l'équité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

   Dans la section **Equité**, choisissez les caractéristiques à surveiller pour l'équité.
Pour chaque caractéristique que vous sélectionnez,
{{site.data.keyword.aios_short}} surveillera la propension du modèle déployé à donner un résultat favorable pour un groupe sur l'autre.
Bien que les caractéristiques soient surveillées individuellement, le débiaisement corrige les problèmes pour toutes les caractéristiques ensemble.

6. [Configurez le moniteur de détection de dérive](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

   Dans la section **Dérive**, vous configurez un modèle de détection de dérive.
   
5. [Fournissez un ensemble d'exemples de données de retour à votre modèle](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv).

   Pour permettre la surveillance de la qualité, vous devez fournir à votre modèle des données de retour.
Les données de qualité n'apparaîtront pas dans le tableau de bord tant que ce ne sera pas fait.
Vous pouvez générer les demandes en même temps en ajoutant des exemples de données de retour au modèle pour l'évaluation. Pour cette tâche, vous allez télécharger un fichier CSV contenant des exemples de données de retour.

6. [Obtenez des analyses](/docs/services/ai-openscale?topic=ai-openscale-io-ov).

   Une fois que vous avez configuré la surveillance de l'exactitude, le contrôle d'exactitude s'exécute au bout d'une heure. Dans un système de production, cela permet au tableau de bord d'accumuler des données de retour. Pour ce tutoriel, vous voudrez probablement déclencher le contrôle d'exactitude manuellement après avoir ajouté vos données de retour,
pour pouvoir voir les résultats dans le tableau de bord **Analyses**.

   Pour voir le résultat immédiatement, sélectionnez un déploiement sur la page **Insights**
et cliquez sur l'une des métriques **Qualité** puis sur **Vérifier la qualité maintenant**.
