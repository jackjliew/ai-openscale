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

In questo supporto didattico, verranno eseguite le seguenti attività:

- [Eseguire il provisioning di servizi di machine learning e storage di {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps).
- [Configurare un progetto Watson Studio e creare, eseguire il training e la distribuzione di un modello di machine learning](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup).
- [Configurare ed esplorare la fiducia, la trasparenza e l'esplicabilità del modello](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios).

## Eseguire il provisioning dei servizi {{site.data.keyword.Bluemix_notm}} prerequisiti
{: #gs-prps}

Oltre a {{site.data.keyword.aios_short}}, per completare questo supporto didattico, è necessario disporre dei seguenti account e servizi.

**Importante**: per prestazioni ottimali, si consiglia di creare i servizi prerequisiti nella stessa regione di {{site.data.keyword.aios_short}}. Per visualizzare le ubicazioni disponibili per {{site.data.keyword.aios_short}}, consultare [Disponibilità del servizio](/docs/resources?topic=resources-services_region).

1.  Accedere all'[account {{site.data.keyword.Bluemix_notm}}](https://{DomainName}){: external} con il proprio {{site.data.keyword.ibmid}}.
1.  Per ognuno dei seguenti servizi che non sono stati ancora associati al proprio account, creare un'istanza facendo clic sul link, fornendo un nome al servizio, selezionando il piano **Lite** (gratuito) e facendo clic sul pulsante **Crea**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Configurare un progetto Watson Studio
{: #gs-setup}

1.  Accedere all'[account Watson Studio](https://dataplatform.ibm.com/){: external} e iniziare con la creazione di un nuovo progetto. Fare clic su **Crea un progetto**.

    ![Crea progetto Watson Studio](images/studio_create_proj.png)

1.  Fare clic sul riquadro **Standard**.

    ![Seleziona progetto Standard Watson Studio](images/studio_create_standard.png)

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

1.  Ora è possibile selezionare i modelli distribuiti che verranno monitorati da {{site.data.keyword.aios_short}}. Selezionare il modello creato e fare clic su **Avanti**.

    ![Seleziona modelli distribuiti](images/wos-select-model-deployment.png)



### Fornire una serie di dati campione al modello
{: #gs-samp}

Prima di poter configurare i monitor, è necessario generare almeno una richiesta di punteggio al modello per generare la registrazione del payload che i monitor possono utilizzare. In questa sezione, l'utente fornirà i dati di esempio nel formato di un file JSON per generare una richiesta di punteggio.

1.  Scaricare il file [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  Dalla scheda **Distribuzioni** del progetto Watson Studio, fare clic sul link **credit-risk-deploy**, fare clic sulla scheda **Verifica** e selezionare l'icona di input JSON.

    ![Verifica JSON](images/json_test02.png)

1.  Ora, aprire il file `credit_payload_data.json` scaricato e copiare il contenuto nel campo JSON nella scheda **Verifica**. Fare clic sul pulsante **Previsione** per inviare e assegnare un punteggio ai payload di training al modello.

    ![Previsione JSON](images/json_test03.png)

### Preparazione al monitoraggio
{: #gs-prepmon}

1.  Ora, nell'istanza {{site.data.keyword.aios_short}}, selezionare la distribuzione e fare clic su **Inizia**.

    ![Seleziona distribuzione](images/wos-select-model-deployment.png)

1.  Specificare la funzione che contiene la risposta che il modello prevederà. (Nel database dell'utente, quale colonna della tabella contiene i valori delle previsioni o le etichette). In questo caso, il modello prevede il rischio di credito, pertanto selezionare la colonna **Rischio** e fare clic su **Avanti**.

    ![Preparazione per il monitoraggio](images/wos-select-model-deployment.png)

1.  Di seguito, l'utente fornirà le informazioni sul modello e sui dati di training. Fare clic su **Avanti**.

    ![Preparazione alla spiegazione](images/config-what-monitor.png)

1.  Dal menu **Tipo di dati**, selezionare **Numerico/di categoria** come il tipo di dati analizzato dalla distribuzione e fare clic su **Avanti**.

    ![Selezionare tipo di input](images/config-input-monitor.png)

1.  Per i dati numerici o di categoria, è necessario fornire le informazioni sui dati di training per il modello per poter configurare i monitor. Selezionare **Configura manualmente i monitor** per fornire le informazioni di connessione ai dati di training.

    ![Selezionare tipo di configurazione](images/config-manual-monitor.png)

1.  Il tipo di algoritmo è importante per il monitoraggio delle metriche del modello, ad esempio l'Accuratezza. Poiché la previsione che il modello è in grado di produrre è "Rischio" o "Nessun rischio", selezionare il [tipo di algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) **Classificazione binaria** e fare clic su **Avanti**.

    ![Binaria](images/binary.png)

1.  Le informazioni sull'ubicazione per i dati di esempio vengono prepopolate nella seguente schermata. Selezionare **Avanti** per continuare.

    ![Specifica ubicazione Db2 della pagina dei dati di training](images/gs-config-train-db2-monitor.png)

1.  Anche lo schema e la tabella sono prepopolati. Fare clic su **Avanti** per proseguire.

    ![Specifica ubicazione Db2 dello schema e della tabella di training](images/gs-fair-config-table-db2.png)

1.  Ora, è necessario specificare la funzione che contiene le risposte che il modello prevederà (ovvero, nel database dell'utente, quale colonna della tabella contiene i valori delle previsioni (etichette)). In questo caso, il modello prevederà il rischio di credito, pertanto selezionare la colonna **Rischio** e fare clic su **Avanti**.

    Il database di training ha i valori forniti per il training del modello.
    {: note}

    ![Previsione dell'input dell'etichetta](images/gs-config-label.png)

1.  Selezionare le colonne utilizzate per il training del modello. Si tratta dei dati che la distribuzione del modello necessita in una richiesta. Tutte le colonne di dati, eccetto `_training`, sono input per il modello. Selezionare tutti gli altri input e fare clic su **Avanti**.

    ![Input di esplicabilità](images/explain_inputs1.png)

1.  Per i dati di categoria, è necessario identificare le colonne che ora contengono numeri interi, ma che in origine contenevano valori di testo. Selezionare i valori come mostrato di seguito.

    ![Input di esplicabilità](images/config_categories.png)

1.  Esaminare il riepilogo delle selezioni, fare clic su **Salva**, quindi fare clic su **OK**.

### Configurare il monitoraggio della correttezza
{: #gs-cfgfair}

1.  Fare clic su **Correttezza**.

1.  Leggere le informazioni sulla correttezza e fare clic su **Avanti**. Per ulteriori informazioni, consultare [Correttezza](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

1.  Ora è possibile selezionare quali funzioni monitorare per la correttezza. Per ciascuna funzione selezionata, {{site.data.keyword.aios_short}} monitorerà la propensione del modello distribuito per un risultato favorevole per un gruppo rispetto all'altro. In questo esempio, verranno monitorate le funzioni **Sesso** ed **Età** .

    Le funzioni vengono monitorate individualmente, ma qualsiasi annullamento di distorsione correggerà gli errori per tutte le funzioni complessivamente. Fare clic sui riquadri **Sesso** ed **Età** e fare clic su **Avanti**.

1.  {{site.data.keyword.aios_short}} esegue il rilevamento della distorsione rispetto a un gruppo monitorato, confrontandolo con un gruppo di riferimento. Per la funzione **Sesso**, aggiungere il valore `maschile` al **Gruppo di riferimento** e il valore `femminile` al **Gruppo monitorato** quindi fare clic su **Avanti**.

    Il modello verrà contrassegnato come con distorsione per il **Sesso** se i rapporti di previsione del rischio per il gruppo monitorato differiscono dai rapporti per il gruppo di riferimento. Pertanto, se il modello prevede Rischio per i clienti di sesso maschile il 60% delle volte e per i clienti di sesso femminile il 20% delle volte, è presente una distorsione.

    ![Gruppi di genere](images/gender_groups1.png)

1.  Assegnare una soglia di correttezza per il **Sesso**. Il dashboard delle operazioni visualizza un avviso se il tasso correttezza supera la soglia impostata. Impostare la soglia al 90%, quindi fare clic su **Avanti**.

1.  Per la funzione **Età**, aggiungere i valori `26-74` al **Gruppo di riferimento** e i valori `19-25` al **Gruppo monitorato**, quindi fare clic su **Avanti**.

    Come con il **Sesso**, il modello verrò contrassegnato come con distorsione per l'**Età** se i rapporti di previsione del rischio per il gruppo monitorato differiscono dai rapporti per il gruppo di riferimento. Pertanto, se i clienti con età comprese tra 26 e 74 anni ricevono una previsione di rischio con un rapporto differente rispetto ai clienti con età comprese tra 19 e 25 anni, il modello presenta una distorsione.

    ![Gruppi BP](images/age_groups.png)

1.  Impostare la soglia per l'**Età** al 90%, quindi fare clic su **Avanti**.

1.  Trascinare e rilasciare i valori dal campo **Valori dai dati di training** nei campi **Valori favorevoli** e **Valori sfavorevoli**. Per questo supporto didattico, il valore favorevole è **Nessun rischio** e il valore sfavorevole è **Rischio**. Fare clic su **Avanti**.

    {{site.data.keyword.aios_short}} rileva automaticamente quale colonna nel database di registrazione del payload contiene i valori di previsione e li presenta nel campo **Valori dai dati di training**. Tenere presente che, mentre il database di training contiene i valori forniti per il training del modello, il database di registrazione del payload contiene i dati di feedback raccolti durante il runtime del modello, che è facoltativamente possibile utilizzare per eseguire nuovamente il training e la distribuzione del modello.
    {: note}

    ![Valori positivi e negativi](images/pos_and_neg2.png)

1.  Utilizzare il dispositivo di scorrimento per modificare la dimensione minima del campione su 100, quindi fare clic su **Avanti**.

    ![Dimensione minima](images/gs-fair-config-sample.png)

    Per questo supporto didattico, la dimensione minima del campione è impostata su 100. Di norma, è consigliata una dimensione del campione maggiore per evitare che i risultati vengano alterati da una dimensione del campione troppo piccola.
    {: note}

1.  Esaminare le selezioni effettuate, fare clic su **Salva**, quindi fare clic su **OK**.

    ![Riepilogo della configurazione](images/fair-summary.png)

    Viene visualizzata la seguente finestra, che fornisce un endpoint di calcolo del punteggio con distorsione annullata. Poiché questo supporto didattico utilizza il metodo GUI e non la CLI per assegnare i punteggi ai dati, fare clic su **OK** per proseguire.

    ![API di annullamento della distorsione](images/gs-insight-debias-api.png)

### Configurare il monitoraggio dell'accuratezza
{: #gs-cfgac}

1.  Fare clic su **Accuratezza**.

1.  Leggere le informazioni sull'accuratezza e fare clic su **Avanti**. Per ulteriori informazioni, consultare [Accuratezza](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

1.  Impostare la soglia di avviso dell'accuratezza al 90% e fare clic su **Avanti**.

1.  Nella schermata successiva, utilizzare il dispositivo di scorrimento per modificare la dimensione minima del campione su 10, quindi fare clic su **Avanti**.

    Per questo supporto didattico, la dimensione minima del campione è stata impostata su 10. Di norma, è consigliata una dimensione del campione maggiore per evitare che i risultati vengano alterati da una dimensione del campione troppo piccola.
    {: note}

1.  Per la dimensione massima del campione, utilizzare 10000. Fare clic su **Avanti**.

1.  Esaminare le selezioni effettuate, fare clic su **Salva**, quindi fare clic su **OK**.

1.  Infine, viene presentata l'opzione di aggiungere i dati di feedback, che verranno illustrati nella sezione successiva. Per ora, chiudere la finestra facendo clic su **OK**, senza fare clic sul pulsante **Aggiungi dati di feedback**.

    Per ulteriori dettagli, consultare [Configurazione del monitor Accuratezza](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config).

## Fornire una serie di dati di feedback di esempio al modello
{: #gs-smpfeed}

Per abilitare il monitoraggio dell'accuratezza, è necessario fornire al modello i dati di feedback. I dati sull'accuratezza non verranno visualizzati nel dashboard fino a quando non viene completata questa operazione. È possibile generare tutte le richieste simultaneamente aggiungendo dati di feedback di esempio al modello per l'assegnazione del punteggio. Per questa attività, verrà scaricato un file CSV che contiene i dati di feedback di esempio.

1.  Scaricare il file [credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv).

1.  In {{site.data.keyword.aios_short}}, fare clic sulla scheda **Insight**.

    ![Insight](images/insight-dash-tab.png)

1.  Fare clic sul riquadro per il modello distribuito.

    ![Scheda insight - nessun dato](images/gs-insight-overview.png)

1.  Fare clic su **Configura monitor**.

    ![Icona modifica](images/gs-insight-edit-icon.png)

1.  Fare clic su **Accuratezza**, quindi su **Feedback**.
1.  Fare clic sul pulsante **Aggiungi dati di feedback** e selezionare il file `accredit_feedback_data.csv` scaricato e fare clic su **Apri**. 
2. Selezionare il delimitatore **Virgola (,)** e fare clic su **Seleziona**.

    Attualmente, le dimensioni dei file sono limitate a 8 MB.
    {: note}

    ![Delimitatore accuratezza](images/accuracy-delimit.png)

L'aggiunta del file CSV fornisce i dati di feedback al modello.

## Configurare il monitor Deviazione
{: gs-drift-config}

Per informazioni su come configurare il monitor Deviazione, consultare [Configurare il monitor di rilevamento deviazione](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

## Visualizzazione dei risultati
{: #gs-viewres}

Dopo aver configurato il monitoraggio dell'accuratezza, la verifica dell'accuratezza viene eseguita dopo un'ora. In un sistema di produzione, ciò consente al dashboard di accumulare i dati di feedback. Ai fini di questo supporto didattico, è consigliabile attivare manualmente la verifica dell'accuratezza dopo aver aggiunto i dati di feedback, per consentire la visualizzazione dei risultati nel dashboard **Insight**.

Per verificare immediatamente i risultati, dalla pagina **Insight**, selezionare una distribuzione e fare clic su **Controlla correttezza ora** o **Controlla qualità ora**.

Per conoscere comeinterpretare i risultati, consultare [Acquisizione degli insight](/docs/services/ai-openscale?topic=ai-openscale-io-ov)

## Informazioni correlate
{: #wos-info}

- Per informazioni sulle distorsioni, consultare [Correttezza](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor).
- Per informazioni sulla bontà dei risultati previsionali del modello, consultare [Accuratezza](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- Per informazioni sull'interpretazione di grafici, dati e transazioni, consultare [Monitoraggio della correttezza, Richieste medie al minuto e Accuratezza](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).
