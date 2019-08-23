---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Générateur de graphique ![étiquette bêta](images/beta.png)
{: #chart_builder}

Le générateur de graphique de {{site.data.keyword.aios_short}} vous permet de créer des visualisations personnalisées
pour mieux comprendre les prévisions et les entrées d'un modèle à l'exécution. Il donne la possibilité de visualiser la sortie de la prévision du modèle pour les caractéristiques ou plages de données importantes pour l'entreprise. Il aide à découvrir les nouvelles tendances des données, qui peuvent inviter les équipes métier et sciences des données à envisager des modifications du modèle d'IA. 
{: shortdesc}

Par exemple, si vous êtes familiarisé avec notre modèle de risque de crédit des tutoriels,
vous pouvez voir la séparation dans les classes prévues pour différentes plages de l'attribut Credit History. 

   ![graphique montrant la prévision du sexe par la caractéristique d'âge](images/by_custom_chart.png)
      
   Vous pouvez également voir si le modèle est fiable, lors de la prévision pour ces plages d'historique de crédit. Vous pouvez analyser le contenu utile d'évaluation envoyé à votre déploiement dans la plage de données sélectionnée
par un graphique personnalisé (en faisant un choix parmi les caractéristiques, les classes de prévision et la confiance).

   ![graphique montrant la prévision du sexe par la caractéristique d'âge](images/by_custom_chart002.png)
   
