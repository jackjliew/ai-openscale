---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Formattazione e caricamento dei dati di feedback in {{site.data.keyword.aios_short}}
{: #fmt-upld-fdbk-data}

I dati di feedback sono essenziali per gestire un modello senza distorsione. È necessario caricare i dati di feedback nel servizio {{site.data.keyword.aios_full}} regolarmente per garantire che il modello prenda in considerazione i dati aggiornati che possono indicare modifiche nel contesto dell'applicazione predittiva. Con un loop di feedback, il sistema impara continuamente, monitorando l'efficacia delle previsioni e rieseguendo il training quando necessario. Il monitoraggio e l'utilizzo del feedback risultante sono alla base del machine learning. Le seguenti informazioni sono intese a guidare l'utente nella formattazione e nel caricamento dei dati di feedback.
(: shortdesc)

## Formattazione dei dati di feedback
{: #fmt-upld-fdbk-data-fmt}

Per leggere correttamente i dati di feedback, devono essere formattati in modo appropriato. Il servizio {{site.data.keyword.aios_short}} accetta i seguenti formati:

- Formati file CSV, che è possibile caricare utilizzando la IU o l'API REST
- Formati file JSON, che possono essere caricati utilizzando solo l'API REST

Questi formati di file sono definiti da uno schema, `schema_dati_training`, disponibile nei dettagli di sottoscrizione. Per visualizzare lo `schema_dati_training`, eseguire il seguente comando utilizzando l'API Python:

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

Per confrontare lo schema dei dati di training con lo schema di feedback, è possibile voler visualizzare anche lo schema di feedback. Per visualizzare lo schema di feedback, eseguire il seguente comando utilizzando l'API Python:

```
subscription.feedback_logging.print_table_schema()
```


### Formato CSV
{: #fmt-upld-fdbk-data-fmt-csv}

Generalmente, per un file CSV si forniscono i dati in colonne e righe con una riga per i nomi colonna. 

Generalmente, non sono richieste le virgolette quando i nomi colonna sono tutti in maiuscolo, ciò li rende non sensibili al maiuscolo/minuscolo per Db2, tuttavia per altri database e nel caso in cui i caratteri dei nomi sono misti, il maiuscolo/minuscolo deve corrispondere.
Se il file contiene nomi colonna, le colonne non devono necessariamente corrispondere all'ordine della tabella, tuttavia se il file non ha nomi colonna, è necessario mettere in corrispondenza con l'ordine della tabella. È possibile avere colonne che non sono nei dati di training originali. Tali colonne vengono ignorate durante l'elaborazione. 


### Formato JSON
{: #fmt-upld-fdbk-data-fmt-json}

Il formato JSON consiste di una raccolta di ogegtti con campi corrispondenti ai nomi colonna. 

