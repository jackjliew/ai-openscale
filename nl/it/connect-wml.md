---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Specifica di un'istanza del servizio {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #wml-connect}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza {{site.data.keyword.pm_full}}. L'istanza {{site.data.keyword.pm_short}} è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

## Prerequisiti
{: #wml-prereq}

È necessario aver eseguito il provisioning di un'istanza {{site.data.keyword.pm_full}} nello stesso account {{site.data.keyword.Bluemix_notm}} in cui è presente l'istanza del servizio {{site.data.keyword.aios_short}}. Se è stato eseguito il provisioning di un'istanza {{site.data.keyword.pm_full}} in un altro account, non sarà possibile configurare quell'istanza con la registrazione automatica del payload con {{site.data.keyword.aios_short}}.

## Connessione dell'istanza del servizio {{site.data.keyword.pm_short}}
{: #wml-config}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza {{site.data.keyword.pm_full}}.

1.  Dalla home page dello strumento {{site.data.keyword.aios_short}}, fare clic su **Inizia**.

    ![Home page](images/gs-config-start.png)

2.  Seleziona il riquadro {{site.data.keyword.pm_full}}.

    ![Selezione riquadro](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} controlla l'account {{site.data.keyword.Bluemix_notm}} per individuare eventuali istanze {{site.data.keyword.pm_full}} esistenti. È possibile quindi selezionare un'istanza dal menu a discesa **Servizio Watson Machine Learning**.

    ![Selezionare il servizio {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

4.  (Facoltativo) Si può anche scegliere l'opzione **Seleziona un percorso differente**, per specificare un'ubicazione di machine learning al di fuori del proprio account {{site.data.keyword.Bluemix_notm}}. Fornire le credenziali per la propria ubicazione come JSON valido:

    ![Impostare l'istanza {{site.data.keyword.pm_short}}](images/gs-get-wml.png)

    Fare clic su **Avanti**.

5.  {{site.data.keyword.aios_short}} controlla l'istanza di Machine Learning selezionata per individuare un elenco di distribuzioni memorizzate in quell'istanza. Dall'elenco di distribuzioni, selezionare quelle da monitorare.

    ![Selezionare distribuzioni](images/gs-config-deploy.png)

6.  Fare clic su **Avanti**.
7.  Fare clic su **Salva**.

### Passi successivi
{: #wml-next}

{{site.data.keyword.aios_short}} ora è pronto per poter  [specificare un database](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
