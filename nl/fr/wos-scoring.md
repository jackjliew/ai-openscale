---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# Envoi d'une demande d'évaluation
{: #cdb-score}

Pour configurer les moniteurs, {{site.data.keyword.aios_short}} requiert que vous envoyiez un contenu utile d'évaluation,
afin de commencer à journaliser les données qui seront surveillées.

- Les modèles déployés dans {{site.data.keyword.pm_full}} sont envoyés automatiquement à {{site.data.keyword.aios_short}}.
Pour les demandes d'évaluation envoyées automatiquement, vous n'avez pas besoin d'effectuer cette tâche et aucun fragment de code n'apparaît.
- Pour les autres moteurs d'apprentissage automatique, comme Microsoft Azure, Amazon SageMaker ou un moteur d'apprentissage automatique personnalisé,
le contenu utile d'évaluation doit être envoyé avec l'API de journalisation de contenu utile.
Pour cela, vous devez utiliser un fragment de code au format cURL ou Python, que vous pouvez extraire de la page Journalisation du contenu utile.
Pour plus d'informations, voir
[Journalisation du contenu utile pour les instances de service non-{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

## Procédure pour la journalisation du contenu utile
{: #cdb-score-apisteps}

1. Dans le tableau de bord de {{site.data.keyword.aios_short}}, cliquez sur un carreau du déploiement.
2. Cliquez sur **Configurer les moniteurs**. 
3. Dans le volet de navigation, cliquez sur **Journalisation du contenu utile**.
2. Choisissez entre le code `cURL` et le code `Python` en cliquant sur l'onglet `cURL` ou `Python`.
3. Cliquez sur **Copier dans le presse-papiers** et collez pour journaliser les données de demande et de réponse du déploiement de modèle. Pour plus d'informations, consultez
[Journalisation du contenu utile pour les instances de service non-{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Les zones et les valeurs des fragments de code doivent être remplacées par vos valeurs réelles, car les valeurs fournies ne sont que des exemples.
{: important}

![Sélection de la base de données](images/config-send-scoring.png)

Une fois que vous avez exécuté votre journalisation du contenu utile, une coche apparaît dans la colonne **Prêt à surveiller** pour le déploiement sélectionné. Cliquez sur **Configurer les moniteurs** pour continuer.

## Comprendre le nombre de demandes d'évaluation
{: #cdb-score-capacity}

Les demandes d'évaluation font partie intégrante du traitement de {{site.data.keyword.aios_short}}. Chaque enregistrement de transaction que vous envoyez au modèle à évaluer génère un traitement supplémentaire
permettant au service {{site.data.keyword.aios_short}} d'effectuer la perturbation et de créer des explications.

- Pour les modèles tabulaires, de texte ou d'image, la demande de base suivante génère des points de données :

   -ai-open-scale-ibm-aios-scheduling  | 1 | Service de planification - demande d'évaluation génère 5000 points de données.

- Pour les modèles de classification tabulaire uniquement, d'autres demandes d'évaluation sont faites pour une explication contrastive. Les demandes suivantes sont ajoutées à la demande de base précédente :

   - 100 demandes d'évaluation génère 51 points de données supplémentaires par demande.
   - 101 demandes d'évaluation génère sai-open-scale-ibm-aios-scheduling  | 1 | Service de planification - point de données supplémentaire par demande.


## Etapes suivantes
{: #cdb-score-next-steps-scoringreq}

[Configurer les moniteurs](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config).
