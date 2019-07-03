---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Specifica di un'istanza del servizio Amazon SageMaker ML
{: #csm-connect}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza del servizio Amazon SageMaker. L'istanza del servizio Amazon SageMaker è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

## Connessione dell'istanza del servizio Amazon SageMaker
{: #csm-config}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza del servizio Amazon SageMaker.

1.  Dalla home page dello strumento {{site.data.keyword.aios_short}}, fare clic su **Inizia**.

    ![Home page](images/gs-config-start.png)

1.  Selezionare il riquadro **Amazon SageMaker** e fare clic su **Avanti**.

    ![Selezionare il servizio Amazon SageMaker ](images/connect-sage.png)

1.  Immettere le credenziali:

    - ID chiave di accesso: l'ID chiave di accesso AWS, `aws_access_key_id`, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno a AWS.
    - Chiave di accesso segreta: la chiave di accesso segreta AWS, `aws_secret_access_key`, che è richiesta per verificare chi è l'utente e per autenticare e autorizzare le chiamate che si fanno a AWS.
    - Regione: immettere la regione in cui è stato creato l'ID chiave di accesso. Le chiavi sono memorizzate e utilizzate nella regione in cui sono state create e non possono essere trasferite in un'altra regione. 

    ![Immettere le credenziali del servizio Amazon SageMaker](images/connect-sage-cred.png)

1.  Fare clic su **Avanti**.

1.  {{site.data.keyword.aios_short}} elencherà i modelli distribuiti; selezionare quelli che si desidera monitorare

    ![Selezionare i modelli Amazon SageMaker distribuiti](images/connect-sage-deploys.png)

1.  Fare clic su **Avanti**.

### Passi successivi
{: #csm-next}

{{site.data.keyword.aios_short}} ora è pronto per poter  [specificare un database](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
