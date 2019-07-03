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

# Présentation des métriques de qualité ![étiquette bêta](images/beta.png)
{: #anlz_metrics}

La surveillance de la qualité permet de déterminer si votre modèle prévoit bien les résultats. Lorsque la surveillance de la qualité est activée, elle génère un ensemble de métriques toutes les heures par défaut. Vous pouvez générer ces métriques sur demande en cliquant sur le bouton **Vérifier la qualité maintenant** ou en utilisant le client Python.

Les métriques de qualité sont calculées en fonction des informations suivantes :

- données de commentaires étiquetées manuellement,
- réponses du déploiement surveillé pour ces données.

En vue d'une surveillance adéquate, les données de commentaires doivent être régulièrement consignées dans {{site.data.keyword.aios_short}}. Les données de commentaires peuvent être fournies à l'aide de l'option "Ajouter des données de commentaires" ou en utilisant le client Python ou l'API REST.

Pour les moteurs d'apprentissage automatique autres que {{site.data.keyword.aios_short}}, par exemple Microsoft Azure ML Studio ou Amazon Sagemaker ML, la surveillance de l'équité crée des demandes d'évaluation supplémentaires sur le déploiement surveillé.
{: note}

Vous pouvez examiner les valeurs de toutes les métriques au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique des métriques de qualité montrant la dérive de la zone sous la courbe ROC](images/quality_metrics_001.png)


Pour consulter les détails connexes, tels que la matrice de confusion pour la classification binaire et multi-classe, qui sont disponibles pour certaines métriques,
cliquez sur le graphique.

![tableau des détails des métriques de qualité](images/quality_metrics_002.png)

## Métriques de qualité prises en charge
{: #anlz_metrics_supqualdets}

Les métriques de qualité suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

- [Zone sous la courbe ROC](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [Zone sous la courbe PR](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [Proportion de la variance expliquée](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_var){: download}
- [Erreur absolue moyenne](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_abserror){: download}
- [Erreur quadratique moyenne](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_squerror){: download}
- [R au carré](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_r_squared){: download}
- [Racine de l'erreur quadratique moyenne](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-supqualdets_squ_errors_mean){: download}
- [Exactitude](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [Taux positif réel pondéré (wTPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-wtpr){: download}
- [Taux positif réel (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [Taux de faux positifs pondéré (wFPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wfpr_weighted){: download}
- [Taux de faux positifs (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [Rappel pondéré](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_weighted_recall){: download}
- [Rappel](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [Précision pondérée](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wgth_prec){: download}
- [Précision](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [Mesure F1 pondérée](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wght_f1-measure){: download}
- [Mesure F1](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [Perte logarithmique](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## Détails de qualité pris en charge
{: #anlz_metrics_supqualdets_suppr_dets}

Les détails suivants des métriques de qualité sont pris en charge par {{site.data.keyword.aios_short}} :

### Matrice de confusion
{: #anlz_metrics_supqualdets_confusion-quickovr}

La matrice de confusion vous aide à déterminer vos données de commentaires pour lesquelles la réponse du déploiement surveillé est correcte et celles pour lesquelles elle ne l'est pas.

Pour plus d'information, voir [Matrice de confusion](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx).
