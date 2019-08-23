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

# Présentation des métriques de qualité
{: #anlz_metrics}

La surveillance de la qualité permet de déterminer si votre modèle prévoit bien les résultats. Lorsque la surveillance de la qualité est activée, elle génère un ensemble de métriques toutes les heures par défaut. Vous pouvez générer ces métriques sur demande en cliquant sur le bouton **Vérifier la qualité maintenant** ou en utilisant le client Python.
{: shortdesc}

Les métriques de qualité sont calculées en fonction des informations suivantes :

- données de retour étiquetées manuellement,
- réponses du déploiement surveillé pour ces données.

En vue d'une surveillance adéquate, les données de retour doivent être régulièrement consignées dans {{site.data.keyword.aios_short}}. Les données de retour peuvent être fournies à l'aide de l'option "Ajouter des données de retour" ou en utilisant le client Python ou l'API REST.

Pour les moteurs d'apprentissage automatique autres que {{site.data.keyword.aios_short}}, tels que Microsoft Azure ML Studio, Microsoft Azure ML Service ou Amazon Sagemaker ML, la surveillance de la qualité crée des demandes d'évaluation supplémentaires sur le déploiement surveillé.
{: note}

Vous pouvez examiner les valeurs de toutes les métriques au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique des métriques de qualité montrant la dérive de l'aire sous la courbe ROC](images/quality_metrics_001.png)


Pour consulter les détails connexes, tels que la matrice de confusion pour la classification binaire et multi-classe, qui sont disponibles pour certaines métriques,
cliquez sur le graphique.

![tableau des détails des métriques de qualité](images/quality_metrics_002.png)

## Métriques de qualité prises en charge
{: #anlz_metrics_supqualdets}

Les métriques de qualité suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

- [Aire sous la courbe ROC](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [Aire sous la courbe PR](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [Proportion de la variance expliquée](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_var)
- [Erreur absolue moyenne](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_abserror)
- [Erreur quadratique moyenne](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_squerror)
- [R au carré](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_r_squared)
- [Racine de l'erreur quadratique moyenne](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-supqualdets_squ_errors_mean)
- [Exactitude](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [Taux positif réel pondéré (wTPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-wtpr)
- [Taux positif réel (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [Taux de faux positifs pondéré (wFPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wfpr_weighted)
- [Taux de faux positifs (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [Rappel pondéré](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_weighted_recall)
- [Rappel](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [Précision pondérée](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wgth_prec)
- [Précision](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [Mesure F1 pondérée](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wght_f1-measure)
- [Mesure F1](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [Perte logarithmique](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## Détails de qualité pris en charge
{: #anlz_metrics_supqualdets_suppr_dets}

Les détails suivants des métriques de qualité sont pris en charge par {{site.data.keyword.aios_short}} :

### Matrice de confusion
{: #anlz_metrics_supqualdets_confusion-quickovr}

La matrice de confusion vous aide à déterminer vos données de retour pour lesquelles la réponse du déploiement surveillé est correcte et celles pour lesquelles elle ne l'est pas.

Pour plus d'informations, consultez [Matrice de confusion](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx).

## Etapes suivantes

- Lorsque {{site.data.keyword.aios_short}} détecte un problème de qualité, comme des violations du seuil d'exactitude, vous devez générer une nouvelle version du modèle qui corrige le problème. A l'aide des données libellées manuellement de la table des retours, vous devez reformer le modèle en plus des données de formation d'origine.

