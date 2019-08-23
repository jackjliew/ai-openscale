---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# Aire sous la courbe ROC
{: #quality_roc}

L'aire sous la courbe ROC (receiver operating characteristic - caractéristique d'efficacité du récepteur) donne la surface sous la courbe de rappel et de taux de faux positifs. Elle correspond à la sensibilité par rapport au taux de conséquences.
{: shortdesc}

## Aire sous la courbe ROC en bref
{: #quality_roc-glance}

- **Description** : surface sous la courbe des taux de faux positifs et de rappels
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de retour deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de retour ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

## Interprétation de l'affichage
{: #quality_roc-display}

![affichage du graphique de zone sous la courbe ROC](images/quality-area-under-roc.png)

## Calculs
{: #quality_roc-math}

L'aire sous la courbe ROC est tracée paramétriquement
comme le `taux de vrais positifs` par rapport au `taux de faux positifs`
relativement à un seuil `T`.



