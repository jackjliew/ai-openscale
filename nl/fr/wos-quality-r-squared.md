---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R au carré
{: #quality_r_squared}

R au carré est le rapport de la différence entre la variance cible et la variance de l'erreur de prévision sur la variance cible. Il peut vous indiquer si les données que vous avez utilisées pour créer le modèle conviennent bien à la régression.
{: shortdesc}

## R au carré en bref
{: #quality_r_squared-glance}

- **Description** : ratio de la différence entre la variance cible et la variance de l'erreur de prévision sur la variance cible.
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de retour deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de retour ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

## Interprétation de l'affichage
{: #quality_r_squared-display}

![affichage du graphique de R au carré](images/xxxx.png)

## Calculs
{: #quality_r_squared-math}

La métrique R au carré est calculée par la formule suivante.

```
                  variation expliquée
R au carré =ai-open-scale-ibm-aios-scheduling  | 1 | Service de planification-  _____________________

                    variation totale
```
