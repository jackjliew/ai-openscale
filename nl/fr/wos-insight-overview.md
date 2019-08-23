---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: dashboard, navigating, navigation, insights

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

# Obtention d'analyses avec {{site.data.keyword.aios_short}}
{: #io-ov}

Vous pouvez suivre tous les déploiements que vous surveillez au moyen du tableau de bord {{site.data.keyword.aios_full}}. Le tableau de bord est votre vue principale de {{site.data.keyword.aios_short}}
et il vous permet d'obtenir des analyses de la qualité de vos modèles.
{: shortdesc}

## Analyses
{: #io-ins}

L'onglet **Analyses**
( ![Tableau de bord Analyse](images/insight-dash-tab.png) )
vous fournit une vue de haut niveau de votre surveillance des déploiements.

  ![Tableau de bord Analyse](images/insight-dashboard.png)

- ***Déploiements surveillés*** -  Dans cet exemple, 10 déploiements au total sont surveillés. Huit d'entre eux sont présentés sous forme de carreaux individuels.

- ***Alertes de qualité*** - Trois alertes de qualité au total (anciennement appelées d'exactitude) sont représentées dans les carreaux suivants.
Dans cet exemple, les déploiements `Driver Performance`, `Market Analytics` et `Pricing Risk`
indiquent respectivement des valeurs d'exactitude de `60%`, `65%` et `79%`.

- ***Alertes d'équité*** - Il y a six alertes d'équité au total,
représentées dans les carreaux suivants et par une petite étiquette `BIAIS`. Dans cet exemple, les déploiements `Driver Performance`, `Market Analytics`, `Regulatory Compliance`,
`Fraud Detection`, `Premium Optimization` et `Damage Cost Estimator`
indiquent respectivement des valeurs d'équité de
`59%`, `68%`, `62%`, `64%`, `79%` et `63%`.

Chaque carreau fournit un résumé de l'activité de surveillance pour le déploiement concerné. Notez que celui du déploiement `Call Center Routing` n'indique aucun problème, ce qui signifie que le modèle est assez stable et exact.


## Analyses de l'équité, de la qualité, des performances, de l'exactitude et de l'analytique
{: #it-ov}

Pour afficher plus de détails sur un déploiement, sélectionnez la tuile correspondante.
Les données de surveillance des différents déploiements s'affichent dans une série de graphiques.
Les graphiques représentent les métriques, comme l'équité, le nombre moyen de demandes par minute ou l'exactitude sur plusieurs jours, semaines ou mois.

- [Affichage des données d'un déploiement](/docs/services/ai-openscale?topic=ai-openscale-it-vdep)
- [Visualisation des données d'une heure spécifique](/docs/services/ai-openscale?topic=ai-openscale-it-vdet)
- l'[équité](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)
- [Qualité](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)
- [Dérive](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
- les [performances](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_performance)
- [Analyses](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)
- [Options de débiaisement](/docs/services/ai-openscale?topic=ai-openscale-it-dbo)

## Explicabilité
{: #io-tran}

Utilisez l'onglet **Expliquer une transaction** ( ![Onglet Expliquer une transaction](images/insight-transact-tab.png) ) pour rechercher un ID de transaction spécifique pour expliquer une transaction de déploiement particulière.

- [Explication des transactions](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)
- [Explication des modèles catégoriels](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Explication des modèles d'image](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Explication des modèles de texte non structuré](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Explications contrastives](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)

## Etapes suivantes
{: #io-next}

- [Ajoutez d'autres déploiements à surveiller](/docs/services/ai-openscale?topic=ai-openscale-dpl-select).

