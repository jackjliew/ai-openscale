---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# A propos de
{: #in-ov}

{{site.data.keyword.aios_full}} est un environnement de niveau entreprise pour les applications imprégnées d'IA,
qui permet de voir comment l'IA est construite, utilisée et rentabilisée, à l'échelle de votre entreprise.
{: shortdesc}

<p>&nbsp;</p>

## Implémentation
{: #in-imp}

Voici comment implémenter {{site.data.keyword.aios_short}} :

- **Configurer {{site.data.keyword.aios_short}}** :
Avec l'environnement graphique facile à utiliser,
[configurez une base de données de journalisation de contenu](/docs/services/ai-openscale?topic=ai-openscale-connect-db)
et l'[instance de Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)
dans laquelle vos modèles et déploiements d'IA seront stockés.

- **Utiliser les moniteurs** :
Configurez comment {{site.data.keyword.aios_short}} surveillera chaque déploiement. Vous pouvez surveiller :

    - l'[équité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - l'[exactitude](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)
    - les [performances](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics#anlz_metrics_performance)

- **Afficher et modifier les données suveillées** :
Avec le [tableau de bord](/docs/services/ai-openscale?topic=ai-openscale-io-ov) de {{site.data.keyword.aios_short}},
vous pouvez facilement afficher des analyses clés et identifier les problèmes de vos déploiements. L'affichage des différents points de données pour chaque fonction surveillée fournit des détails supplémentaires.

<p>&nbsp;</p>

## Limitations
{: #in-lim}

- L'édition actuelle ne prend en charge qu'une seule base de données, une seule instance d'{{site.data.keyword.pm_full}}
et une seule instance de {{site.data.keyword.aios_short}}

- La base de données et l'instance d'{{site.data.keyword.pm_full}} doivent être déployées dans le même compte {{site.data.keyword.cloud_notm}}.

- Le forfait Lite (gratuit) comporte les limites mensuelles suivantes :

    - Deux modèles déployés surveillés
    - 20 transactions expliquées
    - 50 000 enregistrements de contenu (cumulés)
    - 50 000 enregistrements de commentaires (cumulés)

- {{site.data.keyword.aios_short}} utilise une base de données PostgreSQL ou Db2 pour stocker
les données se rapportant aux modèles (données de commentaires, contenu d'évaluation) et les métriques calculées. Les forfaits Db2 Lite ne sont pas pris en charge actuellement.

- Il y a une limite de licence de 20 modèles déployés par instance de {{site.data.keyword.aios_short}}.

- Pour {{site.data.keyword.pm_full}}, le contenu d'images perturbées envoyé via la passerelle d'apprentissage automatique ne peut pas dépasser 1 Mo. Afin d'éviter des problèmes de dépassement de délai, les images ne doivent pas dépasser 125 x 125 pixels
et doivent être envoyées séquentiellement pour que l'explication de la seconde image soit demandée lorsque la première est terminée.


<p>&nbsp;</p>

## Problèmes connus
{: #rn-12ki}

- **Microsoft Azure**

    - Des deux types de services web Azure Machine Learning, seul le `nouveau` est accepté par {{site.data.keyword.aios_short}}. Le type `classique` ne l'est pas.

    - __*Il faut utiliser le nom d'entrée par défaut*__ :
Dans le service web Azure, le nom d'entrée par défaut est `"input1"`. Cette zone est actuellement obligatoire pour {{site.data.keyword.aios_short}}, qui ne peut pas fonctionner si elle manque.

      Si votre service web Azure n'utilise pas le nom par défaut, remplacez le nom d'entrée par `"input1"` et le code fonctionnera.

- **AWS SageMaker**

    - __*L'algorithme BlazingText n'est pas pris en charge*__ :
Le format de contenu d'entrée de l'algorithme AWS SageMaker BlazingText n'est pas pris en charge dans l'édition actuelle de {{site.data.keyword.aios_short}}.

- **Instance de service ML personnalisé**

    - Avec le [module Python](/docs/services/ai-openscale?topic=ai-openscale-as-module),
l'explicabilité ne fonctionne pas pour l'instance de service personnalisée. Ceci est dû au fait que l'instance de service personnalisée requiert une prévision numérique dans les données de réponse,
qui n'est pas incluse avec le script du module.

<p>&nbsp;</p>

## Moteurs d'apprentissage automatique et infrastructures pris en charge
{: #in-fram}

Le service {{site.data.keyword.aios_short}} prend en charge les moteurs d'apprentissage automatique suivants. Chaque evironnement d'exécution prend en charge les modèles créés dans les infrastructures suivantes :

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Personnalisé](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS (ICP uniquement)](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

La prise en charge complète inclut les fonctionnalités suivantes pour l'infrastructure, le problème et le type de données :

- Journalisation de contenu	
- Journalisation de commentaires	
- Exactitude	
- Détection de biais à l'exécution	
- Explicabilité	
- Débiaisement automatique

<p>&nbsp;</p>

## Navigateurs pris en charge
{: #in-brw}

Les outils du service {{site.data.keyword.aios_short}} nécessitent le même niveau de navigateur qu'{{site.data.keyword.cloud_notm}}. Pour le détail, voir la rubrique {{site.data.keyword.cloud_notm}} [Prérequis](/docs/overview?topic=overview-prereqs-platform#browsers-platform).

<p>&nbsp;</p>

## Outil CLI ModelOps
{: #in-mop}

L'[outil d'exploitation de modèle CLI {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window}
vous permet d'exécuter les tâches liées à la gestion du cycle de vie des modèles d'apprentissage automatique. Il est complémentaire à l'{{site.data.keyword.cloud_notm}} outil CLI,
augmenté du [plugin d'apprentissage automatique
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}.

<p>&nbsp;</p>

## Client Python
{: #in-pyc}

Le [client Python {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://ai-openscale-python-client.mybluemix.net/){: new_window}
est une bibliothèque Python qui vous permet de travailler directement avec le service {{site.data.keyword.aios_short}} sur {{site.data.keyword.cloud_notm}}. Vous pouvez l'utiliser, à la place de l'interface utilisateur client {{site.data.keyword.aios_short}},
pour configurer une base de données de journalisation,
lier votre moteur d'apprentissage automatique, et sélectionner et surveiller des déploiements directement. Pour des exemples utilisant le client Python ainsi, voir les
[bloc-notes d'exemples {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Etapes suivantes
{: #in-next}

- [Initiez-vous](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) au service.
- Consultez les [matériaux de Référence des API
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/ai-openscale){: new_window}.

Vous avez encore des questions ? 

- [Nouveautés](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contacter IBM
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
