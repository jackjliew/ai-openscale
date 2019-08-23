---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Especificando uma instância de serviço do Amazon SageMaker ML
{: #csm-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância de serviço do Amazon SageMaker. Sua instância de serviço do Amazon SageMaker é onde você armazena seus modelos e implementações de IA.
{: shortdesc}

Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

## Conecte sua instância de serviço Amazon SageMaker
{: #csm-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância de serviço do Amazon SageMaker.

1. Na guia **Configurar**, clique em **Provedor de aprendizado de máquina**. Dependendo de seu ambiente, talvez você não veja todos os provedores a seguir:

   ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

1.  Clique no bloco **Amazon SageMaker**.

    ![Inserir as credenciais de serviço do Amazon SageMaker](images/connect-sage-cred.png)

1.  Insira e salve suas credenciais:

    - ID da chave de acesso: seu ID da chave de acesso da AWS, `aws_access_key_id`, que verifica quem você é, além de autenticar e autorizar chamadas feitas para a AWS.
    - Chave de acesso secreta: sua chave de acesso secreta da AWS, `aws_secret_access_key`, que é necessária para verificar quem você, além de para autenticar e autorizar chamadas feitas para a AWS.
    - Região: insira a região onde seu ID da chave de acesso foi criado. As chaves são armazenadas e usadas na região em que foram criadas e não podem ser transferidas para outra região. 
    - Nome da instância do provedor de serviços: o nome específico designado a esse provedor de serviços.
    - Descrição (opcional): sua descrição em linguagem simples dessa instância do provedor de serviços. Se tiver ambientes de produção e teste, inclua essas informações nestes locais.

1.  O {{site.data.keyword.aios_short}} lista seus modelos implementados. Selecione aqueles que você deseja monitorar.

### Próximos passos
{: #csm-next}

Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
