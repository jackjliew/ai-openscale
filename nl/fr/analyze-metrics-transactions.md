---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: metrics, monitoring, custom metrics, thresholds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyse des métriques et des transactions ![balise bêta](images/beta.png)
{: #anlz_metrics}

{{site.data.keyword.aios_full}} permet d'analyser les mesures et les transactions par divers moyens. {: shortdesc}

## Métriques d'équité
{: #anlz_metrics_fairness}

Utilisez la surveillance de l'équité pour déterminer si les résultats produits par votre modèle sont équitables ou non pour le groupe surveillé. Lorsque la surveillance de l'équité est activée, elle génère un ensemble de métriques toutes les heures par défaut. Vous pouvez générer ces métriques sur demande en cliquant sur le bouton **Vérifier la qualité maintenant** ou en utilisant le client Python.

Les métriques d'équité sont calculées en fonction des informations suivantes :

- données de contenu d'évaluation. 

En vue d'une surveillance adéquate, toutes les demandes d'évaluation doivent être consignées également dans {{site.data.keyword.aios_short}}. La journalisation des données de contenu est automatisée pour les moteurs {{site.data.keyword.pm_full}}. 

Pour les autres moteurs d'apprentissage automatique, les données de contenu peuvent être fournies à l'aide du client Python ou de l'API REST.

Pour les moteurs d'apprentissage automatique autres que {{site.data.keyword.pm_full}}, la surveillance de l'équité crée des demandes d'évaluation supplémentaires sur le déploiement surveillé.{: note}

Vous pouvez examiner la valeur de toutes les métriques au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique des métriques de l'équité montrant une baisse au-dessous du seuil](images/fairness_metrics_001.png)

Vous pouvez consulter les détails connexes, tels que des résultats favorables et défavorables :

![détails de l'équité](images/fairness_metrics_002.png)

Vous pouvez consulter les transactions détaillées :

![graphique de l'équité montrant une liste de transactions](images/fairness_metrics_003.png)

Vous pouvez consulter le noeud final d'évaluation débiaisée recommandé :

![détails du noeud final d'évaluation débiaisée](images/fairness_metrics_004.png)

### Métriques d'équité prises en charge
{: #anlz_metrics_supfairmets}

Les métriques d'équité suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

#### Equité d'un groupe
{: #anlz_metrics_supfairmets_group}

- **Description** : la propension des modèles à donner des résultats favorables à un groupe sur un autre. 
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** : noeud final d'évaluation débiaisée que vous pouvez utiliser dans votre application métier pour recevoir des réponses débiaisées de votre modèle déployé. 
- **Type de problème** : tous
- **Type de données** : structuré
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : oui

### Détails d'équité pris en charge
{: #anlz_metrics_supfairdets}

Les détails suivants des métriques d'équité sont pris en charge par {{site.data.keyword.aios_short}} :

- Pourcentages favorables pour chacun des groupes
- Moyennes d'équité pour tous les groupes d'équité

  Taux d'impact disparate = (% de résultats favorables dans le groupe surveillé) / (% de résultats favorables dans le groupe de référence)

- Distribution des données pour chacun des groupes surveillés
- Distribution des données de contenu


<!---
BTW, I propose to use screenshots with data from FastPath.
Source monitored group or referenced group
Source of bias is also in fairness metrics
--->


## Métriques de qualité
{: #anlz_metrics_quality}

La surveillance de la qualité permet de déterminer si votre modèle prévoit bien les résultats. Lorsque la surveillance de la qualité est activée, elle génère un ensemble de métriques toutes les heures par défaut. Vous pouvez générer ces métriques sur demande en cliquant sur le bouton **Vérifier la qualité maintenant** ou en utilisant le client Python.

Les métriques de qualité sont calculées en fonction des informations suivantes :

- données de commentaires étiquetées manuellement, 
- réponses du déploiement surveillé pour ces données. 

En vue d'une surveillance adéquate, les données de commentaires doivent être régulièrement consignées dans {{site.data.keyword.aios_short}}. Les données de commentaires peuvent être fournies à l'aide de l'option "Ajouter des données de commentaires" ou en utilisant le client Python ou l'API REST. 

Pour les moteurs d'apprentissage automatique autres que {{site.data.keyword.aios_short}}, par exemple Microsoft Azure ML Studio ou Amazon Sagemaker ML, la surveillance de l'équité crée des demandes d'évaluation supplémentaires sur le déploiement surveillé.{: note}

Vous pouvez examiner les valeurs de toutes les métriques au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique des métriques de qualité montrant la dérive de la zone sous la courbe ROC](images/quality_metrics_001.png)


Pour certaines métriques, vous pouvez également consulter les détails connexes, tels que la matrice de confusion pour la classification binaire et multi-classes.

![tableau des détails des métriques de qualité](images/quality_metrics_002.png)

### Métriques de qualité prises en charge
{: #anlz_metrics_supqualdets}

Les métriques de qualité suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

#### Zone sous la courbe ROC
{: #anlz_metrics_supqualdets_roc}

- **Description** : surface sous la courbe des taux de faux positifs et de rappels 
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Zone sous la courbe PR
{: #anlz_metrics_supqualdets_pr}

- **Description** : surface sous la courbe de précision et de rappel
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Proportion de la variance expliquée
{: #anlz_metrics_supqualdets_var}

- **Description** : la proportion de la variance expliquée est le rapport entre la variance expliquée et de la variance cible. La variance expliquée est la différence entre la variance cible et la variance de l'erreur de prévision.
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

#### Erreur absolue moyenne
{: #anlz_metrics_supqualdets_abserror}

- **Description** : moyenne de la différence absolue entre la prévision du modèle et la valeur cible
- **Seuils par défaut** : limite supérieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

#### Erreur quadratique moyenne
{: #anlz_metrics_supqualdets_squerror}

- **Description** : moyenne du carré des différences entre la prévision du modèle et la valeur cible
- **Seuils par défaut** : limite supérieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

#### R au carré
{: #anlz_metrics_supqualdets_r_squared}

- **Description** : ratio de la différence entre la variance cible et la variance de l'erreur de prévision sur la variance cible. 
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

#### Racine de l'erreur quadratique moyenne
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Description** : racine carrée de la moyenne du carré des différences entre la prévision du modèle et la valeur cible
- **Seuils par défaut** : limite supérieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : régression
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

#### Exactitude
{: #anlz_metrics_supqualdets_acc}

- **Description** : proportion des prévisions correctes
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Types de problème** : classification binaire et classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Taux positif réel pondéré (wTPR)
{: #anlz_metrics_supqualdets_wtpr}

- **Description** : moyenne pondérée du TPR de classe avec des poids égaux à la probabilité de classe
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Taux positif réel (TPR)
{: #anlz_metrics_supqualdets_tpr}

- **Description** : proportion des prévisions correctes dans les prévisions de la classe positive
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Taux de faux positifs pondéré (wFPR)
{: #anlz_metrics_supqualdets_wfpr_weighted}

- **Description** : moyenne pondérée du FPR de classe avec des poids égaux à la probabilité de classe
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Taux de faux positifs (FPR)
{: #anlz_metrics_supqualdets_fpr_false}

- **Description** : proportion des prévisions incorrectes dans la classe positive
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Rappel pondéré
{: #anlz_metrics_supqualdets_weighted_recall}

- **Description** : moyenne pondérée des rappels avec des poids égaux à la probabilité de classe
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Rappel
{: #anlz_metrics_supqualdets_recall}

- **Description** : proportion des prévisions correctes dans la classe positive
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Précision pondérée
{: #anlz_metrics_supqualdets_wgth_prec}

- **Description** : moyenne pondérée des précisions avec des poids égaux à la probabilité de classe
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Précision
{: #anlz_metrics_supqualdets_precision}

- **Description** : proportion des prévisions correctes dans les prévisions de la classe positive
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Mesure F1 pondérée
{: #anlz_metrics_supqualdets_wght_f1-measure}

- **Description** : moyenne pondérée de la mesure F1 avec des poids égaux à la probabilité de classe
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Mesure F1
{: #anlz_metrics_supqualdets_f1-measr}

- **Description** : moyenne harmonique des précisions et rappels
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion

#### Perte logarithmique
{: #anlz_metrics_supqualdets_log_loss}

- **Description** : moyenne des logarithmes des probabilités de classe cible (confiance). Egalement appelée log de vraisemblance attendu. 
- **Seuils par défaut** : limite inférieure = 0,8
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique m s'améliore. Cela signifie que le recyclage des modèles est effectif. 
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique m se dégrade. Les données de commentaires deviennent nettement différentes des données de formation. 
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Type de problème** : classification binaire et classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : aucun

### Détails de qualité pris en charge
{: #anlz_metrics_supqualdets_suppr_dets}

Les détails suivants des métriques de qualité sont pris en charge par {{site.data.keyword.aios_short}} :

#### Matrice de confusion
{: #anlz_metrics_supqualdets_confusion}

La matrice de confusion vous aide à déterminer vos données de commentaires pour lesquelles la réponse du déploiement surveillé est correcte et celles pour lesquelles elle ne l'est pas. 

## Métriques de performances
{: #anlz_metrics_performance}

Utilisez la surveillance des performances pour connaître la vitesse des enregistrements de données traités par votre déploiement. Vous pouvez activer la surveillance des performances lorsque vous sélectionnez le déploiement qui doit être suivi et surveillé par {{site.data.keyword.aios_short}}.

Les métriques de performances sont calculées en fonction des informations suivantes :

- données de contenu d'évaluation 

En vue d'une surveillance adéquate, toutes les demandes d'évaluation doivent être consignées également dans {{site.data.keyword.aios_short}}. La journalisation des données de contenu est automatisée pour les moteurs {{site.data.keyword.pm_full}}. Pour les autres moteurs d'apprentissage automatique, les données de contenu peuvent être fournies à l'aide du client Python ou de l'API REST. La surveillance des performances ne crée pas de demandes d'évaluation supplémentaires sur le déploiement surveillé.

Vous pouvez examiner la valeur des métriques de performances au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique de performances](images/performance_metrics_001.png)

### Métriques de performances prises en charge
{: #anlz_metrics_performance_supp_quality_mets}

Les métriques de performances suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

#### Débit
{: #anlz_metrics_performance_supp_quality_mets_through}

- **Description** : moyenne des demandes d'évaluation par minute dans la période donnée
- **Seuils par défaut** : non applicable
- **Recommandation par défaut** : non applicable
- **Type de problème** : tous
- **Valeurs de graphique** : valeur moyenne dans la période
- **Détails de métriques disponibles** : aucun

## Analyse des données de contenu
{: #anlz_metrics_payload}

Vous pouvez analyser le contenu d'évaluation envoyé à votre déploiement dans la plage de données sélectionnée en utilisant l'une des méthodes suivantes :

- En examinant les classes de prévision et la répartition de la confiance dans chaque classe
   
   ![graphique mappant la répartition de la prévision en confiance](images/by_confidence.png)
   
- En personnalisant le graphique (en faisant un choix parmi les fonctions, les classes de prévision et la confiance)
   
   ![graphique montrant la fonction de prévision pour le sexe par la fonction d'âge](images/by_custom_chart.png)

