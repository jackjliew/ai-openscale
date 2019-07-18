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

# Specifica di un'istanza di Microsoft Azure ML Studio
{: #connect-azure}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza di Microsoft Azure ML Studio. L'istanza di Azure ML Studio è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

## Connessione dell'istanza di Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza di Azure ML Studio.

1.  Dalla scheda **Configura**, fare clic su **Provider di machine learning**.

    ![viene visualizzato il pannello per la selezione del provider del servizio di machine learning con i riquadri per i motori di machine learning supportati](images/wos-machine-learning-providers-selection.png)

1.  Fare clic sul riquadro **Microsoft Azure ML Studio**.

    ![Immettere le credenziali Azure ML Studio](images/connect-azure-cred.png)

1.  Immettere e salvare le credenziali:

    - ID client: il valore stringa effettivo dell'ID client, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno ad Azure Studio.
    - Segreto client: il valore stringa effettivo del segreto, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno ad Azure Studio.
    - Tenant: l'ID tenant corrisponde alla propria organizzazione ed è un'istanza dedicata di Azure AD. Per trovare l'ID tenant, passare il puntatore sul nome account per ottenere l'ID tenant/directory oppure selezionare Azure Active Directory > Proprietà > ID directory nel portale Azure.
    - ID sottoscrizione: le credenziali di sottoscrizione che identificano in modo univoco la propria sottoscrizione Microsoft Azure. L'ID sottoscrizione forma parte dell'URI per ogni chiamata al servizio.

    Consultare [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} per istruzioni su come ottenere le credenziali di Microsoft Azure.
    {: note}

1.  {{site.data.keyword.aios_short}} elenca i modelli distribuiti; selezionare quelli che si desidera monitorare e fare clic su **Configura**.

Sono state selezionate correttamente le distribuzioni.

### Passi successivi
{: #ca-next}

{{site.data.keyword.aios_short}} ora è pronto per poter [configurare i monitor](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
