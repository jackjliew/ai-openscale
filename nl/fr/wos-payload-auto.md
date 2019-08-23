---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Automatisation de la journalisation du contenu utile
{: #fmrk-workaround-pyld-lg}

Il y a une journalisation automatique du contenu utile entre {{site.data.keyword.aios_full}} et {{site.data.keyword.pm_full}}
lorsqu'ils sont mis à disposition dans le même compte {{site.data.keyword.Bluemix_notm}}. Vous pouvez également automatiser la journalisation du contenu utile pour d'autres fournisseurs d'apprentissage automatique
ou pour une instance d'{{site.data.keyword.pm_full}} qui ne ne se trouve pas dans le même compte :
{: shortdesc}

### Cas 1 : Conservation du format d'origine de l'entrée et de la sortie d'évaluation
(différent de celui requis par {{site.data.keyword.aios_short}})
{: #fmrk-workaround-case1}

Si vos applications utilisent un format de contenu utile d'origine qui ne peut pas être changé, choisissez l'une des options suivantes :

- Option 1 : Le point d'extrémité d'évaluation du moteur d'apprentissage automatique personnalisé doit accepter les formats de contenu utile. 

   Selon le format de contenu utile :
{{site.data.keyword.aios_short}} (type {{site.data.keyword.pm_full}}) ou celui de l'utilisateur renvoie la sortie dans le format correspondant. Si le format est celui de l'utilisateur, convertissez-le au format {{site.data.keyword.aios_short}}
et stockez le contenu utile sous forme d'enregistrement de contenu utile dans la table de journalisation du contenu utile. Si le format d'entrée d'évaluation est celui de {{site.data.keyword.aios_short}},
ne stockez pas le contenu utile (il provient de {{site.data.keyword.aios_short}} et non de l'utilisateur).

   Pour plus d'informations, consultez
[Utilisation de deux formats de contenu utile](#fmrk-workaround-notsuppt).

- Option 2 : Si pour une raison quelconque l'incorporation d'une telle logique dans un seul point d'extrémité d'API REST n'est pas possible, vous pouvez définir deux points d'extrémité. 

   L'un est utilisé par votre application, mais vous devez ajouter la journalisation du contenu utile et convertir celui-ci au format attendu. Le deuxième point d'extrémité est utilisé par {{site.data.keyword.aios_short}} pour effectuer les calculs requis, tels que le biais et l'explicabilité. Aucune journalisation du contenu utile n'est requise pour ce point d'extrémité. Lors de la configuration de {{site.data.keyword.aios_short}}, il faut faire pointer le deuxième point d'extrémité sur celui qui a les formats compatibles.

   Pour plus d'informations, consultez
[Utilisation de deux points d'extrémité](#fmrk-workaround-opt2-cs1).

- Option 3 : Déplacez le module de journalisation du contenu utile sur le point d'extrémité initial ou dans l'application aval. 

   Si votre application supporte cette option, il n'y a développer qu'un seul point d'extrémité sur le moteur d'apprentissage automatique personnalisé :
celui pour {{site.data.keyword.aios_short}}.

### Cas 2 : Utilisation du format de contenu utile requis par {{site.data.keyword.aios_short}}
{: #fmrk-workaround-case2}

Dans ce cas, il n'y a aucun besoin d'effectuer une conversion du format de l'utilisateur (entrée/sortie d'évaluation) à celui requis par {{site.data.keyword.aios_short}}.

Comme il ne faut pas que les demandes d'évaluation internes soient consignées comme contenu utile utilisateur
(calculs effectués par {{site.data.keyword.aios_short}}),
vous devez soit développer deux points d'extrémité, soit coder une logique supplémentaire pour un seul point d'extrémité.

- Option 1 : Deux points d'extrémité. Cette option est presque identique à l'option 2 du Cas 1.
La seule différence est qu'il n'y a besoin d'effectuer aucune conversion de format car les formats sont déjà alignés.

- Option 2 : Un seul point d'extrémité. Il y a besoin de détecter si la demande d'évaluation provient de l'application de l'utilisateur. Cela peut être obtenu en envoyant des informations supplémentaires dans le contenu utile d'évaluation (métadonnées). Si ces métadonnées sont détectées, le contenu utile doit être consigné.

## Utilisation de deux formats de contenu utile
{: #fmrk-workaround-notsuppt}

Disons que j'utilise l'offre XYZ pour servir mes modèles. XYZ n'est pas supporté par {{site.data.keyword.aios_short}} pour le moment.

J'ai de nombreuses applications aval qui consomment mes déploiements sur XYZ et je ne peux pas changer le format du contenu utile d'évaluation. En revanche, je peux modifier la logique du point d'extrémité d'évaluation.

### Procédure

1. Développez un moteur d'apprentissage automatique personnalisé qui encapsule le déploiement XYZ.
2. Implémentez le point d'extrémité d'évaluation sur le moteur d'apprentissage automatique personnalisé
pour prendre en charge les formats de contenu utile XYZ et {{site.data.keyword.aios_short}}.
3. Ajoutez la logique dans le point d'extrémité d'évaluation sur votre moteur d'apprentissage automatique personnalisé
pour détecter le format du contenu utile.
4. Si le contenu utile provient d'applications aval,
convertissez-le au format {{site.data.keyword.aios_short}}
et consignez-le sous forme d'enregistrements de contenu utile dans {{site.data.keyword.aios_short}}.
5. Basculez les points d'extrémité d'évaluation des applications aval sur le nouveau que vous avez créé.

Si l'URL du point d'extrémité d'évaluation doit rester la même, utilisez la redirection d'URL, également appelée proxy.

## Utilisation de deux points d'extrémité
{: #fmrk-workaround-opt2-cs1}

Si le format de votre contenu utile ne peut pas être changé,
par exemple si vos applications aval ne pourraient plus fonctionner,
vous devez utiliser des points d'extrémité séparés. Cette approche comprend les éléments suivants :

- point d'extrémité d'évaluation (dans le format de l'utilisateur) avec le point d'extrémité d'évaluation d'origine utilisant le format utilisateur pour l'entrée et la sortie
- moteur d'apprentissage automatique personnalisé avec point d'extrémité de perturbation (format {{site.data.keyword.aios_short}}) et point d'extrémité de reconnaissance - Le point d'extrémité de perturbation encapsule le point d'extrémité d'évaluation d'origine et effectue la conversion
du format {{site.data.keyword.aios_short}} à celui de l'utilisateur et de la sortie utilisateur à celle de {{site.data.keyword.aios_short}}. Ces éléments sont nécessaires pour que {{site.data.keyword.aios_short}} fasse des demandes d'évaluation correctes et comprenne la sortie.
- encapsuleur de point d'extrémité d'évaluation avec fonction de journalisation de contenu utile - Cet encapsuleur est consommé par l'application aval à la place du point d'extrémité d'évaluation d'origine. Sa logique a été étendue avec une fonction de journalisation de contenu utile. Chaque fois qu'une demande d'évaluation est exécutée,
l'entrée et la sortie sont converties au format {{site.data.keyword.aios_short}} et journalisées.

Le diagramme suivant montre la solution de moteur d'apprentissage automatique personnalisé
dans laquelle le moteur gère les points d'extrémité de perturbation et de reconnaissance et les traduit dans votre format :

![Spécification des points d'extrémité d'API REST](images/woscustommlworkflow.png)

### Procédure
{: #fmrk-workaround-smple-cd}

1. En utilisant un bloc-notes, créez un point d'extrémité d'évaluation
pour le déploiement du modèle de risque de crédit (scikit-learn) sur le service d'apprentissage automatique Microsoft Azure. Pour plus d'informations, consultez
[cet exemple de bloc-notes](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb).
2. Créez un moteur d'apprentissage automatique personnalisé et déployez-le sur Microsoft Azure Cloud comme application Flask. Créez les points d'extrémité de perturbation et de reconnaissance.Pour plus d'informations, consultez
[ces instructions de déploiement](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure).
3. Configurez {{site.data.keyword.aios_short}} pour fonctionner avec le moteur d'apprentissage automatique personnalisé.Pour plus d'informations, consultez
[cet exemple de bloc-notes](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb).
4. Créez un encapsuleur de point d'extrémité d'évaluation qui automatise la journalisation du contenu utile sur le service d'apprentissage automatique Microsoft Azure. Pour plus d'informations, consultez
[cet exemple de bloc-notes](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb).

Accordez une attention particulière aux points suivants :

- Identifiants :
Pour rendre le tutoriel plus facile à suivre,
les identifiants {{site.data.keyword.aios_short}} sont codés en dur dans le code (encapsuleur de point d'extrémité d'évaluation). Vous devez remplacer ces valeurs par vos identifiants réels.
- SDK Python ou API REST :
Le tutoriel utilise le SDK Python pour la journalisation du contenu utile. Vous pouvez également utiliser l'API REST, mais vous devez alors générer ou actualiser le jeton vous-même. 
- {{site.data.keyword.cloud_notm}} ou Cloud Pak for Data :
Si vous utilisez {{site.data.keyword.wos4d_notm}},
les identifiants sont dans un format différent ;
[voici l'exemple de bloc-notes](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb). La classe de client {{site.data.keyword.aios_short}} est également différente. Il s'agit de la classe de client `APIClient4ICP`.
- Journalisation du contenu utile dans un point d'extrémité/package séparé -
extraction de la journalisation du contenu utile et des méthodes de conversion dans un package ou point d'extrémité séparé. Elles peuvent ainsi être réutilisées si vous souhaitez injecter un lot de contenus utiles en dehors de l'encapsuleur de point d'extrémité d'évaluation.

