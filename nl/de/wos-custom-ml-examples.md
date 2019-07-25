---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Angepasste Machine Learning-Engine - Beispiele
{: #fmrk-workaround-cstmmlsengex}

Orientieren Sie sich an den folgenden Beispielen, um Ihre eigene angepasste Machine Learning-Engine einzurichten.
{: shortdesc}

## Python und Flask
{: #fmrk-workaround-pandflask}

Das [auf Git veröffentlichte Beispiel einer angepassten Machine Learning-Engine](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) verwendet Python und Flask, um das Modell 'scikit-learn' zu bedienen.

In der [README-Datei](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) enthält eine Beschreibung zur lokalen Bereitstellung der App zu Testzwecken sowie als cf-Anwendung unter IBM Cloud. Die Implementierung von REST-API-Endpunkten finden Sie in der [app.py-Datei](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py).

## Node.js
{: #fmrk-workaround-nodejs}

Ein Beispiel für eine JSON geschriebene angepasste Machine Learning-Engine finden Sie im [Node.js-Beispiel](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs).

## End-to-End-Codemuster
{: #fmrk-workaround-e2ecode}

Das [Codemuster](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale) veranschaulicht anhand eines End-to-End-Beispiels die durchgängige Bereitstellung und Integration einer angepassten Machine Learning-Engine mit {{site.data.keyword.aios_short}}.

