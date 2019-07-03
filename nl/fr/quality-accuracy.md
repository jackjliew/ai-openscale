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

# Exactitude
{: #accuracy-opener}

L'exactitude est une mesure de la proportion de prévisions correctes d'un modèle.
{: shortdesc}

## L'exactitude en bref
{: #anlz_metrics_supqualdets_acc}

- **Description** : proportion des prévisions correctes
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** :
   - **Tendance à la hausse** : une tendance à la hausse indique que la métrique s'améliore. Cela signifie que le recyclage des modèles est effectif.
   - **Tendance à la baisse** : une tendance à la baisse indique que la métrique se dégrade. Les données de commentaires deviennent nettement différentes des données de formation.
   - **Variation erratique ou irrégulière** : une variation erratique ou irrégulière indique que les données de commentaires ne sont pas cohérentes d'une évaluation à l'autre. Augmentez la taille d'échantillon minimale pour le moniteur de qualité.
- **Types de problème** : classification binaire et classification multi-classes
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : matrice de confusion


## Comprendre l'exactitude
{: #acc-understand}

L'exactitude peut signifier différentes choses selon le type de l'algorithme :

- *Classification multi-classes* :
L'exactitude mesure le nombre de fois qu'une classe quelconque a été prévue correctement, normalisé par le nombre de points de données. Pour plus de détails, voir
[Multi-class classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external}
dans la documentation d'Apache Spark.

- *Classification binaire* :
Pour un algorithme de classification binaire, l'exactitude est mesurée comme la zone située sous une courbe ROC. Pour plus de détails, voir
[Binary classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external}
dans la documentation d'Apache Spark.

- *Régression* :
Les algorithmes de régression sont mesurés à l'aide du coefficient de détermination, ou R2. Pour plus de détails, voir
[Regression model evaluation](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external}
dans la documentation d'Apache Spark.

### Fonctionnement
{: #acc-works}

Vous devez ajouter des données de commentaires étiquetées manuellement via l'interface utilisateur {{site.data.keyword.aios_short}}
comme dans les exemples suivants,
avec un [client Python](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external} ou une
[API REST](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external}.

Reportez-vous aux [Infrastructures prises en charge](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)
pour connaître les limitations de la surveillance de l'exactitude.

### Exactitude débiaisée
{: #acc-debias-view}

Lorsqu'il y a des données pour, l'exactitude est calculée à la fois sur le modèle d'origine et sur le modèle débiaisé.
{{site.data.keyword.aios_full_notm}} calcule l'exactitude pour la sortie débiaisée et l'enregistre dans la table de journalisation de contenu
sous la forme d'une colonne additionnelle.

![affichage d'un modèle avec l'exactitude calculée à la fois pour le modèle d'origine et le modèle débiaisé.](images/debiased-accuracy.png)
