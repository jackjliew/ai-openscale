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

# Supporto per più motori di machine learning
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} supporta più motori di machine learning all'interno di una singola istanza a condizione che il provisioning venga eseguito tramite [l'SDK Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).
{: shortdesc}

Quando si configura per la prima volta {{site.data.keyword.aios_short}}, è possibile utilizzare l'interfaccia utente o l'opzione di configurazione automatizzata per eseguire il provisioning del primo motore di machine learning. L'aggiunta di motori di machine learning richiede l'utilizzo dell'SDK Python. Nello specifico, è possibile aggiungere motori di machine learning a {{site.data.keyword.aios_short}} utilizzando il metodo `client.data_mart.bindings.add`.

## Metodi di collegamento
{: #fmrk-workaround-multmleng-binding}

È possibile collegare più di un motore di machine learning a {{site.data.keyword.aios_short}} utilizzando il metodo `client.data_mart.bindings.add` dell'API Python. 

- Per collegare il motore di machine learning {{site.data.keyword.pm_full}}, eseguire il seguente comando:

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- Per collegare il motore di machine learning Azure ML Studio, eseguire il seguente comando:

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- Per collegare il motore di machine learning AWS Sagemaker, eseguire il seguente comando:

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

Per visualizzare un elenco di tutti i collegamenti, eseguire il metodo `list`:

`    client.data_mart.bindings.list()
    `


| uid | nome | tipo_servizio | creato |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | motore Azure ML Studio | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | istanza WML | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | motore AWS SageMaker | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tabella 1. Collegamenti servizio" caption-side="top"}


Per informazioni su specifici motori di machine learning, consultare i seguenti argomenti:

- [Collegare il motore di machine learning personalizzato](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).
- [Collegare il motore di machine learning Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [Collegare il motore di machine learning Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


Per un esempio funzionante di un notebook reale, consultare [i notebook di esempio di {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

