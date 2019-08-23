---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# Equité d'un groupe
{: #quality_group}

La métrique d'équité pour un groupe indique la propension du modèle à donner des résultats favorables à un groupe par rapport à un autre. Il peut s'agir de n'importe quel groupe, comme l'âge, le sexe ou la race.
{: shortdesc}

## L'équité pour un groupe en bref
{: #quality_group-glance}

- **Description** : la propension des modèles à donner des résultats favorables à un groupe sur un autre.
- **Seuils par défaut** : limite inférieure = 80 %
- **Recommandation par défaut** : point d'extrémité d'évaluation débiaisée que vous pouvez utiliser dans votre application métier pour recevoir des réponses débiaisées de votre modèle déployé.
- **Type de problème** : tous
- **Type de données** : structuré
- **Valeurs de graphique** : dernière valeur dans la période
- **Détails de métriques disponibles** : oui

## Attributs protégés
{: #quality_group-atts}

{{site.data.keyword.aios_short}} détecte automatiquement si un modèle comporte des attributs protégés connus. Lorsqu'il détecte ces attributs, il recommande automatiquement de configurer un moniteur de biais pour chaque attribut présent
pour garantir le suivi du biais en production sur ces attributs potentiellement sensibles. 

### sexe
{: #quality_group-sex}

{{site.data.keyword.aios_short}} recommande de configurer le moniteur de biais dans l'attribut **Sex**
en définissant `Woman` et `Non-Binary` comme valeurs surveillées, et `Male` comme valeur de référence. 

### ethnicité
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}} recommande de configurer le moniteur de biais dans l'attribut **ethnicity**
en définissant `White-caucasian` comme valeur de référence et les autres ethnicités comme valeurs surveillées.

### état matrimonial
{: #quality_group-marital}

{{site.data.keyword.aios_short}} recommande de configurer le moniteur de biais dans l'attribut **marital status**
en définissant `married` comme valeur de référence et `single` comme valeur surveillée.

### âge
{: #quality_group-age}

{{site.data.keyword.aios_short}} recommande de configurer le moniteur de biais dans l'attribut **age**
de telle manière que la plage d'âges produise un débiaisement permettant une action.

### code postal
{: #quality_group-zip}

{{site.data.keyword.aios_short}} recommande de configurer le moniteur de biais dans l'attribut **zip code**
de telle sorte que les différents codes postaux soient évalués.

## Interprétation de l'affichage
{: #quality_group-display}

### Score d'équité d'un groupe
{: #quality_group-display-fairnessscore}



### Groupes surveillés
{: #quality_group-display-monitoredgroups}



### Planning
{: #quality_group-display-schedule}

Le volet **Planning** affiche le 



