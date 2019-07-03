---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Racine de l'erreur quadratique moyenne (RMSE - root-mean-squared error) ![étiquette bêta](images/beta.png)
{: #supqualdets_squ_errors_mean}

La vue de la racine de l'erreur quadratique moyenne montre la différence entre les valeurs prévues et les valeurs observées de votre modèle.
{: shortdesc}

## La racine de l'erreur quadratique moyenne en bref
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Description** : racine carrée de la moyenne du carré des différences entre la prévision du modèle et la valeur cible
- **Seuils par défaut** : limite supérieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

## Interprétation de l'affichage
{: #supqualdets_squ_errors_mean-display}

![affichage du graphique de racine de l'erreur quadratique moyenne](images/xxxx.png)

## Calculs
{: #supqualdets_squ_errors_mean-math}

La racine de l'erreur quadratique moyenne est la racine carrée de la moyenne des (prévisions moins valeurs observées) au carré.

```
          _________________________________________________________________
RMSE  =  √(prévisions - valeurs observées)*(prévisions - valeurs observées)
```
