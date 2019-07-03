---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Infrastructures Amazon SageMaker
{: #frmwrks-aws-sage}

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures Amazon SageMaker suivantes :
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Native | Classification | Structuré |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}


## Ajout d'Amazon SageMaker à {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

Vous pouvez configurer {{site.data.keyword.aios_short}} pour qu'il fonctionne avec Amazon SageMaker
à l'aide d'une des méthodes suivantes :

- Si c'est la première fois que vous ajoutez un fournisseur d'apprentissage automatique à {{site.data.keyword.aios_short}},
vous pouvez utiliser l'interface de configuration.
Pour plus d'information, voir
[Spécification d'une instance Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python.
Cette méthode est obligatoire si vous voulez avoir plusieurs fournisseurs.
Pour savoir comment effectuer cela par programme, voir
[Lier votre moteur d'apprentissage automatique Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Exemples de bloc-notes
{: #frmwrks-aws-sage-smpl-ntbks}

Les bloc-notes suivants montrent comment utiliser Amazon SageMaker :

- [Création et déploiement du modèle de prévision de risque de crédit](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Création d'un magasin de données, surveillance du déploiement de modèle et analyse des données](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## Explorer plus avant
{: #frmwrks-aws-sage-mediumblogs}

[Surveiller l'apprentissage automatique Sagemaker avec Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
