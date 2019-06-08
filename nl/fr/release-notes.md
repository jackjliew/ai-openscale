---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

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

Ce document détaille les nouvelles fonctionnalités d'{{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 29 mai 2019
{: #rn-29May2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

- __*Améliorations de l'affichage du biais*__: ![étiquette bêta](images/beta.png)
L'affichage du biais comprend les vues suivantes : 

    - Contenu + Données perturbées :
Comprend la demande d'évaluation reçue pour l'heure sélectionnée
plus des enregistrements d'heures précédentes si le nombre minimum d'enregistrements requis pour l'évaluation n'était pas atteint. Comprend les enregistrements perturbés/synthétisés supplémentaires utilisés pour tester la réponse du modèle lorsque la valeur de la fonction surveillée change.
    - Contenu :
Demandes d'évaluation réelles reçues par le modèle durant l'heure sélectionnée.
    - Formation :
Enregistrements de données de formation utilisés pour former le modèle.
    - Données débiaisées :
Sortie de l'algorithme de débiaisement après traitement des données d'exécution et perturbées.

   Pour plus d'information, voir
[Affichage du biais](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz).

- __*Calcul de l'exactitude pour la sortie débiaisée*__ :
Le calcul de l'exactitude inclut la sortie débiaisée. Vous pouvez comparer l'exactitude du modèle débiaisé à celle d'un modèle de production

   Pour plus d'information, voir [Exactitude](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view).

- __*Possibilité de moteurs d'apprentissage automatique multiples*__ :
{{site.data.keyword.aios_short}} peut prendre en charge plusieurs moteurs d'apprentissage automatique
dans une même instance à condition que la mise à disposition soit effectuée via l'interface de ligne de commande (CLI).

   Pour plus d'information, voir
[Outil de ligne de commande ModelOps](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-mop).

- __*Internationalisation*__ :
{{site.data.keyword.aios_short}} offre des versions localisées et permet de traiter les données dans les langues prises en charge.
L'interface utilisateur, la documentation et les messages d'erreur sont actuellement traduits dans les langues suivantes : 
    - Allemand
    - Français
    - Italien
    - Espagnol
    - Portugais brésilien
    - Japonais
    - Chinois simplifié
    - Chinois traditionnel
    - Coréen

   Pour plus d'information (avec les limitations), voir
[Langues prises en charge pour {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-sl-langs).

- __Amélioration pour les infrastructures *{{site.data.keyword.pm_full}}*__ :
{{site.data.keyword.aios_short}} prend maintenant en charge les infrastructures scikit-learn et XGBoost avec le moteur {{site.data.keyword.pm_full}}.

   Pour plus d'information, voir
[Infrastructures WML](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml).

## 25 avril 2019
{: #rn-25April2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

Outre les améliorations en termes d'utilisation et les mises à jour de sécurité, nos développeurs ont été suffisamment occupés par les nouvelles fonctionnalités. Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées ces dernières semaines :

- __*Visite guidée de la configuration automatique*__ : un nouveau mode de configuration de votre environnement {{site.data.keyword.aios_short}}. Utilisez la [configuration automatique](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start) pour mettre à disposition des services et télécharger et configurer un modèle. Vous remarquerez cette option une fois que vous avez une instance de {{site.data.keyword.aios_short}}.
- __*Basculement vers la version bêta*__ : ![balise bêta](images/beta.png) un nouvel commutateur, **Explorer la nouvelle version bêta**, vous permet de travailler dans notre environnement bêta, où vous pouvez consulter toutes les fonctions les plus récentes et les nouvelles fonctionnalités. Vous n'êtes pas satisfait de ce que vous voyez ? Il suffit de revenir en arrière en cliquant sur **Revenir à la version d'origine**. Il n'y aura aucune incidence sur votre configuration et vos moniteurs. Les fonctionnalités suivantes font partie du programme bêta en cours :
    - __*Matrice de confusion*__ : une [matrice de confusion affiche](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx#it-conf-mtx) les faux positifs et les faux négatifs. Cliquez sur une cellule pour afficher le sous-ensemble d'enregistrements de commentaires.

## 10 avril 2019
{: #rn-10April2019}

- __*L'outil Express Path prend maintenant en charge les modèles client*__ :
Automatisation du processus d'intégration à {{site.data.keyword.aios_short}}.

   Pour plus d'information, voir
[ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/).


## 5 mars 2019
{: #rn-5March2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées depuis l'édition précédente :

- __*Nouveau modèle Credit Risk*__ :
un nouvel exemple de modèle / tutoriel Credit Risk est pris en charge pour tous les moteurs d'évaluation. Pour plus d'information, voir les rubriques
[Initiation](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) et
[Ressources complémentaires](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Calcul du débiaisement*__ :
vous pouvez commuter entre votre modèle de production et un modèle débiaisé créé par {{site.data.keyword.aios_short}}. Pour plus d'information, voir [Modèle de production et modèle débiaisé](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) et
[Fonctionnement du débiaisement](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

## 22 février 2019
{: #rn-22February2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées depuis l'édition précédente :

- __*Modifications de l'interface utilisateur*__ :
Vous pouvez importer un fichier JSON pour configurer par programme tous les moniteurs et fonctions lors de la création d'abonnement. Vous pouvez également exporter le fichier de configuration. Pour plus d'information, voir la rubrique
[Configurer un abonnement de déploiements avec des fichiers JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov).

## 7 février 2019
{: #rn-7February2019}

Voici les nouvelles fonctionnalités et les changements apportés au service.

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

## 14 décembre 2018
{: #rn-14December2018}

Voici les nouvelles fonctionnalités, les changements et les problèmes connus du service.

Voici les fonctionnalités ajoutées à {{site.data.keyword.aios_short}} ou améliorées depuis l'édition bêta :

- __*Disponibilité générale*__ :
Edition Disponibilité générale d'{{site.data.keyword.aios_full_notm}} en forfait IBM Cloud standard (payant).

- __*IBM Cloud Private for Data V1.2*__ :
Si vous utilisez {{site.data.keyword.aios_short}} on IBM Cloud Private for Data V1.2,
consultez la documentation, qui comprend les instructions d'installation, ici :
[Liste de contrôle d'installation](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Prise en charge de votre type de modèle*__ :
En plus des déploiements de modèle d'IA dans Watson Machine Learning,
{{site.data.keyword.aios_short}} prend en charge les déploiements de modèle dans les environnements Microsoft Azure, Amazon SageMaker et personnalisés. Pour plus d'information, voir [Types de modèle pris en charge](/docs/services/ai-openscale?topic=ai-openscale-in-ov).

- __*Base de données "légère" gratuite*__ :
Une base de données gérée "légère" gratuite
fournit tout ce dont vous avez besoin pour commencer à utiliser {{site.data.keyword.aios_short}}. Pour les détails, voir les [forfaits tarifaires {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/watson-openscale){: new_window}.

- __*Surveillance de biais*__ :
Prise en charge d'attributs protégés de type `flottant` et `double`, et détection de biais
sur les modèles de régression linéaire. Et {{site.data.keyword.aios_short}} peut débiaiser automatiquement votre modèle d'IA pour vous. Pour plus d'information, voir [Comprendre l'équité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

- __*Explicabilité*__ :
Prise en charge des modèles de régression, des fonctions Python et des explications contrastives complémentaires. Pour plus d'information, voir [Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

- __*Magasin de données*__ :
Surveillance de la qualité sans s'appuyer sur Watson Machine Learning,
et possibilité d'utiliser votre propre base de données, qu'il s'agisse de Db2, Postgres ou Db2 on Cloud.

- __*Interface utilisateur améliorée*__ :
L'interface utilisateur de {{site.data.keyword.aios_short}} a été améliorée
pour inclure une distribution en histogramme de l'exécution
avec commutation pour les données de formation, l'ID et la gestion de version du modèle, et un tableau des ID de transaction de l'histogramme. Pour plus d'information, voir [Visualisation des données d'une heure spécifique](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).

- __*Autre option pour la configuration du tutoriel*__ :
Pour automatiser la mise à disposition et la configuration des services IBM Cloud requis
et pour voir une application IBM {{site.data.keyword.aios_full}}, avec des exemples de données,
vous pouvez installer et exécuter un module Python. Voir [Installation d'un module Python pour configurer {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

## 17 septembre 2018
{: #rn-17September2018}

- **Edition d'évaluation bêta** - Bienvenue dans l'édition d'évaluation bêta d'{{site.data.keyword.aios_full_notm}}.

<p>&nbsp;</p>

## Etapes suivantes
{: #relnotes-in-next}

Vous avez encore des questions ?

- [Limitations](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [Problèmes connus](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)
