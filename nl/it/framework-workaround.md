---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Integrazione di motori di ML learning di terze parti con {{site.data.keyword.aios_short}}
{: #fmrk-workaround}

{{site.data.keyword.aios_full}} si integra con motori esterni per il servizio di machine learning, come Microsoft Azure ML Studio e Amazon SageMaker.
{: shortdesc}

È possibile integrare {{site.data.keyword.aios_short}} con motori di terze parti nei seguenti modi:

- Livello collegamento motore: la possibilità di elencare le distribuzioni e ottenere i dettagli di distribuzione. 
  
- Livello sottoscrizione distribuzione: {{site.data.keyword.aios_short}} deve essere in grado di calcolare il punteggio della  distribuzione sottoscritta nel formato richiesto, come il formato {{site.data.keyword.pm_full}}, e ricevere l'output nello stesso formato compatibile. {{site.data.keyword.aios_short}} deve essere configurato per elaborare sia i formati di input che di output.
   

- Registrazione payload: ogni input e output per il modello distribuito attivato dall'applicazione di un utente deve essere memorizzato in un archivio payload. Il formato dei record di payload segue la stessa specifica di cui si è parlato nella sezione precedente sui livelli di sottoscrizione di distribuzione.
   
   {{site.data.keyword.aios_short}} utilizza questi record per calcolare la distorsione, l'esplicabilità e altro. Non è possibile per {{site.data.keyword.aios_short}} memorizzare automaticamente le transazioni eseguite sul sito dell'utente, che si trova al di fuori del sistema {{site.data.keyword.aios_short}}. Questo è uno dei modi in cui {{site.data.keyword.aios_short}} protegge le informazioni di proprietà. Utilizzare l'API Rest di {{site.data.keyword.aios_short}} o l'SDK Python per gestire i dati sicuri.
   
## Procedura per implementare questa soluzione
{: #fmrk-workaround-steps}

1. [Informazioni sui motori di machine learning personalizzati](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine).
2. [Configurare la registrazione payload](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload).
3. [Automatizzare la registrazione payload](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg).
4. Configurare un motore di machine learning personalizzato utilizzando uno di questi [Esempi di motori di machine learning personalizzati](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).

