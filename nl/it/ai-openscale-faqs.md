---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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
{:faq: data-hd-content-type='faq'}

# FAQ
{: #wos-faqs}

Qui è possibile trovare alcune delle domande più frequenti effettuate dagli utenti di {{site.data.keyword.aios_full}}.
{: shortdesc}

## Domande
{: #wos-faqs-questions}

- [Come posso convertire una colonna di previsione da un tipo di dati numerici a un tipo di dati categoriali?](#wos-faqs-convert-data-types)
- [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](#trainingdata)

### Come posso convertire una colonna di previsione da un tipo di dati numerici a un tipo di dati categoriali?
{: #wos-faqs-convert-data-types}

Quando si configura il monitoraggio della correttezza per un modello, la colonna di previsione consente solo i valori numerici anche se l'etichetta di previsione è categoriale. Come la configuro per la funzione categoriale (cioé non numerica)? È richiesta una conversione manuale? 

I dati di training possono avere etichette classe “Loan Denied”, “Loan Granted”. Il valore di previsione restituito dall'endpoint di calcolo del punteggio WML ha valori "0.0", "1.0", ecc. L'endpoint di calcolo del punteggio ha anche una colonna facoltativa che contiene la rappresentazione testuale della previsione. Ad esempio, se prediction=1.0, la colonna predictionLabel può avere un valore "Loan Granted". Se tale colonna è disponibile, mentre si configura il risultato favorevole e non favorevole per il modello, è possibile specificare i valori stringa "Loan Granted" e "Loan Denied". Se tale colonna non è disponibile, è necessario specificare i valori numeri interi/doppi 1.0, 0.0 per la classe favorevole/non favorevole.

WML ha un concetto di schema di output che definisce lo schema dell'output dell'endpoint di calcolo del punteggio WML e il ruolo per le diverse colonne. I ruoli vengono utilizzati per identificare le colonne che contengono i valori di previsione, quelle con la probabilità previsionale, i valori etichetta classe ecc. Lo schema di output è impostato automaticamente per i modelli creati tramite il builder di modelli. Può anche essere impostato utilizzando il client WML python. Gli utenti possono utilizzare lo schema di output per definire una colonna che contiene la rappresentazione stringa della previsione. Ciò si realizza impostando modeling_role per la colonna su 'decoded-target'. La documentazione per il client WML python è disponibile all'indirizzo: http://wml-api-pyclient-dev.mybluemix.net/#repository. Cercare "OUTPUT_DATA_SCHEMA" per conoscere lo schema di output e l'API da utilizzare, cioé l'API store_model che accetta OUTPUT_DATA_SCHEMA come parametro.

### Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?
{: #trainingdata}

È necessario fornire l'accesso {{site.data.keyword.aios_short}} ai dati di training memorizzati in Db2 o {{site.data.keyword.cos_full_notm}}, oppure è necessario eseguire un notebook che possa accedere ai dati di training. {{site.data.keyword.aios_short}} ha bisogno dell'accesso ai dati di training per i seguenti motivi:

- Generare spiegazioni contrastanti: per creare spiegazioni è necessario accedere alle statistiche, come il valore mediano, la deviazione standard e i valori distinti dai dati di training.
- Visualizzare le statistiche dei dati di training: per compilare la pagina dei dettagli di distorsione, {{site.data.keyword.aios_short}} deve avere dati di training da cui generare le statistiche.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

Nell'approccio basato sul notebook, è previsto che l'utente carichi le statistiche e altre informazioni durante la configurazione di una distribuzione in {{site.data.keyword.aios_short}}. Ciò implica che {{site.data.keyword.aios_short}} non avrà più accesso ai dati di training esterni al notebook, che viene eseguito nel proprio ambiente. Ha solo accesso alle informazioni caricate durante la configurazione.


