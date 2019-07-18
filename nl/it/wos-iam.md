---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


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

Con i ruoli di gestione della piattaforma è possibile assegnare agli utenti diversi livelli di autorizzazione per l'esecuzione di azioni della piattaforma all'interno dell'account o su un servizio. Ad esempio, i ruoli di gestione della piattaforma assegnati alle risorse di catalogo, consentono agli utenti di completare azioni come la creazione, l'eliminazione, la modifica e la visualizzazione delle istanze del servizio. Mentre i ruoli di gestione della piattaforma assegnati ai servizi di gestione dell'account consentono agli utenti di completare azioni come l'invito e la rimozione degli utenti, l'utilizzo dei gruppi di risorse e la visualizzazione delle informazioni di fatturazione. Per ulteriori informazioni sui servizi di gestione account, consultare [Assegnazione dell'accesso ai servizi di gestione account](/docs/iam?topic=iam-account-services#account-services).

Seleziona tutti i ruoli interessati quando si crea una politica. Ogni ruolo consente di completare azioni separate e non eredita le azioni dei ruoli inferiori.
{: tip}

La seguente tabella fornisce degli esempi per alcune delle azioni di gestione della piattaforma che gli utenti possono intraprendere nel contesto delle risorse di catalogo e dei gruppi di risorse. Consultare la documentazione di ogni offerta del catalogo per comprendere in che modo i ruoli vengono applicati agli utenti nel contesto del servizio utilizzato.


|  | Uno o tutti i servizi abilitati a IAM | Servizio selezionato in un gruppo di risorse | Gruppo di risorse selezionato |
|:--------------|:------------|:-------------|:-------------|
| Ruolo visualizzatore | Visualizzare istanze, alias, bind e credenziali | Visualizzare solo le istanze specificate nel gruppo di risorse | Visualizzare il gruppo di risorse |
| Ruolo operatore |  Visualizzare istanze e gestire alias, bind e credenziali |  Non applicabile | Non applicabile |
| Ruolo editor |  Creare, eliminare, modificare e visualizzare istanze. Gestire alias, bind e credenziali | Creare, eliminare, modificare, sospendere, riprendere, visualizzare e associare solo le istanze specificate nel gruppo di risorse | Visualizzare e modificare il nome del gruppo di risorse |
| Ruolo amministratore |  Tutte le azioni di gestione per i servizi | Tutte le azioni di gestione per le istanze specificate nel gruppo di risorse | Visualizzare, modificare e gestire l'accesso per il gruppo di risorse |
| Ruolo amministratore cluster (specifico solo di {{site.data.keyword.wos4d_full}}) | Ha accesso completo alla piattaforma IBM Cloud Private |Ha accesso completo alle istanze specificate nel gruppo di risorse | Le seguenti azioni possono essere completate solo dall'amministratore del cluster: connessione a una directory LDAP, aggiunta di utenti e assegnazione di ruoli IAM, gestione di carichi di lavoro, infrastruttura e applicazioni in tutti gli spazi dei nomi, creazione di spazi dei nomi, assegnazione quote, aggiunta di politiche di sicurezza pod, aggiunta di un repository Helm interno, eliminazione di un repository Helm interno, aggiunta di grafici Helm al repository Helm interno, rimozione di grafici Helm dal repository Helm interno, e sincronizzazione di repository Helm interni ed esterni |
{: row-headers}
{: class="comparison-table"}
{: caption="Tabella 1. Ruoli e azioni di gestione della piattaforma di esempio per i servizi in un account" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


Per i ruoli di accesso al servizio, che consentono agli utenti di accedere a {{site.data.keyword.aios_short}} nonché alla capacità di chiamare l'API REST, {{site.data.keyword.aios_short}} rimanda ai ruoli di gestione della piattaforma elencati nella tabella precedente. Per informazioni sull'assegnazione dei ruoli utente nell'interfaccia utente, consultare [Gestione dell'accesso alle risorse](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

 
