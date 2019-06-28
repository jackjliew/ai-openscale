---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure, ml, machine learning, services

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Especificando uma instância do Microsoft Azure ML Studio
{: #connect-azure}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância
do Microsoft Azure ML Studio. Sua instância do Azure ML Studio é onde você armazena seus modelos e
implementações de IA.
{: shortdesc}

## Conecte sua instância do Azure ML Studio
{: #ca-connect}

O {{site.data.keyword.aios_short}} se conecta aos modelos e implementações de IA em uma
instância do Azure ML Studio.

1.  Na página inicial da ferramenta {{site.data.keyword.aios_short}}, clique em **Iniciar**.

    ![Home page](images/gs-config-start.png)

1.  Selecione o ladrilho **Microsoft Azure ML Studio** e clique em **Avançar**.

    ![Selecione o Azure ML Studio](images/connect-azure.png)

1.  Insira suas credenciais:

    Consulte [Como: usar o portal para criar um aplicativo Azure AD e o principal do serviço que pode acessar recursos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window} para obter instruções sobre como obter as credenciais do Microsoft Azure.
    {: note}

    ![Insira as credenciais do Azure ML Studio](images/connect-azure-cred.png)

1.  Clique em **Avançar**.

1.  O {{site.data.keyword.aios_short}} listará seus modelos implementados; selecione os que você deseja monitorar

    ![Select MS Azure deployed models](images/connect-azure-deploys.png)

1.  Clique em **Avançar**.

### Próximos passos
{: #ca-next}

O {{site.data.keyword.aios_short}} agora está pronto para você [especificar seu banco de dados](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db).
