---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# Specifica di un'istanza di Microsoft Azure ML Studio
{: #connect-azure}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza di Microsoft Azure ML Studio. L'istanza di Azure ML Studio è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

## Connessione dell'istanza di Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza di Azure ML Studio.

1.  Dalla home page dello strumento {{site.data.keyword.aios_short}}, fare clic su **Inizia**.

    ![Home page](images/gs-config-start.png)

1.  Selezionare il riquadro **Microsoft Azure ML Studio** e fare clic su **Avanti**.

    ![Selezionare Azure ML Studio](images/connect-azure.png)

1.  Immettere le credenziali:

    Consultare [How to: Use the portal to create an Azure AD application and service principal that can access resources ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window} per istruzioni su come ottenere le credenziali di Microsoft Azure.
    {: note}

    ![Immettere le credenziali Azure ML Studio](images/connect-azure-cred.png)

1.  Fare clic su **Avanti**.

1.  {{site.data.keyword.aios_short}} elencherà i modelli distribuiti; selezionare quelli che si desidera monitorare

    ![Selezionare i modelli MS Azure distribuiti](images/connect-azure-deploys.png)

1.  Fare clic su **Avanti**.

### Passi successivi
{: #ca-next}

{{site.data.keyword.aios_short}} ora è pronto per poter  [specificare il database](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db).
