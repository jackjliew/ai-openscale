---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# Taux de faux positifs (FPR - false positive rate) ![étiquette bêta](images/beta.png)
{: #quality_fpr_false}

Le taux de faux positifs donne la proportion de prévisions incorrectes dans la classe positive.
{: shortdesc}

## Taux de faux positifs (FPR)
{: #quality_fpr_false-glance}

- **Description** : proportion de prévisions incorrectes dans la classe positive
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

## Interprétation de l'affichage
{: #quality_fpr_false-display}

![affichage du graphique de taux de faux positifs](images/quality-fpr.png)

## Calculs
{: #quality_fpr_false-math}

Le taux de faux positifs est calculé comme le nombre total de faux positifs divisé par le nombre de faux positifs plus le nombre de vrais négatifs.

```
                          nombre de faux positifs
Taux de faux positifs =  ______________________________________________________

                         (nombre de faux positifs + nombre de vrais négatifs)
```
