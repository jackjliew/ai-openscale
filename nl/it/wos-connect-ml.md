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

# Registrazione payload per istanze di servizio non {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #cml-connect}

Se il modello AI è distribuito in un motore di machine learning diverso da {{site.data.keyword.pm_full}}, è necessario abilitare la registrazione del payload per il motore di machine learning esterno con un client Python.
{: shortdesc}

Consultare informazioni più complete nella [documentazione del client Python{{site.data.keyword.aios_short}} ](http://ai-openscale-python-client.mybluemix.net/){: external} e nei notebook di esempio del client Python {{site.data.keyword.aios_short}} che fanno parte dei [supporti didattici {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}.

## Prima di iniziare
{: #cml-prereq}

Sarà necessario che i dati di training del proprio modello siano disponibili in Db2 o {{site.data.keyword.cos_full}} per monitorare la distorsione per il modello. L'esplicabilità e l'accuratezza non sono supportate per le funzioni Python. Per ulteriori informazioni sui dati di training, consultare [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- Importare e inizializzare {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  È possibile trovare le credenziali seguendo i passi mostrati nell'argomento "[Creazione delle credenziali](/docs/services/ai-openscale?topic=ai-openscale-cred-create)".

- Creare un nome schema nel database PostgreSQL

- Impostare un datamart

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## Passi successivi
{: #cml-next}

- Per continuare con il client {{site.data.keyword.aios_short}}, consultare [Configurazione dei monitor Accuratezza e Qualità](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Per continuare con la libreria dei comandi Python, fare riferimento alla [documentazione del client Python](http://ai-openscale-python-client.mybluemix.net/){: external}.
