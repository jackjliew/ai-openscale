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

# Présentation des métriques de performances ![étiquette bêta](images/beta.png)
{: #anlz_metrics_performance}

Utilisez la surveillance des performances pour connaître la vitesse des enregistrements de données traités par votre déploiement. Vous pouvez activer la surveillance des performances lorsque vous sélectionnez le déploiement qui doit être suivi et surveillé par {{site.data.keyword.aios_short}}.
{: shortdesc}

Les métriques de performances sont calculées en fonction des informations suivantes :

- données de contenu utile d'évaluation

En vue d'une surveillance adéquate, toutes les demandes d'évaluation doivent être consignées également dans {{site.data.keyword.aios_short}}. La journalisation des données de contenu utile est automatisée pour les moteurs {{site.data.keyword.pm_full}}. Pour les autres moteurs d'apprentissage automatique, les données de contenu utile peuvent être fournies à l'aide du client Python ou de l'API REST. La surveillance des performances ne crée pas de demandes d'évaluation supplémentaires sur le déploiement surveillé.

Vous pouvez examiner la valeur des métriques de performances au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique de performances](images/performance_metrics_001.png)

## Métriques de performances prises en charge
{: #anlz_metrics_performance_supp_quality_mets}

Les métriques de performances suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

- [Débit](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
