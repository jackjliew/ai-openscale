---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

O {{site.data.keyword.aios_short}} suporta múltiplos mecanismos de aprendizado de máquina em uma única instância. É possível provisioná-los por meio da configuração do painel do {{site.data.keyword.aios_short}} ou do [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).
{: shortdesc}

Ao configurar pela primeira vez o {{site.data.keyword.aios_short}}, você pode ter usado a interface com o usuário ou a opção de configuração automatizada para provisionar seu primeiro mecanismo de aprendizado de máquina. A inclusão de mecanismos de aprendizado de máquina requer que você use a guia de configuração no painel do {{site.data.keyword.aios_short}} ou o Python SDK.

## Usando o painel para incluir provedores
{: #fmrk-workaround-multmleng-dashboard}

1. Depois de abrir o {{site.data.keyword.aios_short}}, na guia **Configurar**, clique nos botões **Incluir provedores de aprendizado de máquina**.

   ![O botão Incluir provedores é mostrado na janela Provedores de aprendizado de máquina](images/wos-configure-multi-providers.png)

2. Clique no bloco do fornecedor que você deseja incluir e clique em **Avançar**.

   ![a tela Seleção de provedores de aprendizado de máquina é mostrada](images/wos-machine-learning-providers-selection.png)

3. Insira as informações necessárias, tais como as credenciais e clique em **Salvar**.

Depois de salvar sua configuração, você terá a opção de ir para o painel, escolher implementações ou configurar monitores.

## Editando provedores de aprendizado de máquina
{: #fmrk-workaround-editingproviders-dashboard}

Precisa editar um provedor de aprendizado de máquina? Clique no ícone do menu do bloco ![o ícone do menu do bloco](images/v-three-dots.png) e, em seguida, em **Visualizar e editar detalhes**.

   ![a opção de visualização e edição dos provedores de aprendizado de máquina é mostrada](images/wos-machine-learning-providers-edit.png)

## Incluindo provedores de aprendizado de máquina usando o método de ligação Python SDK
{: #fmrk-workaround-multmleng-binding}

É possível ligar mais de um mecanismo de aprendizado de máquina ao {{site.data.keyword.aios_short}} usando o método `client.data_mart.bindings.add` da API Python. 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- Para ligar o mecanismo de aprendizado de máquina {{site.data.keyword.pm_full}}, execute o comando a seguir:

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- Para ligar o mecanismo de aprendizado de máquina Azure ML Studio, execute o comando a seguir:

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon SageMaker
{: #fmrk-workaround-multmleng-binding-aws}

- Para ligar o mecanismo de aprendizado de máquina AWS Sagemaker, execute o comando a seguir:

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

### Microsoft Azure ML Service
{: #fmrk-workaround-multmleng-binding-azureservice}

- Para ligar o mecanismo de aprendizado de máquina do Azure ML Service, execute o comando a seguir:

  `binding_uid_4 = client.data_mart.bindings.add('My Azure ML Service engine', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### Produzindo uma lista de provedores de aprendizado de máquina
{: #fmrk-workaround-multmleng-binding-list}

Para visualizar uma lista de todas as ligações, execute o método `list`:

`    client.data_mart.bindings.list ()
    `


| uid | nome | service_type | Criado |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | Meu mecanismo do Azure ML Service | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | Meu mecanismo Azure ML Studio | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | Instância do WML | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | Meu mecanismo AWS SageMaker | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tabela 1. Ligações de serviço" caption-side="top"}


Para obter informações sobre mecanismos de aprendizado de máquina específicos, consulte os tópicos a seguir:

- [Ligar seu mecanismo de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind).
- [Ligar o seu mecanismo de estúdio de aprendizado de máquina do Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [Ligar o mecanismo de serviço de aprendizado de máquina Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [Ligar seu mecanismo de aprendizado de máquina do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


Para obter um exemplo de trabalho de um bloco de notas real, consulte [os blocos de notas de amostra do {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

