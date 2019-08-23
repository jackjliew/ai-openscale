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

# Rappel
{: #quality_recall}

Le rappel donne la proportion de prévisions correctes dans la classe positive.
{: shortdesc}

## Le rappel en bref
{: #quality_recall-glance}

- **Description** : proportion des prévisions correctes dans la classe positive
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de retour deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de retour ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

## Interprétation de l'affichage de la métrique de rappel
{: #quality_recall-display}

![affichage du graphique de rappel](images/quality-recall.png)

### Score d'équité
{: #quality_recall-display-fairness-score}

Pour la métrique de rappel, le score d'équité suivant est affiché. 

![pourcentage du score de rappel](images/wos-quality-recall-score.png)

### Planning
{: #quality_recall-display-schedule}

Le volet **Planning** affiche l'heure de la **Dernière évaluation** et de la **Prochaine évaluation**.
Les métriques de qualité sont évaluées toutes les heures.
Vous pouvez forcer l'évaluation en cliquant sur **Vérifier la qualité maintenant**.
Vous pouvez également ajouter un retour en cliquant sur **Ajouter des données de retour**.

![volet de planification, avec l'heure de la dernière évaluation et de la prochaine](images/wos-quality-schedule.png)


### Recommandation
{: #quality_recall-display-recommendations}

Afin de vous aider à interpréter le graphique, le volet **Recommandation** affiche les tendances qui indiquent une amélioration ou une détérioration de l'efficacité du modèle.

![volet de recommandation](images/wos-quality-positive-recommendation.png)




## Calculs
{: #quality_recall-math}

Le rappel (R) est défini comme le nombre de vrais positifs (Tp - true positives) sur le nombre de vrais positifs plus le nombre de faux négatifs (Fn).

```
                       nombre de vrais positifs
Rappel =   ______________________________________________________

           (nombre de vrais positifs + nombre de faux négatifs)
```
