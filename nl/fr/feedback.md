---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: feedback data, data, feedback, models

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

# Formatage et téléchargement des données de commentaires dans {{site.data.keyword.aios_short}}
{: #fmt-upld-fdbk-data}

Les données de commentaires sont essentielles pour maintenir un modèle non biaisé.
Vous devez en télécharger régulièrement dans le service {{site.data.keyword.aios_full}}
pour que votre modèle prenne en compte les données à jour
pouvant indiquer des changements dans le contexte de votre application de prévision.
Avec une boucle de commentaires, le système apprend continuellement en surveillant l'efficacité des prévisions et par une reformation quand c'est nécessaire.
La surveillance et l'utilisation des commentaires résultants sont au coeur de l'apprentissage automatique.
Les informations qui suivent sont destinées à vous aider à formater et télécharger vos données de commentaires.
(: shortdesc)

## Formatage des données de commentaires
{: #fmt-upld-fdbk-data-fmt}

Pour que les données de commentaires puissent être lues correctement, elles doivent être formatées correctement.
Le service {{site.data.keyword.aios_short}} accepte les formats suivants :

- Les fichiers au format CSV, qui peuvent être téléchargés avec l'interface utilisateur ou l'API REST
- Les fichiers au format JSON, qui ne peuvent être téléchargés qu'avec l'API REST

Ces formats de fichier sont définis par un schéma, `training_data_schema`, qui est disponible dans les détails de l'abonnement.
Pour voir le schéma `training_data_schema`, exécutez la commande suivante avec l'API Python :

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

Pour comparer le schéma des données de formation à celui des commentaires,
il peut être utile d'afficher également ce dernier.
Pour cela, exécutez la commande suivante avec l'API Python :

```
subscription.feedback_logging.print_table_schema()
```


### Format CSV
{: #fmt-upld-fdbk-data-fmt-csv}

En général, pour un fichier CSV, vous fournissez les données en colonnes et en lignes avec une ligne pour le nom des colonnes.

Il n'y a généralement pas besoin de guillemets si les noms de colonne sont entièrement en majuscules,
ce qui les rend insensibles à la casse pour Db2 ;
en revanche, pour les autres bases de données ou si les noms de colonne comportent des minuscules, la casse doit correspondre.
Si le fichier contient des noms de colonne,
les colonnes n'ont pas nécessairement besoin d'être dans l'ordre de la table ;
en revanche, s'il n'y a pas de noms de colonne, l'ordre doit correspondre.
Il est possible d'avoir des colonnes qui ne figurent pas dans les données de formation d'origine.
Elles sont alors ignorées lors du traitement.


### Format JSON
{: #fmt-upld-fdbk-data-fmt-json}

Le format JSON consiste en un ensemble d'objets dont les zones correspondent aux noms des colonnes.

