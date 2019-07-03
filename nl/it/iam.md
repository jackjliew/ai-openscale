---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## Ruoli e azioni di Identity and Access Management

L'accesso alle istanze del servizio {{site.data.keyword.aios_full}} per gli utenti nel proprio account è controllato da {{site.data.keyword.Bluemix_notm}} IAM (Identity and Access Management). A ogni utente che accede al servizio {{site.data.keyword.aios_short}} nel proprio account deve essere assegnata una politica di accesso con un ruolo IAM definito. La politica determina le azioni che un utente può eseguire all'interno del contesto del servizio o dell'istanza selezionati. Le azioni consentite sono personalizzate e definite dal servizio {{site.data.keyword.Bluemix_notm}} come operazioni che è consentito eseguire sul servizio. Le azioni vengono quindi associate ai ruoli utente IAM.

Le politiche consentono di concedere l'accesso a diversi livelli. Alcune delle opzioni includono quanto segue: 

* Accesso a tutte le istanze del servizio nel proprio account
* Accesso a una singola istanza del servizio nel proprio account
* Accesso a una risorsa specifica all'interno di un'istanza

Dopo aver definito l'ambito della politica di accesso, si assegna un ruolo che determina il livello di accesso dell'utente. Esaminare le seguenti tabelle che descrivono quali azioni sono consentite da ciascun ruolo all'interno del servizio {{site.data.keyword.aios_short}}.

La seguente tabella illustra le azioni che sono associate ai ruoli di gestione della piattaforma. I ruoli di gestione della piattaforma consentono agli utenti di eseguire attività sulle risorse del servizio a livello di piattaforma, ad esempio assegnare l'accesso utente per il servizio, creare o eliminare istanze e collegare le istanze alle applicazioni.

|Ruolo gestione piattaforma|Descrizione delle azioni| Azioni di esempio                                               |
|--------------------------|------------------------|-----------------------------------------------------------------|
|Visualizzatore            | Descrizione            | <ul><li>Esempio 1</li><li>Esempio 2</li></ul>                   |
|Editor                    | Descrizione            |<ul><li>Esempio 1</li><li>Esempio 2</li></ul>                    |
|Operatore                 | Descrizione            | <ul><li>Esempio 1</li><li>Esempio 2</li><li>Esempio 3</li></ul> |
|Amministratore            | Descrizione            |<ul><li>Esempio 1</li><li>Esempio 2</li><li>Esempio 3</li></ul>  |
{: caption="Tabella 1. Azioni e ruoli utente IAM" caption-side="top"}


La seguente tabella descrive le azioni associate ai ruoli di accesso al servizio. I ruoli di accesso al servizio consentono agli utenti di accedere a {{site.data.keyword.aios_short}} così come di richiamare l'API {{site.data.keyword.aios_short}}.

|Ruolo accesso servizio|Descrizione delle azioni|Azioni di esempio                                               |
|---------------------|------------------------|-----------------------------------------------------------------|
|Lettore              | Descrizione            | <ul><li>Esempio 1</li><li>Esempio 2</li></ul>                   |
|Scrittore            | Descrizione            |<ul><li>Esempio 1</li><li>Esempio 2</li></ul>                    |
|Manager              | Descrizione            | <ul><li>Esempio 1</li><li>Esempio 2</li><li>Esempio 3</li></ul> |
{: caption="Tabella 2. Azioni e ruoli accesso al servizio IAM" caption-side="top"}


Per informazioni sull'assegnazione dei ruoli utente nell'interfaccia utente, consultare [Gestione dell'accesso alle risorse](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
