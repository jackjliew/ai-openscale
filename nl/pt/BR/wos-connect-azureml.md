---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure studio, ml, machine learning, services, studio

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

# Especificando uma instância do Microsoft Azure ML Studio
{: #connect-azure}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância
do Microsoft Azure ML Studio. Sua instância do Azure ML Studio é onde você armazena seus modelos e
implementações de IA.
{: shortdesc}

Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

## Conecte sua instância do Azure ML Studio
{: #ca-connect}

O {{site.data.keyword.aios_short}} se conecta aos modelos e implementações de IA em uma
instância do Azure ML Studio.

1. Na guia **Configurar**, clique em **Provedor de aprendizado de máquina**. Dependendo de seu ambiente, talvez você não veja todos os provedores a seguir:

   ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

1.  Clique no bloco **Microsoft Azure ML Studio**.

    ![Insira as credenciais do Azure ML Studio](images/connect-azure-cred.png)

1.  Insira e salve suas credenciais:

    - ID do cliente: o valor de sequência real de seu ID do cliente, que verifica quem você é, além de autenticar e autorizar chamadas feitas para o Azure Studio.
    - Segredo do cliente: o valor de sequência real do segredo, que verifica quem você é, além de autenticar e autorizar chamadas feitas para o Azure Studio.
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
