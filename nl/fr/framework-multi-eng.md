---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: multiple engines, non-Watson, machine learning, frameworks, provision

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

# Possibilité de moteurs d'apprentissage automatique multiples
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} peut prendre en charge plusieurs moteurs d'apprentissage automatique
dans une même instance à condition que la mise à disposition soit effectuée via le
[SDK Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).
{: shortdesc}

Lorsque vous avez configuré {{site.data.keyword.aios_short}} au départ,
vous avez peut-être utilisé l'interface utilisateur ou l'option de configuration automatisée
pour mettre à disposition votre premier moteur d'apprentissage automatique. L'ajout d'autres moteurs d'apprentissage automatique nécessite d'utiliser le SDK Python. Plus précisément, l'ajout de moteurs d'apprentissage automatique à {{site.data.keyword.aios_short}} se fait avec la méthode `client.data_mart.bindings.add`.

## Méthodes de liaison
{: #fmrk-workaround-multmleng-binding}

Vous pouvez lier plusieurs moteurs d'apprentissage automatique à {{site.data.keyword.aios_short}}
en utilisant la méthode `client.data_mart.bindings.add` de l'API Python. 

- Pour lier le moteur d'apprentissage automatique {{site.data.keyword.pm_full}}, exécutez la commande suivante :

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- Pour lier le moteur d'apprentissage automatique Azure ML Studio, exécutez la commande suivante :

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- Pour lier le moteur d'apprentissage automatique AWS Sagemaker, exécutez la commande suivante :

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

Pour afficher la liste de toutes les liaisons, exécutez la méthode `list` :

`    client.data_mart.bindings.list()
    `


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | Mon moteur Azure ML Studio | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | Instance WML | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | Mon moteur AWS SageMaker | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tableau 1. Services liés" caption-side="top"}


Pour des informations sur les différents moteurs d'apprentissage automatique, voir les rubriques suivantes :

- [Lier votre moteur d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).
- [Lier votre moteur d'apprentissage automatique Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [Lier votre moteur d'apprentissage automatique Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


Pour un exemple de bloc-notes fonctionnel, voir
[les exemples de bloc-note {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

