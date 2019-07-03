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

# Soporte para varios motores de aprendizaje automático
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} da soporte a varios motores de aprendizaje automático en una única instancia siempre que suministro se
realice mediante el
[SDK de Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).
{: shortdesc}

Cuando configuró por primera vez {{site.data.keyword.aios_short}}, es posible que utilizara la interfaz de usuario o la opción de configuración
automática para suministrar el primer motor de aprendizaje automático. Añadir motores de aprendizaje automático requiere que se utilice el SDK de
Python. En particular, puede añadir motores de aprendizaje automático a {{site.data.keyword.aios_short}} utilizando el método
`client.data_mart.bindings.add`.

## Métodos de enlace
{: #fmrk-workaround-multmleng-binding}

Puede enlazar más de un motor de aprendizaje automático a {{site.data.keyword.aios_short}} utilizando el método de la API de Python API `client.data_mart.bindings.add`. 

- Para enlazar el motor de aprendizaje automático de {{site.data.keyword.pm_full}}, ejecute los mandatos siguientes:

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- Para enlazar el motor de aprendizaje automático de Azure ML Studio, ejecute el mandato siguiente:

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- Para enlazar el motor de aprendizaje automático de AWS Sagemaker, ejecute el mandato siguiente:

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

Para ver una lista de todos los enlaces, ejecute el método `list`:

`client.data_mart.bindings.list()`


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | My Azure ML Studio engine | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML instance | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | My AWS SageMaker engine | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tabla 1. Enlaces de servicio" caption-side="top"}


Para obtener información sobre los motores de aprendizaje automático específicos, consulte los temas siguientes:

- [Enlazar el motor de aprendizaje automático
personalizado](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).
- [Enlazar el motor de Microsoft Azure Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [Enlazar el motor de aprendizaje automático de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


Para ver un ejemplo de trabajo de un cuaderno real, consulte [los cuadernos de ejemplo de {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

