---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Creazione di credenziali
{: #cred-create}

Per accedere alle API REST di {{site.data.keyword.aios_short}}, sono richiesti una chiave API della piattaforma e un ID data mart (istanza del servizio). La chiave API della piattaforma fornisce a un singolo utente la possibilità di accedere alle risorse in {{site.data.keyword.cloud_notm}}.

Per gli account enterprise, un amministratore può creare il data mart e, quindi, invitare altri utenti nell'account, fornendo a tali utenti l'accesso a un data mart {{site.data.keyword.aios_short}} specifico. Quindi, un utente può creare la propria chiave API della piattaforma e accedere allo stesso data mart {{site.data.keyword.aios_short}}; non si verifica alcun conflitto o rischio per la sicurezza.

Per creare una chiave API della piattaforma, completare la seguente procedura:

- Accedere a [{{site.data.keyword.cloud_notm}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}){: new_window}.

- Selezionare **Gestisci** --> **Sicurezza** --> **Chiavi API della piattaforma**

    ![Chiavi API della piattaforma](images/cred-api-key.png)

- Creare e salvare una chiave API della piattaforma.

Per trovare l'ID (o l'istanza del servizio) del data mart dell'utente:

- Nella pagina {{site.data.keyword.aios_short}} **Configurazione --> Riepilogo**, la prima voce è l'ID (istanza del servizio) del data mart.

    ![ID data mart](images/data-mart-id.png)
