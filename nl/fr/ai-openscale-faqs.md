---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: FAQs, frequently asked questions, questions

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Questions fréquentes
{: #wos-faqs}

Vous trouverez ici quelques-unes des questions les plus fréquemment posées par les utilisateurs d'{{site.data.keyword.aios_full}}.
{: shortdesc}

## Questions
{: #wos-faqs-questions}

- [Comment convertir une colonne de prévision d'un type de données entier vers un type de données catégoriel ?](#wos-faqs-convert-data-types)

### Comment convertir une colonne de prévision d'un type de données entier vers un type de données catégoriel ?
{: #wos-faqs-convert-data-types}

Lors de la configuration de la surveillance de l'équité pour un modèle,
la colonne de prévision n'autorise qu'une valeur numérique entière
même si le libellé de prévision est catégoriel.
Comment la configurer pour une fonction catégorielle (non entière) ?
Une conversion manuelle est-elle nécessaire ? 

Supposons que les données de formation aient comme libellés de classe “Prêt refusé” et “Prêt accordé”.
La valeur de prévision renvoyée par le noeud final d'évaluation WML a des valeurs comme “0.0”, “1.0", etc.
Le noeud final d'évaluation a également une colonne facultative qui contient la représentation texte de la prévision.
Par exemple, si prediction=1.0, la colonne predictionLabel pourrait avoir la valeur “Prêt accordé”.
Si une telle colonne est disponible,
lors de la configuration des résultats favorable et défavorable du modèle, vous pouvez spécifier les valeurs chaîne “Prêt accordé” et “Prêt refusé”.
Si une telle colonne n'est pas disponible, vous devez spécifier les valeurs entières/doubles 1.0 et 0.0 pour la classe favorable/défavorable.

WML a un concept de schéma de sortie qui définit le schéma de la sortie du noeud final d'évaluation WML et le rôle des différentes colonnes.
Les rôles servent à déterminer la colonne qui contient la valeur de prévision,
celle qui contient la probabilité de la prévision, et la valeur de libellé de classe, etc.
Le schéma de sortie est défini automatiquement pour les modèles créés avec le générateur de modèle.
Il peut également être défini avec le client Python WML.
Les utilisateurs peuvent utiliser le schéma de sortie pour définir une colonne contenant la représentation chaîne de la prévision.
Cela se fait en définissant le modeling_role de la colonne à 'decoded-target'.
La documentation du client Python WML est disponible à l'adresse : http://wml-api-pyclient-dev.mybluemix.net/#repository.
Recherchez “OUTPUT_DATA_SCHEMA” pour comprendre le schéma de sortie ; l'API à utiliser est l'API store_model qui accepte le schéma OUTPUT_DATA_SCHEMA en paramètre.



