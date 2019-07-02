---

title: Attendibilità e trasparenza per i modelli di machine learning con {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Supporto didattico (avanzato)
{: #tadv-tutorial-advanced}

## Scenario
{: #tadv-scenario}

Un'azienda di autonoleggio ha raccolto i dati di feedback relativi alla soddisfazione dei clienti. Il modello presentato utilizza questi dati per prevedere un corso d'azione da seguire per un cliente, ad esempio per fornire un voucher da utilizzare per il prossimo noleggio.

Il modello utilizza i campi dei dati del cliente ID (un numero ID), GENERE, STATO (celibe/nubile o coniugato/a), FIGLI (numero), ETÀ, STATO CLIENTE (attivo o inattivo), PROPRIETARIO DI AUTOMOBILE (sì o no), SERVIZIO CLIENTE (commento del cliente), SODDISFAZIONE (soddisfatto o insoddisfatto) e AREA DI BUSINESS (relativa a prodotto o servizio) per prevedere uno di quattro valori (NA, voucher, upgrade gratuito, prelievo on-demand) per il campo di dati AZIONE.

## Prerequisiti
{: #tadv-prereqs}

Per completare questo supporto didattico, saranno necessari:

- Un account [Watson Studio ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://dataplatform.ibm.com/){: new_window}.
- Un account [{{site.data.keyword.cloud_notm}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}){: new_window}.

Durante il supporto didattico, verrà eseguito il provisioning dei seguenti servizi {{site.data.keyword.cloud_notm}} Lite (gratuiti):

- Machine Learning
- Apache Spark
- Object Storage

Inoltre, verrà eseguito il provisioning del seguente servizio {{site.data.keyword.cloud_notm}} **a pagamento**:

- PostgreSQL

  È possibile ottenere un credito per {{site.data.keyword.cloud_notm}} pari a 200 dollari passando a un account a pagamento con carta di credito. Se si dispone già di un account a pagamento, si riceverà un rimborso una tantum pari a 16 dollari del costo del primo GB di storage, per un mese.
  {: tip}

Il database PostgreSQL e l'istanza {{site.data.keyword.pm_full}} devono essere distribuiti nello stesso account {{site.data.keyword.cloud_notm}}.
{: important}

Se è già stato eseguito il provisioning dei servizi necessari, ad esempio se è già stato completato il supporto didattico precedente, procedere a [Configurare un progetto Watson Studio](#tadv-setup-ws) di seguito.

## Introduzione
{: #tadv-intro}

In questo supporto didattico, verranno svolte le seguenti attività:

- Eseguire il provisioning di servizi di machine learning e storage di {{site.data.keyword.cloud_notm}}
- Configurare un progetto Watson Studio ed eseguire un notebook Python per creare, eseguire il training e la distribuzione di un modello di machine learning
- Eseguire un notebook Python per creare un data mart, configurare i monitor delle prestazioni, dell'accuratezza e della correttezza e creare dati da monitorare
- Visualizzare i risultati nella scheda Insight di {{site.data.keyword.aios_short}}

## Eseguire il provisioning di servizi {{site.data.keyword.cloud_notm}}
{: #tadv-svcs}

Accedere all'account [{{site.data.keyword.cloud_notm}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}){: new_window} con l'ID IBM. Quando si esegue il provisioning dei servizi, particolarmente nel caso di Apache Spark, Object Storage e Db2 Warehouse, verificare che l'organizzazione e lo spazio selezionati siano identici per tutti i servizi.

### Creare un account Watson Studio
{: #tadv-stac}

- [Creare un'istanza di Watson Studio ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/watson-studio){: new_window} se non si dispone già di un'istanza associata all'account:

  ![Watson Studio](images/watson_studio.png)

- Fornire un nome al servizio, selezionare il piano Lite (gratuito) e fare clic sul pulsante **Crea**.

### Eseguire il provisioning di un servizio di Machine Learning
{: #tadv-pml}

- [Eseguire il provisioning di un'istanza di Watson Machine Learning ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/machine-learning){: new_window} se non si dispone già di un'istanza associata all'account:

  ![Machine Learning](images/machine_learning.png)

- Fornire un nome al servizio, selezionare il piano Lite (gratuito) e fare clic sul pulsante **Crea**.

- Prendere nota delle credenziali del servizio di Machine Learning. Nell'istanza di machine learning, fare clic sul link **Credenziali del servizio** nella parte sinistra della pagina. Assegnare un nome alla credenziale e fare clic su **Aggiungi**. Quindi, dall'elenco di credenziali, fare clic su **Visualizza credenziale** e copiare le credenziali per uso successivo.

### Eseguire il provisioning di un servizio Spark
{: #tadv-ps}

- [Eseguire il provisioning di un servizio Spark ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/apache-spark){: new_window} se non si dispone già di un servizio associato all'account:

  ![Apache Spark](images/spark.png)

- Assegnare un nome al servizio, selezionare il piano Lite (gratuito) e fare clic sul pulsante **Crea**.

- Prendere nota delle credenziali del servizio per l'istanza di Spark. Aprire l'istanza di Spark e fare clic su **Credenziali di servizio** nel menu a sinistra. Fare clic sul pulsante **Nuova credenziale**, assegnare un nome alle credenziali e fare clic su **Aggiungi**. Quindi, fare clic sul link **Visualizza credenziali** accanto alla serie appena creata e copiare le credenziali per uso successivo.

### Eseguire il provisioning di un servizio Object Storage
{: #tadv-pos}

- [Eseguire il provisioning di un servizio Object Storage ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} se non si dispone già di un servizio associato all'account:

  ![Object Storage](images/object_storage.png)

- Fornire un nome al servizio, selezionare il piano Lite (gratuito) e fare clic sul pulsante **Crea**.

### Eseguire il provisioning di un servizio PostgreSQL a pagamento
{: #tadv-ppgs}

- [Eseguire il provisioning di un servizio PostgreSQL a pagamento ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window} se non si dispone già di un servizio associato all'account.

  ![Compose for PostgreSQL](images/postgres.png)

- Fornire un nome al servizio, selezionare il piano Standard e fare clic sul pulsante **Crea**.

  È possibile ottenere un credito per {{site.data.keyword.cloud_notm}} pari a 200 dollari passando a un account a pagamento con carta di credito. Se si dispone già di un account a pagamento, si riceverà un rimborso una tantum pari a 16 dollari del costo del primo GB di storage, per un mese.
  {: tip}

- Prendere nota delle credenziali del servizio per l'istanza di PostgreSQL. Aprire l'istanza esistente (o appena creata) di PostgreSQL e fare clic su **Credenziali di servizio** nel menu a sinistra. Fare clic sul pulsante **Nuova credenziale**, assegnare un nome alle credenziali e fare clic su **Aggiungi**. Quindi, fare clic sul link **Visualizza credenziali** accanto alla serie appena creata e copiare le credenziali per uso successivo.

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![Set data type manually](images/data-type-manual.png)

- Ora, i dati di training dovrebbero essere visualizzati correttamente nelle colonne. Fare clic su **Avanti** per continuare, quindi fare clic su **Avvia caricamento** per caricare i dati.

--->

## Configurare un progetto Watson Studio
{: #tadv-setup-ws}

- Accedere all'[account Watson Studio![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://dataplatform.ibm.com/){: new_window}. Fare clic sull'icona dell'avatar dell'account nella parte in alto a destra e verificare che l'account che si sta utilizzando sia lo stesso account utilizzato per creare i servizi {{site.data.keyword.cloud_notm}}:

  ![Stesso account](images/same_account.png)

- In Watson Studio, iniziare creando un nuovo progetto. Selezionare "Crea un progetto":

  ![Crea progetto Watson Studio](images/studio_create_proj.png)

- Selezionare il riquadro **Standard** per creare il progetto:

  ![Seleziona progetto Standard Watson Studio](images/studio_create_standard.png)

- Fornire un nome e una descrizione al progetto, accertarsi che il servizio Object Storage creato nel passo precedente sia selezionato nel menu a discesa **Storage** e fare clic su **Crea**.

### Associare i servizi {{site.data.keyword.cloud_notm}} al progetto Watson
{: #tadv-acsw}

- Aprire il progetto Watson Studio e selezionare la scheda **Impostazioni**. Nella sezione **Servizi associati**, fare clic sul menu a discesa **Aggiungi servizio** e selezionare **Watson**:

  ![Aggiungi servizio Watson](images/add_watson_service.png)

- Fare clic sul link **Aggiungi** nel riquadro **Machine Learning** e selezionare la scheda **Esistente**. Selezionare il servizio creato nella sezione precedente dal menu a discesa **Istanza di servizio esistente** e fare clic su **Seleziona**.

- Dalla scheda delle impostazioni del progetto, selezionare nuovamente **Aggiungi servizio** e selezionare **Spark** dal menu a discesa. Dalla scheda **Esistente**, selezionare il servizio Spark creato e fare clic su **Seleziona**.

## Creare e distribuire un modello di machine learning
{: #tadv-deploy-ml}

### Aggiungere il notebook `CARS4U Action Recommendation - model` al progetto Watson Studio

- Scaricare il seguente file:

    - [CARS4U Action Recommendation - model ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- Dalla scheda **Asset** nel progetto Watson Studio, fare clic sul pulsante **Aggiungi al progetto** e selezionare **Notebook** dal menu a discesa:

  ![Aggiungi connessione](images/add_notebook.png)

- Selezionare **Da file**:

  ![Nuovo modulo notebook](images/new_notebook_name.png)

- Quindi, fare clic sul pulsante **Seleziona file** e selezionare il file "CARS4U Action Recommendation - model" scaricato:

  ![Nuovo modulo notebook](images/new_notebook_name2.png)

- Nella sezione **Seleziona runtime**, selezionare l'istanza Spark creata in precedenza dall'elenco a discesa:

  ![Runtime Spark](images/spark_runtime.png)

- Fare clic su **Crea notebook**.

### Modificare ed eseguire il notebook `CARS4U Action Recommendation - model`
{: #tadv-ern}

Il notebook `CARS4U Action Recommendation - model` contiene le istruzioni dettagliate per ciascuna fase nel codice python che si sta per eseguire. Durante l'esecuzione del notebook, è opportuno dedicare del tempo alla comprensione delle funzioni di ciascun comando.
{: tip}

- Dalla scheda **Asset** del progetto Watson Studio, fare clic sull'icona **Modifica** accanto al notebook `CARS4U Action Recommendation - model` per modificarlo.

- Nella sezione 2.2, "Caricamento dei dati sul database PostgreSQL", sostituire le credenziali del servizio Postgres con le credenziali create nella sezione precedente.

- Nella sezione 4, "Memorizzare il modello nel repository", nel campo **SUGGERIMENTO**, sostituire le credenziali di Watson Machine Learning con le credenziali create nella sezione precedente.

- Una volta immesse le credenziali, il notebook è pronto per l'esecuzione. Fare clic sulla voce di menu **Kernel** e selezionare **Riavvia ed esegui tutto** dal menu:

  ![Riavvia ed esegui](images/restart_and_run.png)

  Questa operazione creerà, eseguirà il training e la distribuzione di **CARS4U - Action Recommendation Model** nel progetto. È possibile verificare l'avvenuta distribuzione del modello selezionando la scheda **Distribuzioni** del progetto Watson Studio e facendo clic sul link **CARS4U - Area and Action Model Deployment**.

## Configurare {{site.data.keyword.aios_short}}
{: #tadv-config-aios}

### Eseguire il provisioning di {{site.data.keyword.aios_short}}
{: #tadv-paios}

- Se non è già stato eseguito il provisioning di un'istanza di {{site.data.keyword.aios_short}}, fare clic sul link **Catalogo** dall'account {{site.data.keyword.cloud_notm}} ed inserire il filtro "OpenScale". Selezionare il riquadro per {{site.data.keyword.aios_short}}.

<!---
  ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)
--->

- Fornire un nome al servizio, selezionare il piano Lite e fare clic su **Crea**.

### Connettere {{site.data.keyword.aios_short}} al modello di machine learning
{: #tadv-cmlm}

Poiché il modello di machine learning è già stato distribuito, è possibile configurare {{site.data.keyword.aios_short}} per garantire affidabilità e trasparenza per i modelli. Selezionare la scheda **Manage** dell'istanza {{site.data.keyword.aios_short}} e fare clic sul pulsante **Avvia applicazione**. Viene aperta la pagina Introduzione di {{site.data.keyword.aios_full}}; fare clic su **Inizia**.

- Selezionare il riquadro "Watson Machine Learning" e fare clic su **Avanti**.

  ![Imposta istanza WML](images/gs-wml-default.png)

- Selezionare l'istanza di Watson Machine Learning dal menu a discesa e fare clic su **Avanti**.

  ![Imposta istanza WML](images/gs-set-wml.png)

- Ora è possibile selezionare quali modelli distribuiti verranno monitorati da {{site.data.keyword.aios_short}}. Selezionare il modello creato e distribuito e fare clic su **Avanti** per accettare quanto segue:

  ![Seleziona modelli distribuiti](images/gs-set-deploy.png)

- Successivamente, è necessario selezionare un database PostgreSQL. Esistono due opzioni: il database del piano Lite gratuito o un database esistente o nuovo. Per questo supporto didattico, selezionare il riquadro **Utilizza il database esistente o acquistane uno nuovo**.

    ![Seleziona database](images/gs-set-lite-db1.png)

  È possibile visualizzare ulteriori dettagli su ciascuna di queste opzioni nell'argomento [Specifica di un database](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
  {: note}

- Se è stata selezionata l'opzione "Utilizza il database esistente o acquistane uno nuovo", {{site.data.keyword.aios_short}} controlla l'account {{site.data.keyword.cloud_notm}} per individuare eventuali database Compose for PostgreSQL esistenti.

  Selezionare lo schema "data_mart" dal menu a discesa **Schema**.

  ![Seleziona database](images/gs-set-schema1.png)

- Una volta selezionati il database e lo schema, fare clic su **Avanti** per esaminare i dati di riepilogo e fare clic su **Salva**.

  ![Seleziona database](images/gs-setup-summary3.png)

  Fare clic su **Passa al dashboard** quando richiesto.

## Creare un data mart e configurare i monitoraggi delle prestazioni, dell'accuratezza e della correttezza
{: #tadv-config-monitors}

### Aggiungere il notebook `{{site.data.keyword.aios_short}} and Watson ML engine` al progetto Watson Studio
{: #tadv-aomn}

Il notebook `{{site.data.keyword.aios_short}} and Watson ML engine` contiene le istruzioni dettagliate per ciascuna fase nel codice python che si sta per eseguire. Durante l'esecuzione del notebook, è opportuno dedicare del tempo alla comprensione delle funzioni di ciascun comando.
{: tip}

- Scaricare il seguente file:

    - [{{site.data.keyword.aios_short}} and Watson ML engine ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Dalla scheda **Asset** nel progetto Watson Studio, fare clic sul pulsante **Aggiungi al progetto** e selezionare **Notebook** dal menu a discesa:

  ![Aggiungi connessione](images/add_notebook.png)

- Selezionare **Da file**:

  ![Nuovo modulo notebook](images/new_notebook_name.png)

- Quindi, fare clic sul pulsante **Seleziona file** e selezionare il file "{{site.data.keyword.aios_short}} and Watson ML engine" scaricato:

  ![Nuovo modulo notebook](images/new_notebook_name3.png)

- Nella sezione **Seleziona runtime**, selezionare l'istanza Spark creata in precedenza dall'elenco a discesa:

  ![Runtime Spark](images/spark_runtime.png)

- Fare clic su **Crea notebook**.

### Modificare ed eseguire il notebook `{{site.data.keyword.aios_short}} and Watson ML engine`
{: #tadv-eromn}

- Dalla scheda **Asset** nel progetto Watson Studio, fare clic sull'icona **Modifica**accanto al notebook `{{site.data.keyword.aios_short}} and Watson ML engine` per modificarlo.

- Nella sezione 1.1, "Installazione e autenticazione":

    - In **AZIONE: richiama id_istanza (GUID) e chiave api**, completare la procedura per ottenere le credenziali. Sostituire `aios_credentials` con le proprie credenziali.

    - Successivamente, in **AZIONE: aggiungi le credenziali di Watson Machine Learning qui**, sostituire le credenziali di Watson Machine Learning con le credenziali create in precedenza.

    - Infine, in **AZIONE: aggiungi le credenziali PostgreSQL qui**, sostituire le credenziali Postgres con le credenziali create in precedenza.

- Una volta immesse le credenziali, il notebook è pronto per l'esecuzione. Fare clic sulla voce di menu **Kernel** e selezionare **Riavvia ed esegui tutto** dal menu:

  ![Riavvia ed esegui](images/restart_and_run.png)

  Questa operazione configurerà il data mart, abiliterà la registrazione del payload, configurerà e assegnerà i punteggi ai monitor delle prestazioni, dell'accuratezza e della correttezza e fornirà tali metriche all'istanza di {{site.data.keyword.aios_short}}.

## Visualizzazione dei risultati
{: #tadv-results}

### Visualizzare gli insight per la distribuzione
{: #tadv-vide}

Utilizzando il dashboard di [{{site.data.keyword.aios_short}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, fare clic sulla scheda **Insight**:

  ![Insight](images/insight-dash-tab.png)

La pagina Insight fornisce una panoramica delle metriche per i modelli distribuiti. È possibile visualizzare facilmente gli avvisi per le metriche Correttezza o Accuratezza che sono scese al di sotto della soglia impostata durante l'esecuzione del notebook (70%). I dati e le impostazioni utilizzati in questo supporto didattico avranno creato metriche per Accuratezza e Correttezza simili a quelle mostrate di seguito.

  ![Panoramica Insight](images/insight-overview-adv-tutorial.png)

### Visualizzare i dati di monitoraggio per la distribuzione
{: #tadv-vmdd}

Selezionare una distribuzione facendo clic sul riquadro nella pagina Insight. Vengono visualizzati i dati di monitoraggio per tale distribuzione. Scorrere il puntatore nel grafico per selezionare i dati per l'intervallo di tempo durante il quale è stato eseguito il notebook. Quindi, selezionare il link **Visualizza dettagli**.

  ![Monitoraggio dei dati](images/insight-monitor-data1.png)

Ora, è possibile esaminare i grafici per i dati monitorati. Per questo esempio, è possibile utilizzare il menu a discesa **Funzione** per selezionare "Figli" o "Genere" per visualizzare i dettagli sui dati monitorati.

  ![Panoramica Insight](images/insight-review-charts1.png)

<!---

### Visualizzare l'esplicabilità per una transazione del modello
{: #tadv-vemt}

Selezionare il pulsante **Visualizza transazioni** dai grafici per i dati monitorati.

  ![View transactions](images/view_transactions.png)

  viene mostrato un elenco delle transazioni per l'ultima ora. Copiare uno degli ID di transazione.

  ![Transaction list](images/transaction_list.png)

Utilizzando il dashboard [{{site.data.keyword.aios_short}} ![External link icon](../../icons/launch-glyph.svg "icona link esterno")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, fare clic sulla scheda **Esplicabilità**:

  ![Explainability](images/explainability.png)

Incollare il valore dell'ID di transazione copiato nella casella di ricerca e premere il tasto **Invio**. Verrà visualizzata una spiegazione del modo in cui il modello è giunto alla relativa conclusione, compresi il livello di confidenza del modello,  i fattori che hanno contribuito al livello di confidenza e gli attributi utilizzati dal modello.

  ![View Transaction](images/view_transaction1.png)

--->

## Passi successivi
{: #tadv-next}

- Ulteriori informazioni sulla [visualizzazione e interpretazione dei dati](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e sul [monitoraggio dell'esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
