---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, fast start

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

# Supporto didattico interattivo per la configurazione
{: #gs-obj}

In questo supporto didattico, si impara a eseguire il provisioning dei servizi {{site.data.keyword.Bluemix_notm}} richiesti, configurare un progetto e distribuire un modello di esempio in Watson Studio e configurare i monitor in {{site.data.keyword.aios_short}}.
{: shortdesc}

1. [Eseguire il provisioning di servizi di machine learning e storage di {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps).
2. [Configurare un progetto Watson Studio e creare, eseguire il training e la distribuzione di un modello di machine learning](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup).
3. [Configurare ed esplorare la fiducia, la trasparenza e l'esplicabilità del modello](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios).

## Eseguire il provisioning dei servizi {{site.data.keyword.Bluemix_notm}} prerequisiti
{: #gs-prps}

Oltre a {{site.data.keyword.aios_short}}, per completare questo supporto didattico, è necessario disporre dei seguenti account e servizi.

**Importante**: per prestazioni ottimali, si consiglia di creare i servizi prerequisiti nella stessa regione di {{site.data.keyword.aios_short}}. Per visualizzare le ubicazioni disponibili per {{site.data.keyword.aios_short}}, consultare [Disponibilità del servizio](/docs/resources?topic=resources-services_region){: external}.

1.  Accedere all'[account {{site.data.keyword.Bluemix_notm}}](https://{DomainName}){: external} con il proprio {{site.data.keyword.ibmid}}.
1.  Per ognuno dei seguenti servizi che non sono stati ancora associati al proprio account, creare un'istanza facendo clic sul link, fornendo un nome al servizio, selezionando il piano **Lite** (gratuito) e facendo clic sul pulsante **Crea**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Configurare un progetto Watson Studio
{: #gs-setup}

1.  Accedere all'[account Watson Studio](https://dataplatform.ibm.com/){: external} e iniziare con la creazione di un nuovo progetto. Fare clic su **Crea un progetto**.

    ![Crea progetto Watson Studio](images/studio_create_proj.png)

1.  Fare clic sul riquadro **Crea un progetto vuoto**.
1.  Fornire un nome e una descrizione al progetto, accertarsi che il servizio Object Storage creato nel passo precedente sia selezionato nel menu **Storage** e fare clic su **Crea**.

### Associare i servizi {{site.data.keyword.Bluemix_notm}} al progetto Watson
{: #gs-assoc}

1.  Aprire il progetto Watson Studio e selezionare la scheda **Impostazioni**. Nella sezione **Servizi associati**, fare clic su **Aggiungi servizio** e quindi fare clic su **Watson**.

    ![Aggiungi servizio Watson](images/add_watson_service.png)

1.  Fare clic sul link **Aggiungi** nel riquadro **Machine Learning**.
2.  Nella scheda **Esistente**, dall'elenco a discesa **Istanza di servizio esistente**, fare clic sul servizio creato in precedenza.
3. Fare clic su **Seleziona**.

### Aggiungere il modello `Rischio di credito`
{: #gs-addmod}

1.  In {{site.data.keyword.DSX}}, selezionare la scheda **Asset** del progetto, scorrere fino alla sezione **Modelli di Watson Machine Learning** e fare clic sul pulsante **Nuovo modello di Watson Machine Learning**.

1.  Dalla sezione **Seleziona tipo di modello**, selezionare **Da campione** e il modello `Rischio di credito`, quindi fare clic su **Crea**.

    ![Viene visualizzato il riquadro rischio di credito](images/credit-sample-model.png)

### Distribuire il modello `Rischio di credito`
{: #gs-depmod}

1.  Dalla pagina di modello `Rischio di credito`, fare clic sulla scheda **Distribuisci**, quindi su **Aggiungi distribuzione**.
1.  Immettere `credit-risk-deploy` come nome della distribuzione e selezionare il tipo di distribuzione **Servizio web**.
1.  Fare clic su **Salva**.

## Configurare {{site.data.keyword.aios_short}}
{: #gs-confaios}

Una volta distribuito il modello di machine learning, è possibile configurare {{site.data.keyword.aios_short}} per garantire affidabilità e trasparenza per i modelli.

### Eseguire il provisioning di {{site.data.keyword.aios_short}}
{: #gs-provaios}

1.  [Eseguire il provisioning di una nuova istanza del servizio {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  Fornire un nome al servizio, selezionare il **piano Lite** e fare clic su **Crea**.

1.  Selezionare la scheda **Manage** dell'istanza {{site.data.keyword.aios_short}} e fare clic sul pulsante **Avvia applicazione**. Viene aperta la pagina della demo **Benvenuti in {{site.data.keyword.aios_short}}**.
2. Per questo supporto didattico, fare clic su **No Grazie**.

### Selezionare un database
{: #gs-db-choice}

Successivamente, è necessario selezionare un database. Esistono due opzioni: il database gratuito o un database esistente o nuovo.

2. Per questo supporto didattico, selezionare il riquadro **Utilizza il database gratuito del piano Lite**.

   Il database gratuito ha alcune limitazioni importanti. Si tratta di un database ospitato che non fornisce accesso separato ad esso. Fornisce accesso {{site.data.keyword.aios_short}} al proprio database e ai dati. Non è conforme al GDPR. È possibile visualizzare ulteriori dettagli su ciascuna di queste opzioni nell'argomento [Specifica di un database](/docs/services/ai-openscale?topic=ai-openscale-connect-db). Il database esistente può essere un database PostgreSQL o Db2.
    {: tip}

   ![Selezionare il database](images/gs-set-lite-db2.png)

1.  Esaminare il riepilogo e fare clic su **Salva**. Confermare e, quando richiesto, fare clic sul pulsante **Continua con la configurazione**.

    Viene elencato anche un ID Data Mart, che è identico a un ID istanza di {{site.data.keyword.aios_short}}.
    {: tip}

    ![Revisione riepilogo](images/gs-setup-summary4.png)

1.  La schermata visualizzata potrebbe essere simile alla seguente. Poiché verrà utilizzato un metodo GUI per assegnare un punteggio ai dati, è sufficiente selezionare il pulsante **Configura monitor** per completare questa configurazione. 

    ![Codice richiesta di calcolo del punteggio](images/gs-config-send-scoring.png)

### Connettere {{site.data.keyword.aios_short}} al modello di machine learning
{: #gs-ctmod}


1.  Fare clic sul riquadro **Watson Machine Learning**, quindi su **Salva**.

1.  Per questo supporto didattico, selezionare l'istanza di {{site.data.keyword.pm_full}} dal menu e fare clic su **Avanti**.

    È anche possibile selezionare un'ubicazione di {{site.data.keyword.pm_short}} differente. Per ulteriori informazioni, consultare [Specifica di un'istanza del servizio {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-wml-connect).
    {: note}

    ![Configurare l'istanza {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

Ora è possibile selezionare i modelli distribuiti che verranno monitorati da {{site.data.keyword.aios_short}}.


### Fornire una serie di dati campione al modello
{: #gs-samp}

Prima di poter configurare i monitor, è necessario generare almeno una richiesta di punteggio al modello per generare la registrazione del payload che i monitor possono utilizzare. In questa sezione, l'utente fornirà i dati di esempio a Watson Studio nel formato di un file JSON per generare una richiesta di punteggio. 

1.  Scaricare il file [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  Dalla scheda **Distribuzioni** del progetto Watson Studio, fare clic sul link **credit-risk-deploy**, fare clic sulla scheda **Verifica** e selezionare l'icona di input JSON.

    ![Verifica JSON](images/json_test02.png)

1.  Ora, aprire il file `credit_payload_data.json` scaricato e copiare il contenuto nel campo JSON nella scheda **Verifica**. Fare clic sul pulsante **Previsione** per inviare e assegnare un punteggio ai payload di training al modello.

    ![Previsione JSON](images/json_test03.png)

## Passi successivi
{: #gs-next-steps-config}

Continuare con questo supporto didattico completando i seguenti passi:

1. [Preparare i monitor per la distribuzione](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy).

   Per preparare i monitor, è necessario selezionare uno dei modelli distribuiti e aggiungerlo al dashboard. Dalla scheda **Insight**, fare clic su un riquadro, o fare clic sul pulsante **Aggiungi al dashboard** per selezionare un modello distribuito e fare clic su **Configura**.

2. [Configurare la registrazione payload](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data).

   Nella sezione **Registrazione payload**, occorre specificare il tipo di input.

3. [Configurare i dettagli del modello](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets).

   Nella sezione **Dettagli modello**, occorre registrare i dettagli del modello. Per questo supporto didattico selezionare **Configura manualmente i monitor**.

4. [Configurare il monitoraggio della qualità](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

   Nella sezione **Qualità**, impostare la soglia di avviso per la qualità e le dimensioni del campione.

5. [Configurare il monitoraggio della correttezza](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

   Nella sezione **Correttezza**, selezionare quali funzioni monitorare per la correttezza. Per ciascuna funzione selezionata, {{site.data.keyword.aios_short}} monitorerà la propensione del modello distribuito per un risultato favorevole per un gruppo rispetto all'altro. Sebbene le funzioni vengano monitorate individualmente, qualsiasi annullamento di distorsione corregge gli errori per tutte le funzioni complessivamente. 

6. [Configurare il monitor di rilevamento della deviazione](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

   Nella sezione **Deviazione**, configurare un modello di rilevamento della deviazione.
   
5. [Fornire una serie di dati di feedback di esempio al modello](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv).

   Per abilitare il monitoraggio della qualità, è necessario fornire al modello i dati di feedback. I dati sulla qualità non verranno visualizzati nel dashboard fino a quando non viene completata questa operazione. È possibile generare tutte le richieste simultaneamente aggiungendo dati di feedback di esempio al modello per l'assegnazione del punteggio. Per questa attività, verrà scaricato un file CSV che contiene i dati di feedback di esempio.

6. [Acquisire gli insight](/docs/services/ai-openscale?topic=ai-openscale-io-ov).

   Dopo aver configurato il monitoraggio dell'accuratezza, la verifica dell'accuratezza viene eseguita dopo un'ora. In un sistema di produzione, ciò consente al dashboard di accumulare i dati di feedback. Ai fini di questo supporto didattico, è consigliabile attivare manualmente la verifica dell'accuratezza dopo aver aggiunto i dati di feedback, per consentire la visualizzazione dei risultati nel dashboard **Insight**.

   Per verificare immediatamente i risultati, dalla pagina **Insight**, selezionare una distribuzione, fare clic su una delle metriche **Qualità** e fare clic su **Controlla qualità ora**.
