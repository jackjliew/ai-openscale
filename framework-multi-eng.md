---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: multiple engines, non-Watson, machine learning, frameworks, provision

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

# Support for multiple machine learning engines
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} supports multiple machine learning engines within a single instance provided that provisioning is performed through the [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).
{: shortdesc}

When you first set up {{site.data.keyword.aios_short}}, you may have used the user interface or the automated setup option to provision your first machine learning engine. Adding machine learning engines requires that you use the Python SDK. Specifically, you can add machine learning engines to {{site.data.keyword.aios_short}} by using the `client.data_mart.bindings.add` method.

## Binding methods
{: #fmrk-workaround-multmleng-binding}

You can bind more than one machine learning engine to {{site.data.keyword.aios_short}} by using the Python API `client.data_mart.bindings.add` method. 

- To bind the {{site.data.keyword.pm_full}} machine learning engine, run the following command:

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- To bind the Azure ML Studio machine learning engine, run the following command:

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- To bind the AWS Sagemaker machine learning engine, run the following command:

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

To view a list of all the bindings, run the `list` method:

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Table 1. Service bindings" caption-side="top"}


For information about specific machine learning engines, see the following topics:

- [Bind your Custom machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).
- [Bind your Microsoft Azure machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [Bind your Amazon SageMaker machine learning engine](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


For a working example of an actual notebook, see [the {{site.data.keyword.aios_short}} sample notebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

