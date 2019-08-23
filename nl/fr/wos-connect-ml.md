---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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

# Journalisation du contenu utile pour les instances de service non-{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #cml-connect}

Si votre modèle d'AI est déployé dans un moteur d'apprentissage automatique autre que {{site.data.keyword.pm_full}},
vous devez activer la journalisation du contenu utile pour le moteur d'apprentissage automatique externe avec un client Python.
{: shortdesc}

Pour une information plus complète, consultez la
[documentation du client Python {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external},
et les exemples de bloc-notes du client Python {{site.data.keyword.aios_short}}
des [tutoriels {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}.

## Avant de commencer
{: #cml-prereq}

Vous devrez avoir les données de formation de votre modèle disponibles dans Db2 ou {{site.data.keyword.cos_full}} pour surveiller son biais. L'explicabilité et l'exactitude ne sont pas prises en charge pour les fonctions Python. Pour plus d'informations sur les données de formation, consultez [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- Importer et lancer {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  Vous trouverez les identifiants en procédant comme indiqué à la rubrique
"[Création d'identifiants](/docs/services/ai-openscale?topic=ai-openscale-cred-create)".

- Créer un nom de schéma dans votre base de données PostgreSQL

- Configurer un magasin de données

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## Etapes suivantes
{: #cml-next}

- Pour continuer avec le client {{site.data.keyword.aios_short}}, consultez [Configuration du moniteur d'exactitude ou de qualité](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Pour continuer avec la bibliothèque de commandes Python, consultez la [documentation du client Python](http://ai-openscale-python-client.mybluemix.net/){: external}.
