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

# Présentation des métriques d'équité
{: #anlz_metrics_fairness}

Utilisez la surveillance de l'équité de {{site.data.keyword.aios_full}}
pour déterminer si les résultats produits par votre modèle sont équitables ou non pour le groupe surveillé.
Lorsque la surveillance de l'équité est activée, elle génère un ensemble de métriques toutes les heures par défaut. Vous pouvez générer ces métriques sur demande en cliquant sur le bouton **Vérifier la qualité maintenant** ou en utilisant le client Python.
{: shortdesc}

{{site.data.keyword.aios_short}} détecte automatiquement si un modèle comporte des attributs protégés connus.
Lorsqu'il détecte ces attributs, il recommande automatiquement de configurer un moniteur de biais pour chaque attribut présent,
pour garantir le suivi du biais en production sur ces attributs potentiellement sensibles. 

Actuellement, {{site.data.keyword.aios_short}} détecte et recommande des moniteurs pour les attributs protégés suivants : 

- sexe
- ethnicité
- état matrimonial
- âge
- code postal

En plus de détecter les attributs protégés, {{site.data.keyword.aios_short}} recommande
les valeurs dans chaque attribut qui doivent être définies comme valeurs surveillées et valeurs de référence.
Ainsi, par exemple, {{site.data.keyword.aios_short}} recommande de configurer le moniteur de biais dans l'attribut "Sex"
en définissant "Woman" et "Non-Binary" comme valeurs surveillées, et "Male" comme valeur de référence.
Si vous voulez apporter des modifications par rapport aux recommandations, vous pouvez éditer celles-ci via le panneau de configuration du biais. 

Les moniteurs de biais recommandés accélèrent la configuration et garantissent le contrôle de vos modèles d'IA quant à l'équité par rapport aux attributs sensibles.
Les organismes de réglementation commencent à regarder de plus près le biais algorithmique
et il devient essentiel pour les organisations de bien comprendre le fonctionnement de leurs modèles et s'ils donnent des résultats inéquitables pour certains groupes. 

Les métriques d'équité sont calculées en fonction des informations suivantes :

- données de contenu d'évaluation.

En vue d'une surveillance adéquate, toutes les demandes d'évaluation doivent être consignées également dans {{site.data.keyword.aios_short}}. La journalisation des données de contenu est automatisée pour les moteurs {{site.data.keyword.pm_full}}.

Pour les autres moteurs d'apprentissage automatique, les données de contenu peuvent être fournies à l'aide du client Python ou de l'API REST.

Pour les moteurs d'apprentissage automatique autres que {{site.data.keyword.pm_full}}, la surveillance de l'équité crée des demandes d'évaluation supplémentaires sur le déploiement surveillé.
{: note}

Vous pouvez examiner la valeur de toutes les métriques au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique des métriques d'équité montrant une dérive au-dessous du seuil défini](images/fairness_metrics_001.png)

Vous pouvez consulter les détails connexes, tels que des résultats favorables et défavorables :

![détails de l'équité](images/fairness_metrics_002.png)

Vous pouvez consulter les transactions détaillées :

![graphique de l'équité montrant une liste de transactions](images/fairness_metrics_003.png)

Vous pouvez consulter le noeud final d'évaluation débiaisée recommandé :

![détails du noeud final d'évaluation débiaisée](images/fairness_metrics_004.png)

### Métriques d'équité prises en charge
{: #anlz_metrics_supfairmets}

Les métriques d'équité suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

- [Equité d'un groupe](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

Les attributs protégés suivants sont pris en charge par {{site.data.keyword.aios_short}} : 

- [sexe](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [ethnicité](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [état matrimonial](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [âge](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [code postal](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### Détails d'équité pris en charge
{: #anlz_metrics_supfairdets}

Les détails suivants des métriques d'équité sont pris en charge par {{site.data.keyword.aios_short}} :

- Pourcentages favorables pour chacun des groupes
- Moyennes d'équité pour tous les groupes d'équité

```
                          (% de résultats favorables dans le groupe surveillé)
Taux d'impact disparate = ____________________________________________________
                          (% de résultats favorables dans le groupe de référence)
```

- Distribution des données pour chacun des groupes surveillés
- Distribution des données de contenu
