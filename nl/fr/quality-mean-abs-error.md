---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# Erreur absolue moyenne ![étiquette bêta](images/beta.png)
{: #quality_abserror}

L'erreur absolue moyenne donne la moyenne de la différence absolue entre la prévision du modèle et la valeur cible.
{: shortdesc}

## L'erreur absolue moyenne en bref
{: #quality_abserror-glance}

- **Description** : moyenne de la différence absolue entre la prévision du modèle et la valeur cible
- **Seuils par défaut** : limite supérieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

## Interprétation de l'affichage
{: #quality_abserror-display}

![affichage du graphique d'erreur absolue moyenne](images/xxxx.png)

## Calculs
{: #quality_abserror-math}

L'erreur absolue moyenne est calculée en additionnant toutes les erreurs absolues et en les divisant par le nombre d'erreurs.

```
                              SOMME  | Yi - Xi |
Erreurs absolues moyennes =  ____________________

                              nombre d'erreurs
```
