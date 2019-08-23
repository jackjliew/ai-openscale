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

# Taux positif réel pondéré (wTPR)
{: #quality-wtpr}

le taux de vrais positifs pondéré donne la moyenne pondérée du TPR de classe avec des poids égaux à la probabilité de classe.
{: shortdesc)

## Le taux de vrais positifs pondéré en bref
{: #quality-wtpr-glance}

- **Description** : moyenne pondérée du TPR de classe avec des poids égaux à la probabilité de classe
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de retour deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de retour ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

## Interprétation de l'affichage
{: #quality-wtpr-display}

![Affichage du taux de vrais positifs pondéré](images/quality-tpr.png)

## Calculs
{: #quality-wtpr-math}

Le taux de vrais positifs est calculé avec la formule suivante :

```
                  nombre de vrais positifs
TPR =  _________________________________________________________

        (nombre de vrais positifs + nombre de faux négatifs)
```
