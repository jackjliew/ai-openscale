---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Création de moniteurs et de métriques personnalisés ![balise bêta](images/beta.png)
{: #cst_mtrcs}

Les moniteurs personnalisés consolident un ensemble de métriques personnalisées qui vous permettent de suivre de manière quantitative tous les aspects de votre déploiement de modèle et de votre application métier. Vous pouvez définir des métriques personnalisées et les utiliser parallèlement aux métriques standard, telles que les métriques de qualité, de performances ou d'équité des modèles, qui sont surveillées dans {{site.data.keyword.aios_full}}.
{: shortdesc}

Pour gérer les moniteurs et les métriques personnalisés, vous devez utiliser l'interface de programmes qui fait partie du SDK Python. De la même manière, vous pouvez stocker les métriques personnalisées dans le magasin de données {{site.data.keyword.aios_short}} pour y accéder au besoin. Les métriques personnalisées sont également affichées dans le tableau de bord de {{site.data.keyword.aios_short}}.

## Gestion des métriques personnalisées
{: #cst_mtrc_mgmt}

Pour gérer les métriques personnalisées, vous devez effectuer les tâches suivantes :

1. Enregistrer le moniteur personnalisé avec la définition des métriques.
2. Activer le moniteur personnalisé.
3. Stocker les valeurs des métriques.

Les tutoriels avancés suivants montrent comment procéder :

- [Utilisation
d'{{site.data.keyword.pm_full}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

Vous pouvez désactiver et réactiver à tout moment la surveillance personnalisée. Vous pouvez supprimer un moniteur personnalisé si vous n'en avez plus besoin.

Pour plus d'informations, consultez la [documentation du SDK Python](http://ai-openscale-python-client.mybluemix.net/){: external}.

## Accès et visualisation des métriques personnalisées
{: #cst_mtrcs_viz}

Pour accéder aux métriques personnalisées et les visualiser, vous pouvez utiliser l'interface de programmes. Les tutoriels avancés suivants montrent comment procéder :

- [Utilisation
d'{{site.data.keyword.pm_full}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

   Pour plus d'informations, consultez la [documentation du SDK Python](http://ai-openscale-python-client.mybluemix.net/){: external}.

Vos métriques personnalisées sont affichées dans le tableau de bord de {{site.data.keyword.aios_short}}.
