---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Infrastructures ML personnalisées
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures d'apprentissage automatique personnalisé suivantes :
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Equivalente à {{site.data.keyword.pm_full}} | Classification | Structuré |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

## Ajout d'un moteur d'apprentissage automatique personnalisé à {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

Vous pouvez configurer {{site.data.keyword.aios_short}} pour qu'il fonctionne avec un fournisseur d'apprentissage automatique personnalisé
à l'aide d'une des méthodes suivantes :

- Si c'est la première fois que vous ajoutez un fournisseur d'apprentissage automatique personnalisé à {{site.data.keyword.aios_short}},
vous pouvez utiliser l'interface de configuration.
Pour plus d'information, voir
[Specifying a custom machine learning instance](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python.
Cette méthode est obligatoire si vous voulez avoir plusieurs fournisseurs.
Pour savoir comment effectuer cela par programme, voir
[Lier votre moteur d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Exemples de bloc-notes
{: #frmwrks-custom-smpl-ntbks}

- [Création d'un moteur d'apprentissage automatique personnalisé avec un cluster Kubernetes](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Création d'un magasin de données, surveillance du déploiement de modèle et analyse des données](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Explorer plus avant
{: #frmwrks-custom-mediumblogs}

[Surveiller un moteur d'apprentissage automatique personnalisé avec Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
