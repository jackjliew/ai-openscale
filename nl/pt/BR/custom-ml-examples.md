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

# Exemplos do mecanismo de aprendizado de máquina customizado
{: #fmrk-workaround-cstmmlsengex}

Use os exemplos a seguir para configurar seu próprio mecanismo de aprendizado de máquina customizado.
{: shortdesc}

## Python e Flask
{: #fmrk-workaround-pandflask}

O [exemplo de Mecanismo de ML customizado publicado no git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) está usando Python e Flask para entregar o modelo scikit-learn.

O [arquivo LEIA-ME](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) descreve como o app pode ser implementado localmente para propósitos de teste, bem como para o aplicativo cf no IBM Cloud. A implementação de terminais da API de REST pode ser localizada no [arquivo app.py](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py).

## Node.js
{: #fmrk-workaround-nodejs}

Também é possível localizar um exemplo de mecanismo de aprendizado de máquina customizado gravado no [Node.js aqui](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs).

## Padrão de código End2end
{: #fmrk-workaround-e2ecode}

[Padrão de código](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale) mostrando o exemplo de end2end da implementação e integração do mecanismo customizado com o {{site.data.keyword.aios_short}}.

