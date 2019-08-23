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

# Ejemplos de motor de aprendizaje automático personalizado
{: #fmrk-workaround-cstmmlsengex}

Utilice los ejemplos siguientes para configurar su propio motor de aprendizaje automático personalizado.
{: shortdesc}

## Python y flask
{: #fmrk-workaround-pandflask}

El [ejemplo de motor ML
personalizado publicado en git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) utiliza python y flask para servir al modelo scikit-learn.

El [archivo README](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)
describe cómo se puede desplegar la aplicación localmente para fines de pruebas así como la aplicación cf en IBM Cloud. La implementación de puntos finales de API REST se puede encontrar en
[app.py file](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py).

## Node.js
{: #fmrk-workaround-nodejs}

También puede encontrar el ejemplo del motor de aprendizaje automático personalizado escrito en
[Node.js aquí](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs).

## Patrón de código End2end
{: #fmrk-workaround-e2ecode}

[Patrón de código](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale) que muestra un
ejemplo end2end de despliegue de motor personalizado e integración con {{site.data.keyword.aios_short}}.

