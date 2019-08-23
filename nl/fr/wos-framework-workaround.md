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

# Intégration de moteurs d'apprentissage automatique tiers à {{site.data.keyword.aios_short}}
{: #fmrk-workaround}

{{site.data.keyword.aios_full}} peut s'intégrer avec des moteurs d'apprentissage automatique externes tels que Microsoft Azure ML Studio, Microsoft Azure ML Service et Amazon SageMaker.
{: shortdesc}

Vous pouvez intégrer {{site.data.keyword.aios_short}} et des moteurs tiers de différentes manières :

- Niveau liaison de moteur : possibilité de répertorier les déploiements et d'obtenir leurs détails.
  
- Niveau abonnement de déploiement : {{site.data.keyword.aios_short}}
doit pouvoir évaluer le déploiement abonné dans le format requis,
comme le format {{site.data.keyword.pm_full}}, et recevoir la sortie dans le même format compatible. Il doit être configuré pour traiter à la fois les formats d'entrée et de sortie.
   

- Journalisation du contenu utile : chaque entrée et sortie du modèle déployé déclenchée par l'application d'un utilisateur doit être stockée dans un magasin de contenu utile. Le format des enregistrements de contenu utile suit la même spécification qu'indiqué dans la section précédente sur les niveaux abonnement de déploiement.
   
   {{site.data.keyword.aios_short}} utilise ces enregistrements pour calculer le biais, les explications et autres. Il n'est pas possible pour {{site.data.keyword.aios_short}} de stocker automatiquement les transactions exécutées sur le site de l'utilisateur,
qui se trouve en dehors du système {{site.data.keyword.aios_short}}. C'est l'une des manières dont {{site.data.keyword.aios_short}} protège les informations propriétaire. Utilisez l'API REST ou le SDK Python de {{site.data.keyword.aios_short}} pour travailler sur des données sécurisées.
   
## Etapes pour implémenter cette solution
{: #fmrk-workaround-steps}

1. [Découvrir les moteurs d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine).
2. [Configurer la journalisation du contenu utile](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload).
3. [Automatiser la journalisation du contenu utile](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg).
4. Configurez un moteur d'apprentissage automatique personnalisé
en utilisant un de ces [exemples de moteur d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).

