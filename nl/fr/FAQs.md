---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: FAQs, frequently asked questions, questions

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

# Questions fréquentes
{: #wos-faqs}

Vous trouverez ici quelques-unes des questions les plus fréquemment posées par les utilisateurs d'{{site.data.keyword.aios_full}}.
{: shortdesc}

## Questions
{: #wos-faqs-questions}

- [Qu'est-ce que {{site.data.keyword.aios_short}} ?](#faq-whatsa)
- [Comment est déterminé le prix de {{site.data.keyword.aios_short}} ?](#faq-pricing)
- [Existe-t-il un essai gratuit de {{site.data.keyword.aios_short}} ?](#faq-freetrial)
- [Tous mes modèles d'IA sont dans Azure. Puis-je utiliser le moteur d'apprentissage automatique Microsoft Azure avec {{site.data.keyword.aios_short}} ?](#faq-azure)
- [Tous mes modèles d'IA sont dans Amazon. Puis-je utiliser le moteur d'apprentissage automatique Amazon SageMaker avec {{site.data.keyword.aios_short}} ?](#faq-sagemaker)
- [{{site.data.keyword.aios_short}} est-il disponible sur IBM Cloud Pak for Data ?](#faq-icp)
- [Je veux exécuter {{site.data.keyword.aios_short}} sur mes propres serveurs. Quelle puissance de traitement dois-je lui allouer ?](#faq-sizing)
- [Comment convertir une colonne de prévision d'un type de données entier vers un type de données catégoriel ?](#wos-faqs-convert-data-types)
- [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](#trainingdata)

### Qu'est-ce que {{site.data.keyword.aios_short}}
{: #faq-whatsa}

Watson OpenScale suit et mesure les résultats de l'IA sur tout son cycle de vie,
et il l'adapte aux situations métier changeantes - pour des modèles créés et s'exécutant n'importe où.

[Voir la vidéo]().


### Comment est déterminé le prix de {{site.data.keyword.aios_short}} ?
{: #faq-pricing}




### Existe-t-il un essai gratuit de {{site.data.keyword.aios_short}} ?
{: #faq-freetrial}



### Tous mes modèles d'IA sont dans Azure. Puis-je utiliser le moteur d'apprentissage automatique Microsoft Azure avec {{site.data.keyword.aios_short}} ?
{: #faq-azure}



### Tous mes modèles d'IA sont dans Amazon. Puis-je utiliser le moteur d'apprentissage automatique Amazon SageMaker avec {{site.data.keyword.aios_short}} ?
{: #faq-sagemaker}



### {{site.data.keyword.aios_short}} est-il disponible sur IBM Cloud Pak for Data ?
{: #faq-icp}



### Je veux exécuter {{site.data.keyword.aios_short}} sur mes propres serveurs.
Quelle puissance de traitement dois-je lui allouer ?
{: #faq-sizing}





### Comment convertir une colonne de prévision d'un type de données entier vers un type de données catégoriel ?
{: #wos-faqs-convert-data-types}

Lors de la configuration de la surveillance de l'équité pour un modèle,
la colonne de prévision n'autorise qu'une valeur numérique entière
même si le libellé de prévision est catégoriel.
Comment la configurer pour une fonction catégorielle (non entière) ? Une conversion manuelle est-elle nécessaire ? 

Supposons que les données de formation aient comme libellés de classe “Prêt refusé” et “Prêt accordé”. La valeur de prévision renvoyée par le noeud final d'évaluation {{site.data.keyword.pm_full}} a des valeurs comme “0.0”, “1.0", etc.
Le noeud final d'évaluation a également une colonne facultative qui contient la représentation texte de la prévision. Par exemple, si prediction=1.0, la colonne predictionLabel pourrait avoir la valeur “Prêt accordé”. Si une telle colonne est disponible,
lors de la configuration des résultats favorable et défavorable du modèle, vous pouvez spécifier les valeurs chaîne “Prêt accordé” et “Prêt refusé”. Si une telle colonne n'est pas disponible, vous devez spécifier les valeurs entières/doubles 1.0 et 0.0 pour la classe favorable/défavorable.

{{site.data.keyword.pm_full}} a un concept de schéma de sortie qui définit le schéma de la sortie du noeud final d'évaluation {{site.data.keyword.pm_full}}
et le rôle des différentes colonnes. Les rôles servent à déterminer la colonne qui contient la valeur de prévision,
celle qui contient la probabilité de la prévision, et la valeur de libellé de classe, etc.
Le schéma de sortie est défini automatiquement pour les modèles créés avec le générateur de modèle. Il peut également être défini avec le client Python {{site.data.keyword.pm_full}}. Les utilisateurs peuvent utiliser le schéma de sortie pour définir une colonne contenant la représentation chaîne de la prévision. Cela se fait en définissant le modeling_role de la colonne à 'decoded-target'. La documentation du client Python {{site.data.keyword.pm_full}} est disponible à l'adresse : http://wml-api-pyclient-dev.mybluemix.net/#repository. Recherchez “OUTPUT_DATA_SCHEMA” pour comprendre le schéma de sortie ; l'API à utiliser est l'API store_model qui accepte le schéma OUTPUT_DATA_SCHEMA en paramètre.

### Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?
{: #trainingdata}

Vous devez permettre à {{site.data.keyword.aios_short}} d'accéder aux données de formation stockées dans Db2 ou {{site.data.keyword.cos_full_notm}}, ou vous devez exécuter un bloc-notes pouvant accéder aux données de formation. {{site.data.keyword.aios_short}} a besoin d'accéder à vos données de formation pour les raisons suivantes :

- Pour générer des explications contrastées : pour créer des explications, l'accès aux statistiques, telles que la valeur médiane, l'écart type et les valeurs distinctes des données de formation, est requis.
- Pour afficher les statistiques de données de formation : pour remplir la page des détails de biais, {{site.data.keyword.aios_short}} doit avoir des données de formation à partir desquelles générer des statistiques.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

Dans l'approche basée sur le bloc-notes, vous devez télécharger les statistiques et d'autres informations lors de la configuration d'un déploiement dans {{site.data.keyword.aios_short}}. Par conséquent, {{site.data.keyword.aios_short}} n'a plus accès aux données de formation en dehors du bloc-notes qui sont exécutées dans votre environnement. Il a accès uniquement aux informations téléchargées pendant la configuration.


