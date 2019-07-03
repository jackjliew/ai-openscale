---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits

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

# Moteurs d'apprentissage automatique, infrastructures et modèles pris en charge
{: #in-fram}

Le service {{site.data.keyword.aios_short}} prend en charge les moteurs d'apprentissage automatique suivants. Chaque evironnement d'exécution prend en charge les modèles créés dans les infrastructures suivantes :

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Personnalisé](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) (disponible uniquement dans {{site.data.keyword.wos4d_full}})

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

La prise en charge complète inclut les fonctionnalités suivantes pour l'infrastructure, le problème et le type de données :

- Journalisation de contenu	
- Journalisation de commentaires	
- Exactitude	
- Détection de biais à l'exécution	
- Explicabilité	
- Débiaisement automatique

<p>&nbsp;</p>


## Types de modèle pris en charge
{: #abt-models}

Tableau 1. Détails des modèles pris en charge

| Algorithmes | **Equité** | **Débiaisement automatique** | **Explication** | **Exactitude** |
|:---|:---:|:---:|:---:|:---:|
| **Classification structurée** | Oui | Oui<sup>1</sup> | Oui<sup>1</sup> | Oui |
| **Régression structurée**     | Oui | Bientôt disponible | Oui | Oui |
| **Classification de texte**       | Non - rubrique de recherche active | Non - rubrique de recherche active | Oui<sup>1</sup> | Non |
| **Classification d'image**      | Non - rubrique de recherche active | Non - rubrique de recherche active | Oui<sup>1</sup> | Non ||
{: caption="Détails des modèles pris en charge" caption-side="top"}

<sup>1</sup> Si votre modèle / infrastructure produit des probabilités des prévisions

<p>&nbsp;</p>

## Navigateurs pris en charge
{: #in-brw}

Les outils du service {{site.data.keyword.aios_short}} nécessitent le même niveau de navigateur qu'{{site.data.keyword.cloud_notm}}. Pour le détail, voir la rubrique {{site.data.keyword.cloud_notm}} [Prérequis](/docs/overview?topic=overview-prereqs-platform#browsers-platform).

<p>&nbsp;</p>

## Outil CLI ModelOps
{: #in-mop}

L'[outil d'exploitation de modèle CLI {{site.data.keyword.aios_short}}](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external}
vous permet d'exécuter les tâches liées à la gestion du cycle de vie des modèles d'apprentissage automatique. Il est complémentaire à l'outil CLI {{site.data.keyword.cloud_notm}},
augmenté du [plugin d'apprentissage automatique](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}.

<p>&nbsp;</p>

## Client Python
{: #in-pyc}

Le [client Python {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external}
est une bibliothèque Python qui vous permet de travailler directement avec le service {{site.data.keyword.aios_short}} sur {{site.data.keyword.cloud_notm}}. Vous pouvez l'utiliser, à la place de l'interface utilisateur client {{site.data.keyword.aios_short}},
pour configurer une base de données de journalisation,
lier votre moteur d'apprentissage automatique, et sélectionner et surveiller des déploiements directement. Pour des exemples utilisant le client Python ainsi, voir les
[exemples de bloc-note {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Etapes suivantes
{: #in-next}

- [Initiez-vous](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) au service.
- Consulter la [documentation de référence de l'API](https://{DomainName}/apidocs/ai-openscale){: external}.

Vous avez encore des questions ? 

- [Nouveautés](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contacter IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
