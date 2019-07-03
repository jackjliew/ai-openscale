---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: databases, connections, scoring, requests, schema, REST API, API

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

# Esempi di motori di machine learning personalizzati
{: #fmrk-workaround-cstmmlsengex}

Utilizzare i seguenti esempi per configurare il proprio motore di machine learning personalizzato.
{: shortdesc}

## Python e flask
{: #fmrk-workaround-pandflask}

L'[esempio di motore ML personalizzato pubblicato su git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) utilizza pitone e flask per servire il modello scikit-learn.

Il [file README](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) descrive come l'app può essere distribuita localmente per scopi di test così come per la configurazione dell'applicazione su IBM Cloud. L'implementazione degli endpoint API REST può essere trovata nel [file app.py](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py).

## Node.js
{: #fmrk-workaround-nodejs}

È anche possibile trovare l'esempio del motore di machine learning personalizzato scritto in [Node.js qui](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs).

## Modello di codice end2end
{: #fmrk-workaround-e2ecode}

[Modello di codice](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale) che mostra l'esempio end2end della distribuzione del motore personalizzato e l'integrazione con {{site.data.keyword.aios_short}}.

