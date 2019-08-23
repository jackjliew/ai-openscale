---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# Proportion de la variance expliquée
{: #quality_var}

La proportion de variance expliquée est le rapport de la variance expliquée sur la variance cible. La variance expliquée est la différence entre la variance cible et la variance de l'erreur de prévision.
{: shortdesc}

## La proportion de variance expliquée en bref
{: #quality_var-glance}

- **Description** : la proportion de la variance expliquée est le rapport entre la variance expliquée et de la variance cible. La variance expliquée est la différence entre la variance cible et la variance de l'erreur de prévision.
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de retour deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de retour ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

## Interprétation de l'affichage
{: #quality_var-display}

![affichage du graphique de proportion de variance exploqiée](images/xxxx.png)

## Calculs
{: #quality_var-math}

La proportion de variance expliquée est calculée en faisant la moyenne des nombres puis, pour chaque nombre, en soustrayant la moyenne et en mettant les résultats au carré. Puis en calculant les carrés

```
                                  somme des carrés entre les groupes
Proportion de variance expliquée =  ____________________________________

                                      somme du total des carrés
```
