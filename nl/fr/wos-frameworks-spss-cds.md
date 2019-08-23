---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: supported frameworks, models, model types, limitations, limits, spss, c&ds

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Infrastructures IBM SPSS C&DS
{: #frmwrks-spss}

Vous pouvez utiliser IBM SPSS C&DS pour effectuer une journalisation du contenu utile et des retours,
et pour mesurer l'exactitude de performance, la détection de biais à l'exécution, l'explicabilité et la fonction de débiaisement automatique dans {{site.data.keyword.aios_full}}.

Il est prévu que {{site.data.keyword.aios_full}} supporte pleinement les infrastructures IBM SPSS C&DS (Collaboration and Deployment Services) suivantes :
{: shortdesc}

Actuellement, le support est limité à {{site.data.keyword.wos4d_full}}.
{: note}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| SPSS | Classification | Structure |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

Si l'`ID de déploiement` d'un abonnement contient un trait de soulignement,
l'exactitude débiaisée qui est normalement affichée dans l'onglet débiaisé des métriques d'équité n'apparaîtra pas.
{: note}


## Prise en charge de l'explicabilité pour les infrastructures IBM SPSS Collaboration and Deployment Services (C&DS)
{: #frmwrks-spss-exp-supp}

- L'explicabilité est prise en charge pour les modèles binaires et pour les modèles multi-classes SPSS qui renvoient une probabilité pour chacune des classes. 
- L'explicabilité n'est pas prise en charge pour les modèles multi-classes SPSS qui ne renvoient que la probabilité de la classe gagnante.



