---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Infrastructures Microsoft Azure ML Studio
{: #frmwrks-azure}

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures Microsoft Azure Machine Learning Studio suivantes :
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Native | Classification | Structuré |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

## Ajout de Microsoft Azure ML Studio à {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

Vous pouvez configurer {{site.data.keyword.aios_short}} pour qu'il fonctionne avec Microsoft Azure ML Studio
à l'aide d'une des méthodes suivantes :

- Si c'est la première fois que vous ajoutez un fournisseur d'apprentissage automatique à {{site.data.keyword.aios_short}},
vous pouvez utiliser l'interface de configuration.
Pour plus d'information, voir
[Spécification d'une instance Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python.
Cette méthode est obligatoire si vous voulez avoir plusieurs fournisseurs.
Pour savoir comment effectuer cela par programme, voir
[Lier votre moteur d'apprentissage automatique Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


## Exemples de bloc-notes
{: #frmwrks-azure-smpl-ntbks}

Les bloc-notes suivants montrent comment utiliser Microsoft Azure ML Studio :

- [Création d'un magasin de données, surveillance du déploiement de modèle et analyse des données](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Exemples d'évaluation de modèle MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Explorer plus avant
{: #frmwrks-azure-mediumblogs}

[Surveiller l'apprentissage automatique Azure avec Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
