---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Microsoft Azure, ml, machine learning, services

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

1.  Na página inicial da ferramenta {{site.data.keyword.aios_short}}, clique em **Iniciar**.

    ![Home page](images/gs-config-start.png)

1.  Selecione o ladrilho **Microsoft Azure ML Studio** e clique em **Avançar**.

    ![Selecione o Azure ML Studio](images/connect-azure.png)

1.  Insira suas credenciais:

    - ID do cliente: o valor de sequência real de seu ID do cliente, que verifica quem você é, além de autenticar e autorizar chamadas feitas para o Azure Studio.
    - Segredo do cliente: o valor de sequência real do segredo, que verifica quem você é, além de autenticar e autorizar chamadas feitas para o Azure Studio.
    - Locatário: seu ID do locatário corresponde à sua organização e é uma instância dedicada do Azure AD. Para localizar o ID do locatário, passe o mouse sobre o nome de sua conta para obter o ID do diretório/locatário ou selecione Azure Active Directory > Propriedades > ID do diretório no portal do Azure.
    - ID da assinatura: credenciais de assinatura que identificam exclusivamente a assinatura do Microsoft Azure. O ID da assinatura faz parte do URI de cada chamada de serviço.

    Consulte [Como: Usar o portal para criar um aplicativo e uma entidade de serviço do Microsoft Azure Active Directory que possa acessar recursos](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} para obter instruções sobre como obter suas credenciais do Microsoft Azure.
    {: note}

    ![Insira as credenciais do Azure ML Studio](images/connect-azure-cred.png)

1.  Clique em **Avançar**.

1.  O {{site.data.keyword.aios_short}} listará seus modelos implementados; selecione os que você deseja monitorar

    ![Select MS Azure deployed models](images/connect-azure-deploys.png)

1.  Clique em **Avançar**.

### Próximos passos
{: #ca-next}

O {{site.data.keyword.aios_short}} está agora pronto para você [especificar seu banco de dados](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db).
