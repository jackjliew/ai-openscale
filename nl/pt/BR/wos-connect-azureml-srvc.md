---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure ML service, ml, machine learning, services

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

# Especificando uma instância do Microsoft Azure ML Service
{: #connect-azureservice}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância do Microsoft Azure ML Service. A instância do Azure ML Service é o local em que você armazena seus modelos e implementações de IA.
{: shortdesc}

Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Para obter mais informações sobre como realizar essa execução programaticamente, consulte [Vincule seu mecanismo de aprendizado de máquina do serviço Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Conecte a sua instância do Azure ML Service
{: #ca-connect}

O {{site.data.keyword.aios_short}} se conecta aos modelos e implementações de IA em uma instância do Azure ML Service.

1. Na guia **Configurar**, clique em **Provedor de aprendizado de máquina**. Dependendo de seu ambiente, talvez você não veja todos os provedores a seguir:

   ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

1.  Clique no bloco **Microsoft Azure ML Service**.
1.  Insira e salve suas credenciais:

    - Identificador de cliente: o valor da sequência real de seu identificador de cliente, que verifica quem você é e autentica e autoriza as chamadas que você faz para o Azure Service.
    - Segredo do cliente: o valor da sequência real do segredo, que verifica quem você é e autentica e autoriza as chamadas que você faz para o Azure Service.
    - Locatário: seu ID do locatário corresponde à sua organização e é uma instância dedicada do Azure AD. Para localizar o ID do locatário, passe o mouse sobre o nome de sua conta para obter o ID do diretório/locatário ou selecione Azure Active Directory > Propriedades > ID do diretório no portal do Azure.
    - ID da assinatura: credenciais de assinatura que identificam exclusivamente a assinatura do Microsoft Azure. O ID da assinatura faz parte do URI de cada chamada de serviço.
    - Nome da instância do provedor de serviços: o nome específico designado a esse provedor de serviços.
    - Descrição (opcional): sua descrição em linguagem simples dessa instância do provedor de serviços. Se tiver ambientes de produção e teste, inclua essas informações nestes locais.

    Consulte [Como: Usar o portal para criar um aplicativo e uma entidade de serviço do Microsoft Azure Active Directory que possa acessar recursos](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} para obter instruções sobre como obter suas credenciais do Microsoft Azure.
    {: note}

1.  O {{site.data.keyword.aios_short}} lista seus modelos implementados. Selecione aqueles que você deseja monitorar e clique em **Configurar**.

Você selecionou com êxito as implementações.

### Próximos passos
{: #ca-next}

Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
