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

# Suporte para múltiplos mecanismos de aprendizado de máquina
{: #fmrk-workaround-multmleng}

O {{site.data.keyword.aios_short}} suporta múltiplos mecanismos de aprendizado de máquina em uma única instância, desde que o provisionamento seja executado por meio do [SDK do Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820)
{: shortdesc}

Ao configurar pela primeira vez o {{site.data.keyword.aios_short}}, você pode ter usado a interface com o usuário ou a opção de configuração automatizada para provisionar seu primeiro mecanismo de aprendizado de máquina. A inclusão de mecanismos de aprendizado de máquina requer que você use o SDK do Python. Especificamente, é possível incluir mecanismos de aprendizado de máquina no {{site.data.keyword.aios_short}} usando o método `client.data_mart.bindings.add`.

## Métodos de ligação
{: #fmrk-workaround-multmleng-binding}

É possível ligar mais de um mecanismo de aprendizado de máquina ao {{site.data.keyword.aios_short}} usando o método `client.data_mart.bindings.add` da API Python. 

- Para ligar o mecanismo de aprendizado de máquina {{site.data.keyword.pm_full}}, execute o comando a seguir:

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- Para ligar o mecanismo de aprendizado de máquina Azure ML Studio, execute o comando a seguir:

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- Para ligar o mecanismo de aprendizado de máquina AWS Sagemaker, execute o comando a seguir:

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

Para visualizar uma lista de todas as ligações, execute o método `list`:

`    client.data_mart.bindings.list ()
    `


| uid | nome | service_type | Criado |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | Meu mecanismo Azure ML Studio | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | Instância do WML | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | Meu mecanismo AWS SageMaker | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tabela 1. Ligações de serviço" caption-side="top"}


Para obter informações sobre mecanismos de aprendizado de máquina específicos, consulte os tópicos a seguir:

- [Ligar seu mecanismo de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).
- [Ligar seu mecanismo de aprendizado de máquina do Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [Ligar seu mecanismo de aprendizado de máquina do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


Para obter um exemplo de trabalho de um bloco de notas real, consulte [os blocos de notas de amostra do {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

