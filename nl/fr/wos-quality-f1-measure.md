---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, F1-Measure

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

# Mesure F1
{: #quality_f1-measr}

La mesure F1 donne la moyenne harmonique de la précision et du rappel.
{: shortdesc}

## La mesure F1 en bref
{: #quality_f1-measr-glance}

- **Description** : moyenne harmonique des précisions et rappels
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de retour deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de retour ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

## Interprétation de l'affichage
{: #quality_f1-measr-display}

![affichage du graphique de mesure F1](images/quality-f1-meas.png)

## Calculs
{: #quality_f1-measr-math}

La mesure F1 est la moyenne harmonique pondérée de la précision et du rappel.

```
          (précision * rappel)
F1 = 2 *  ____________________

          (précision + rappel)
```

