---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Specifica di un'istanza del servizio Watson Machine Learning
{: #wml-connect}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza Watson Machine Learning (WML). L'istanza WML è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

## Prerequisiti
{: #wml-prereq}

È necessario aver eseguito il provisioning di un'istanza WML nello stesso account {{site.data.keyword.Bluemix_notm}} in cui è presente l'istanza del servizio {{site.data.keyword.aios_short}}. Se è stato eseguito il provisioning di un'istanza WML in un altro account, non sarà possibile configurare quell'istanza con {{site.data.keyword.aios_short}}.

## Connessione dell'istanza del servizio Watson Machine Learning
{: #wml-config}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza WML.

1.  Dalla home page dello strumento {{site.data.keyword.aios_short}}, fare clic su **Inizia**.

    ![Home page](images/gs-config-start.png)

2.  Selezionare il riquadro Watson Machine Learning.

    ![Selezione riquadro](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} controlla l'account {{site.data.keyword.Bluemix_notm}} per individuare eventuali istanze WML esistenti. È possibile quindi selezionare un'istanza dal menu a discesa **Servizio Watson Machine Learning**.

    ![Selezionare il servizio WML](images/gs-set-wml.png)

4.  (Facoltativo) Si può anche scegliere l'opzione **Seleziona un percorso differente**, per specificare un'ubicazione di machine learning al di fuori del proprio account {{site.data.keyword.Bluemix_notm}}. Fornire le credenziali per la propria ubicazione come JSON valido:

    ![Impostare l'istanza WML](images/gs-get-wml.png)

    Fare clic su **Avanti**.

5.  {{site.data.keyword.aios_short}} controlla l'istanza di Machine Learning selezionata per individuare un elenco di distribuzioni memorizzate in quell'istanza. Dall'elenco di distribuzioni, selezionare quelle da monitorare.

    ![Selezionare distribuzioni](images/gs-config-deploy.png)

6.  Fare clic su **Avanti**.
7.  Fare clic su **Salva**.

### Passi successivi
{: #wml-next}

{{site.data.keyword.aios_short}} ora è pronto per poter  [specificare un database](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
