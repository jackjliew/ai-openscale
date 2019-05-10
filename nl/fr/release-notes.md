---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: release notes, what's new 

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

# Nouveautés
{: #rn-relnotes}

Ce document détaille les nouvelles fonctionnalités et les problèmes connus d'{{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 5 mars 2019
{: #rn-5March2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

### Nouvelles fonctionnalités et changements
{: #rn-5March2019nf}

Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées depuis l'édition précédente :

- __*Nouveau modèle Credit Risk*__ :
un nouvel exemple de modèle / tutoriel Credit Risk est pris en charge pour tous les moteurs d'évaluation.
Pour plus d'information, voir les rubriques
[Initiation](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) et
[Ressources complémentaires](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Calcul du débiaisement*__ :
vous pouvez commuter entre votre modèle de production et un modèle débiaisé créé par {{site.data.keyword.aios_short}}.
Pour plus d'information, voir [Modèle de production et modèle débiaisé](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) et
[Fonctionnement du débiaisement](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

## 22 février 2019
{: #rn-22February2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

### Nouvelles fonctionnalités et changements
{: #rn-22February2019nf}

Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées depuis l'édition précédente :

- __*Modifications de l'interface utilisateur*__ :
Vous pouvez importer un fichier JSON pour configurer par programme tous les moniteurs et fonctions lors de la création d'abonnement.
Vous pouvez également exporter le fichier de configuration.
Pour plus d'information, voir la rubrique
[Configurer un abonnement de déploiements avec des fichiers JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov).

## 7 février 2019
{: #rn-7February2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

### Nouvelles fonctionnalités et changements
{: #rn-7February2019nf}

Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées depuis l'édition précédente :

- __*Modifications de l'interface utilisateur*__ :
Plusieurs améliorations ont été apportées à l'interface utilisateur de {{site.data.keyword.aios_short}},
notamment un moyen de [contrôler l'équité et l'exactitude à la demande](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)
et la possibilité de voir la liste des transactions depuis le [graphe des détails d'équité](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Améliorations de l'explicabilité*__ :
Tous les nombres ont maintenant la même précision/échelle pour les valeurs positives pertinentes et négatives pertinentes.

- __*Support SSL de Db2*__ :
{{site.data.keyword.aios_short}} accepte la transmission des certificats autosignés (codés en base-64) avec les identifiants DB2.

- __*Support des bases de données IBM Cloud*__ :
{{site.data.keyword.aios_short}} accepte maintenant Databases for PostgreSQL, en plus de Compose for PostgreSQL et Db2)

### Problèmes connus
{: #rn-7February2019ki}

- **Instance de service ML personnalisé**

    - Avec le [module Python](/docs/services/ai-openscale?topic=ai-openscale-as-module),
l'explicabilité ne fonctionne pas pour l'instance de service personnalisée.
Ceci est dû au fait que l'instance de service personnalisée requiert une prévision numérique dans les données de réponse,
qui n'est pas incluse avec le script du module.

## 14 décembre 2018
{: #rn-14December2018}

Voici les nouvelles fonctionnalités, les changements et les problèmes connus du service.

### Nouvelles fonctionnalités et changements
{: #rn-12nf}

Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées depuis l'édition bêta :

- __*Disponibilité générale*__ :
Edition Disponibilité générale d'{{site.data.keyword.aios_full_notm}} en forfait IBM Cloud standard (payant).

- __*IBM Cloud Private for Data V1.2*__ :
Si vous utilisez {{site.data.keyword.aios_short}} on IBM Cloud Private for Data V1.2,
consultez la documentation, qui comprend les instructions d'installation, ici :
[Liste de contrôle d'installation](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Prise en charge de votre type de modèle*__ :
En plus des déploiements de modèle d'IA dans Watson Machine Learning,
{{site.data.keyword.aios_short}} prend en charge les déploiements de modèle dans les environnements Microsoft Azure, Amazon SageMaker et personnalisés.
Pour plus d'information, voir [Types de modèle pris en charge](/docs/services/ai-openscale?topic=ai-openscale-in-ov).

- __*Base de données "légère" gratuite*__ :
Une base de données gérée "légère" gratuite
fournit tout ce dont vous avez besoin pour commencer à utiliser {{site.data.keyword.aios_short}}.
Pour les détails, voir les [forfaits tarifaires {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/watson-openscale){: new_window}.

- __*Surveillance de biais*__ :
Prise en charge d'attributs protégés de type `flottant` et `double`, et détection de biais
sur les modèles de régression linéaire.
Et {{site.data.keyword.aios_short}} peut débiaiser automatiquement votre modèle d'IA pour vous.
Pour plus d'information, voir [Comprendre l'équité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

- __*Explicabilité*__ :
Prise en charge des modèles de régression, des fonctions Python et des explications contrastives complémentaires.
Pour plus d'information, voir [Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

- __*Magasin de données*__ :
Surveillance de la qualité sans s'appuyer sur Watson Machine Learning,
et possibilité d'utiliser votre propre base de données, qu'il s'agisse de Db2, Postgres ou Db2 on Cloud.

- __*NeuNetS (bêta)*__ :
IBM NeuNetS (Neural Network Synthesizer) est disponible en édition bêta (cloud public uniquement).
Pour plus d'information, voir la [documentation de NeuNetS
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}.

- __*Interface utilisateur améliorée*__ :
L'interface utilisateur de {{site.data.keyword.aios_short}} a été améliorée
pour inclure une distribution en histogramme de l'exécution
avec commutation pour les données de formation, l'ID et la gestion de version du modèle, et un tableau des ID de transaction de l'histogramme.
Pour plus d'information, voir [Visualisation des données d'une heure spécifique](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).

- __*Autre option pour la configuration du tutoriel*__ :
Pour automatiser la mise à disposition et la configuration des services IBM Cloud requis
et pour voir une application IBM {{site.data.keyword.aios_full}}, avec des exemples de données,
vous pouvez installer et exécuter un module Python.
Voir [Installation d'un module Python pour configurer {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

### Problèmes connus
{: #rn-12ki}

- **Microsoft Azure**

    - Des deux types de services web Azure Machine Learning, seul le `nouveau` est accepté par {{site.data.keyword.aios_short}}.
Le type `classique` ne l'est pas.

    - __*Il faut utiliser le nom d'entrée par défaut*__ :
Dans le service web Azure, le nom d'entrée par défaut est `"input1"`.
Cette zone est actuellement obligatoire pour {{site.data.keyword.aios_short}}, qui ne peut pas fonctionner si elle manque.

      Si votre service web Azure n'utilise pas le nom par défaut, remplacez le nom d'entrée par `"input1"` et le code fonctionnera.

- **AWS SageMaker**

    - __*L'algorithme BlazingText n'est pas pris en charge*__ :
Le format de contenu d'entrée de l'algorithme AWS SageMaker BlazingText n'est pas pris en charge dans l'édition actuelle de {{site.data.keyword.aios_short}}.

## 17 septembre 2018
{: #rn-17September2018}

### Nouvelles fonctionnalités et changements
{: #rn-17nf}

- **Edition d'évaluation bêta** - Bienvenue dans l'édition d'évaluation bêta d'{{site.data.keyword.aios_full_notm}}.
