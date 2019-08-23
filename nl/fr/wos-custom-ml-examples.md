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

# Exemples de moteur d'apprentissage automatique personnalisé
{: #fmrk-workaround-cstmmlsengex}

Utilisez les exemples suivants pour configurer votre propre moteur d'apprentissage automatique personnalisé.
{: shortdesc}

## Python et Flask
{: #fmrk-workaround-pandflask}

L'[exemple de moteur d'apprentissage automatique personnalisé
publié sur git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)
utilise Python et Flask pour servir le modèle scikit-learn.

Le [fichier README](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix) explique
comment déployer l'application en local pour des tests ainsi que comme application cf sur IBM Cloud. L'implémentation des points d'extrémité d'API REST se trouve dans le
[fichier app.py](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py).

## Node.js
{: #fmrk-workaround-nodejs}

Vous trouverez également un exemple de moteur d'apprentissage automatique personnalisé
écrit en [Node.js ici](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs).

## Schéma de code end2end
{: #fmrk-workaround-e2ecode}

[Schéma de code](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale)
présentant un exemple end2end de déploiement de moteur personnalisé et d'intégration à {{site.data.keyword.aios_short}}.

