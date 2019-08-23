---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Moteur d'apprentissage automatique personnalisé
{: #fmrk-workaround-customengine}

Un moteur d'apprentissage automatique personnalisé fournit l'infrastructure et l'hébergement pour les modèles et les applications web d'apprentissage automatique. Pour être supporté par {{site.data.keyword.aios_short}}, il doit respecter les exigences suivantes :

- Exposer deux types de points d'extrémité d'API REST :

   * point d'extrémité de reconnaissance (liste GET des déploiements et détails)
   * points d'extrémité d'évaluation (évaluation en ligne et en temps réel)

- Tous les points d'extrémité doivent être compatibles avec la spécification swagger pour être supportés.

- Le contenu utile d'entrée et la sortie du déploiement doivent être conformes au format de fichier JSON décrit dans la spécification.

Actuellement, seuls les formats `BasicAuth` et `none` sont supportés.
{: Note}

L'exemple suivant présente la spécification des points d'extrémité d'API REST :

![Affichage de la spécification des points d'extrémité d'API REST du document swagger](images/wosdeployments.png)


L'exemple suivant montre le format d'un contenu utile d'entrée :

![Exemple de contenu utile d'entrée](images/wosinputdata.png)


## Dans quels cas faut-il utiliser un moteur d'apprentissage automatique personnalisé ?
{: #fmrk-workaround-enging-choice}

L'utilisation d'un moteur d'apprentissage automatique personnalisé est recommandée dans les situations suivantes :

- Vous n'utilisez aucun produit tout prêt pour vos modèles d'apprentissage automatique. Vous venez de développer votre propre système. {{site.data.keyword.aios_short}} n'offre, et n'offrira, aucune prise en charge directe dans ce cas.
- Le moteur tiers que vous utilisez n'est pas encore supporté par {{site.data.keyword.aios_short}}. Dans ce cas, vous pouvez envisager de développer un moteur d'apprentissage automatique personnalisé qui encapsulera vos déploiements initiaux ou natifs.

## Etapes suivantes
{: #fmrk-workaround-nxt-steps-over}

Implémentez votre propre solution en utilisant l'un de ces
[Exemples d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).
