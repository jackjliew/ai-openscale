---

title: Fiabilité et transparence pour vos modèles d'apprentissage automatique avec {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this tutorial, you will provision {{site.data.keyword.Bluemix}} machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how {{site.data.keyword.Bluemix}} services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, video

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
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

# Tutoriel d'initiation (configuration automatisée)
{: #gettingstarted}

{{site.data.keyword.aios_full}} permet aux entreprises d'automatiser et de rendre opérationnel le cycle de vie de l'IA dans les applications métier,
afin de garantir que les modèles sont exempts de biais, qu'ils peuvent être facilement expliqués et compris par les professionnels et qu'ils sont auditables dans les transactions commerciales. {{site.data.keyword.aios_short}} prend en charge les modèles d'IA construits et exécutés dans les outils et infrastructures de service de modèle de votre choix.
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

Le modèle de risque de crédit fourni dans ce tutoriel utilise un ensemble de données de formation contenant 20 attributs sur chaque demandeur de prêt. Deux de ces attributs, l'âge et le sexe, peuvent être testés quant au biais. Ce tutoriel se concentrera sur le biais par rapport à ces deux attributs. Pour plus d'informations sur les données de formation, consultez [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

{{site.data.keyword.aios_short}}
surveillera la propension du modèle déployé à donner un résultat favorable ("aucun risque") pour un groupe (le groupe de référence) sur un autre (le groupe surveillé). Dans ce tutoriel, le groupe surveillé est celui des `femmes` pour le sexe, et `19 à 25 ans` pour l'âge.

## Options de configuration
{: #gs-module}

Il y a plusieurs options de configuration, selon votre préférence et votre niveau d'expertise.

- [La configuration automatisée suivante](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start#wos-fast-start)
vous guide dans le processus en effectuant des tâches pour vous en arrière-plan.

   L'utilisation d'une visite guidée signifie que vous pouvez regarder et cliquer pour passer à la partie suivante.
   
- [La configuration interactive](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-obj)
vous permet de prendre le contrôle avec un script facile à suivre.

   Vous pouvez utiliser l'interface pour effectuer les tâches courantes avec un exemple de modèle et des données injectées.
   
- [Le tutoriel avancé](/docs/services/ai-openscale?topic=ai-openscale-crt-ov)
permet aux utilisateurs plus techniques d'installer un module Python
qui automatise la mise à disposition et la configuration des services requis. Il est destiné aux spécialistes des données ou aux utilisateurs à l'aise avec le codage, Python et les bloc-notes. C'est un exemple d'utilisation du client {{site.data.keyword.aios_short}} pour effectuer des opérations par programme. Le bloc-notes utilisé dans ce tutoriel aboutit au même résultat que la [configuration automatisée](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start#wos-fast-start).

   Ce module nécessite que Python 3 soit installé, ce qui inclut le système de gestion de package pip. Pour les instructions, consultez [Installation d'un module Python pour configurer {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module).

Pour d'autres liens de tutoriels, consultez [Autres ressources](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov).

## Configuration automatique
{: #wos-fast-start}

Pour voir rapidement comment {{site.data.keyword.aios_short}} surveille un modèle, exécutez l'option de scénario de démonstration fournie lors de votre première connexion à l'interface utilisateur {{site.data.keyword.aios_short}}.  Voir [Utilisation de la démonstration de l'interface utilisateur](#wos-work-demo).
{: shortdesc}

## Avant de commencer
{: #wos-prereqs}

Avant de commencer la visite guidée, vous devez avoir configuré les ressources suivantes :

- [{{site.data.keyword.ibmid}}](/docs/account?topic=account-signup){: external}
- [{{site.data.keyword.aios_full}}](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#crt-wos-faststart)

La visite de configuration automatisée est conçue pour fonctionner avec le moins possible d'interaction de l'utilisateur. Elle prend automatiquement pour vous les décisions suivantes :

- Si vous avez plusieurs instances d'{{site.data.keyword.pm_full}},
le processus d'installation effectue un appel API pour les répertorier
et choisit la première de la liste. 
- Pour créer une nouvelle version Lite d'{{site.data.keyword.pm_full}},
le programme d'installation de {{site.data.keyword.aios_short}} utilise le groupe de ressources par défaut de votre compte {{site.data.keyword.Bluemix}}.

### Mettez à disposition un service {{site.data.keyword.aios_short}}
{: #crt-wos-faststart}

Si vous ne l'avez pas déjà fait, mettez à disposition {{site.data.keyword.aios_full}}. 

- Si vous n'en avez pas déjà une associée à votre compte, [mettez à disposition une instance de {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external} :

  ![Carreau {{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

1. Cliquez sur **Catalogue** > **IA** > **{{site.data.keyword.aios_short}}**.
2. Donnez un nom à votre service, choisissez un forfait et cliquez sur le bouton **Créer**.
3. Pour démarrer {{site.data.keyword.aios_short}}, cliquez sur le bouton **Lancer l'application**.

## Configuration automatique
{: #wos-work-demo}

1.  Connectez-vous à votre instance {{site.data.keyword.aios_short}} sur {{site.data.keyword.Bluemix}}.
1.  Pour configurer automatiquement votre instance {{site.data.keyword.aios_short}} avec des données exemples, cliquez sur **Configuration automatique**.

   ![Bienvenue dans la démonstration](images/cloud-auto-setup.png)

   Pendant la mise à disposition des services {{site.data.keyword.aios_short}}, vous pouvez regarder le scénario de démonstration.
Une fois la mise à disposition terminée, cliquez sur le bouton **Démarrer la visite**
pour visiter le tableau de bord {{site.data.keyword.aios_short}},
puis allez à la section [Affichage des résultats dans {{site.data.keyword.aios_short}}](#wos-open).

## Affichage des résultats dans {{site.data.keyword.aios_short}}
{: #wos-open}

Pour consulter les analyses de l'équité et de l'exactitude du modèle,
les détails des données surveillées et l'explicabilité d'une transaction individuelle, ouvrez le tableau de bord {{site.data.keyword.aios_short}}. Chaque déploiement est affiché sous la forme d'un carreau. La visite guidée a configuré un déploiement nommé `GermanCreditRiskModel`, montré par la capture d'écran suivante :


   ![Lancement de la démonstration](images/fastpath_demo_11.33.54.png)


### Afficher les analyses
{: #wos-insights}

La page Analyses permet de voir d'un coup d'oeil les problèmes d'équité et d'exactitude déterminés par les seuils configurés.

   ![Lancement de la démonstration](images/fastpath_demo_11.34.00.png)

### Afficher les données de surveillance
{: #wos-monitoring}

1.  Sur la page Analyses, cliquez sur le carreau `GermanCreditRiskModelICP` pour afficher les détails des données surveillées.
1.  Cliquez sur le marqueur du graphe et faites-le glisser pour afficher une période de date et d'heure présentant les données, puis cliquez sur le lien **Afficher les détails**. Vous avez également la possibilité de cliquer sur différentes périodes de temps dans le graphe pour modifier les données affichées. 

Pour savoir comment interpréter le graphe de temps, voir [Obtention d'analyses](/docs/services/ai-openscale?topic=ai-openscale-it-ov).

### Afficher l'explicabilité
{: #wos-explain}

Pour comprendre les facteurs contributeurs s'il y a du biais pour une certaine période, sélectionnez le bouton d'option **Transactions biaisées** dans l'écran de visualisation présenté à la section précédente.

   ![Lancement de la démonstration](images/fastpath_demo_11.35.06.png)

Les ID des transactions de la dernière heure qui présentent un biais s'affichent. Pour le modèle utilisé dans ce module, il y a un biais pour les demandes disponibles.

   ![Lancement de la démonstration](images/fastpath_demo_11.35.12.png)

Pour savoir comment trouver et expliquer les transactions, consultez [Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

   ![Lancement de la démonstration](images/fastpath_demo_11.35.50.png)

## Terminaison de la visite guidée
{: #wos-done-demo}

Une fois que vous avez terminé la visite, vous pouvez ajouter votre propre déploiement de modèle dans le tableau de bord ou continuer à explorer le déploiement du tutoriel. 

- Pour ajouter votre propre modèle au tableau de bord, cliquez sur le bouton **Ajouter au tableau de bord**.
- Pour continuer à explorer le modèle du tutoriel, cliquez sur le carreau German Credit Risk.

## Etapes suivantes
{: #gs-next}

- Apprenez-en plus sur [l'affichage et l'interprétation des données](/docs/services/ai-openscale?topic=ai-openscale-it-ov)
et sur la [surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
