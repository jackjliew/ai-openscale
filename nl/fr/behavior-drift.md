---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: drift, behavior, metrics

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

# Détection de dérive ![étiquette bêta](images/beta.png)
{: #behavior-drift-ovr}

Au fil du temps, l'importance et l'impact de certaines fonctions d'un modèle évoluent.
Cela affecte les applications associées et les résultats métier qui en découlent.
Avec la détection de dérive, {{site.data.keyword.aios_short}} offre un moyen de suivre les métriques et la performance d'un modèle,
et la manière dont le poids des fonctions évolue dans le temps.
La dérive est la dégradation des performances de prévision dans le temps en raison d'un contexte inconnu.
Au fur et à mesure que vos données évoluent, l'aptitude de votre modèle à faire des prévisions exactes peut se dégrader.
{{site.data.keyword.aios_short}} détecte la dérive et la met en évidence afin que vous puissiez effectuer des actions correctives.
{: shortdesc}

{{site.data.keyword.aios_short}} analyse toutes les transactions pour trouver celles qui contribuent à la dérive.
Il regroupe ensuite les enregistrements en fonction des valeurs d'attribut qui y ont contribué significativement.

## La dérive en bref
{: #behavior-drift-glance}




## Interprétation de l'affichage
{: #behavior-drift-display}

![graphique des métriques d'équité montrant une dérive au-dessous du seuil défini](images/fairness_metrics_001.png)


## Calculs
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} calcule la dérive 
