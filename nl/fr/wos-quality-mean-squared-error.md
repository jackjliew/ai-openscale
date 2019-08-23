---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean squared error

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

# Erreur quadratique moyenne
{: #quality_squerror}

L'erreur quadratique moyenne donne la moyenne de la différence quadratique entre la prévision du modèle et la valeur cible. Elle peut être utilisée comme mesure de la qualité d'un estimateur.
{: shortdesc}

## L'erreur quadratique moyenne en bref
{: #quality_squerror-glance}

- **Description** : moyenne du carré des différences entre la prévision du modèle et la valeur cible
- **Seuils par défaut** : limite supérieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique se dégrade. Les données de retour deviennent nettement différentes des données de formation.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de retour ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

## Interprétation de l'affichage
{: #quality_squerror-display}

![affichage du graphique d'erreur quadratique moyenne](images/xxxx.png)

## Calculs
{: #quality_squerror-math}

L'erreur quadratique moyenne dans sa forme la plus simple est définie par la formule suivante.

```
                         SOMME  (Yi - ^Yi) * (Yi - ^Yi)
Erreurs quadratiques moyennes  =  ________________________________

                             nombre d'erreurs
```
