---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Supporto didattico per l'SDK Python (avanzato)
{: #crt-ov}

## Scenario
{: #crt-scenario}

I finanziatori tradizionali sono sottoposti a forti pressioni per espandere il proprio portafoglio digitale di servizi finanziari per un pubblico più ampio e diversificato, il che richiede un nuovo approccio alla creazione di modelli di rischio di credito. Al momento, i loro team di data science fanno affidamento sulle tecniche di creazione di modelli standard, quali ad esempio gli alberi decisionali e la regressione logistica, che sono adeguati per i dataset di dimensioni contenute e producono suggerimenti facilmente spiegabili. Ciò soddisfa i requisiti normativi, secondo i quali le decisioni relative ai prestiti debbano essere trasparenti e facilmente spiegabili.

Per fornire l'accesso al credito a una popolazione più ampia e maggiormente soggetta a rischi è necessario espandere le informazioni storiche sul credito dei richiedenti oltre il credito tradizionale, come i mutui e i finanziamenti per le automobili, per includere fonti di credito alternative quali gli storici dei pagamenti per le utenze e i piani tariffari telefonici, in aggiunta ai titoli di studio e lavorativi. Queste nuove fonti di dati sono promettenti, ma introducono nuovi rischi aumentando la probabilità di correlazioni impreviste, che introducono una distorsione basata sull'età, il genere o altre caratteristiche personali del richiedente.

Le tecniche di data science più idonee a questi dataset così diversificati, quali le strutture ad albero con potenziamento dei gradienti e le reti neurali, possono generare modelli di rischio altamente accurati ma costosi. Modelli "scatola nera" di questo tipo generano previsioni poco chiare, che in qualche modo devono essere rese trasparenti per garantire la conformità a normative quali l'Articolo 22 del GDPR (General Data Protection Regulation), o al FCRA (Fair Credit Reporting Act) federale gestito dal Consumer Financial Protection Bureau.

Il modello rischio di credito fornito in questo supporto didattico utilizza un dataset di training che contiene 20 attributi relativi a ciascuno dei richiedenti di un prestito. È possibile verificare la distorsione per due di questi attributi, l'età e il sesso. Per questo supporto didattico, l'attenzione sarà rivolta alla distorsione rispetto a età e sesso. Per ulteriori informazioni sui dati di training, consultare [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

{{site.data.keyword.aios_short}} monitorerà la propensione del modello distribuito per un risultato favorevole ("Nessun rischio") per un gruppo (il gruppo di riferimento) rispetto a un altro (il gruppo monitorato). In questo supporto didattico, il gruppo monitorato per il sesso è `femminile`, mentre il gruppo monitorato per l'età è `da 18 a 25`.

## Prerequisiti
{: #crt-prereqs}

Questo supporto didattico utilizza un notebook Jupyter da eseguire in un progetto Watson Studio, utilizzando un ambiente di runtime "Python 3.5 with Spark". Richiede le credenziali di servizio per i seguenti servizi {{site.data.keyword.cloud_notm}}:

- Storage Object Storage (per memorizzare il progetto Watson Studio)
- {{site.data.keyword.aios_short}}
- Watson Machine Learning
- (Facoltativo) Databases for PostgreSQL o Db2 Warehouse

Il notebook Jupyter addestra, crea e distribuisce un modello German Credit Risk, configura {{site.data.keyword.aios_short}} per monitorare quella distribuzione e fornire sette giorni di record cronologici e misurazioni per la visualizzazione nel dashboard Insight di {{site.data.keyword.aios_short}}. È anche possibile, facoltativamente, configurare il continuous learning con Watson Studio e Spark.

## Introduzione
{: #crt-intro}

In questo supporto didattico, verranno svolte le seguenti attività:

- Eseguire il provisioning di servizi di machine learning e storage di {{site.data.keyword.cloud_notm}}
- Configurare un progetto Watson Studio ed eseguire un notebook Python per creare, eseguire il training e la distribuzione di un modello di machine learning
- Eseguire un notebook Python per creare un data mart, configurare i monitor delle prestazioni, dell'accuratezza e della correttezza e creare dati da monitorare
- Visualizzare i risultati nella scheda Insight di {{site.data.keyword.aios_short}}

## Eseguire il provisioning di servizi {{site.data.keyword.cloud_notm}}
{: #crt-services}

Accedere all'account [{{site.data.keyword.cloud_notm}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}){: new_window} con l'{{site.data.keyword.ibmid}}. Quando si esegue il provisioning dei servizi, in particolare se si utilizza Db2 Warehouse, verificare che l'organizzazione e lo spazio selezionati siano identici per tutti i servizi.

### Creare un account {{site.data.keyword.DSX}}
{: #crt-wstudio}

- [Creare un'istanza di {{site.data.keyword.DSX}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/watson-studio){: new_window} se non si dispone già di un'istanza associata all'account:

  ![Watson Studio](images/watson_studio.png)

- Fornire un nome al servizio, selezionare il piano Lite (gratuito) e fare clic sul pulsante **Crea**.

### Eseguire il provisioning di un servizio {{site.data.keyword.cos_full_notm}}
{: #crt-cos}

- [Eseguire il provisioning di un servizio {{site.data.keyword.cos_short}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} se non si dispone già di un servizio associato all'account:

  ![Object Storage](images/object_storage.png)

- Fornire un nome al servizio, selezionare il piano Lite (gratuito) e fare clic sul pulsante **Crea**.

### Eseguire il provisioning di un servizio {{site.data.keyword.pm_full}}
{: #crt-wml}

- [Eseguire il provisioning di un'istanza {{site.data.keyword.pm_short}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/machine-learning){: new_window} se non si dispone già di un servizio associato all'account:

  ![Machine Learning](images/machine_learning.png)

- Fornire un nome al servizio, selezionare il piano Lite (gratuito) e fare clic sul pulsante **Crea**.

### (Facoltativo) Eseguire il provisioning di un servizio Databases for PostgreSQL o DB2 Warehouse
{: #crt-db2}

Se si dispone di un account {{site.data.keyword.cloud_notm}} a pagamento, è possibile fornire un servizio `Databases for PostgreSQL` o `Db2 Warehouse` per sfruttare tutti i vantaggi dell'integrazione con {{site.data.keyword.DSX}} e i servizi di continuous learning. Se si sceglie di non fornire un servizio a pagamento, è possibile utilizzare lo storage interno PostgreSQL gratuito con {{site.data.keyword.aios_short}}, ma non sarà possibile configurare il continuous learning per il modello.

- [Eseguire il provisioning di un servizio Databases for PostgreSQL ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/databases-for-postgresql) o [di un servizio Db2 Warehouse ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://{DomainName}/catalog/services/db2-warehouse) se non si dispone già di un servizio associato all'account:

  ![DB for Postgres](images/dbpostgres.png)

  ![Db2 Warehouse](images/db2_warehouse.png)

- Fornire un nome al servizio, selezionare il piano Standard (Databases for PostgreSQL) o il piano Entry (Db2 Warehouse) e fare clic sul pulsante **Crea**.

## Configurare un progetto {{site.data.keyword.DSX}}
{: #crt-set-wstudio}

- Accedere all'account [{{site.data.keyword.DSX}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://dataplatform.ibm.com/){: new_window}. Fare clic su {{site.data.keyword.avatar}} e verificare che l'account che si sta utilizzando sia lo stesso account utilizzato per creare i servizi {{site.data.keyword.cloud_notm}}:

  ![Stesso account](images/same_account.png)

- In {{site.data.keyword.DSX}}, iniziare creando un nuovo progetto. Selezionare "Crea un progetto":

  ![Crea progetto Watson Studio](images/studio_create_proj.png)

- Selezionare il riquadro **Standard** per creare il progetto:

  ![Seleziona progetto Standard Watson Studio](images/studio_create_standard.png)

- Fornire un nome e una descrizione al progetto, accertarsi che il servizio Cloud Object Storage creato sia selezionato nel menu a discesa **Storage** e fare clic su **Crea**.

## Creare e distribuire un modello di {{site.data.keyword.pm_short}}
{: #crt-make-model}

### Aggiungere il notebook `Working with Watson Machine Learning` al progetto {{site.data.keyword.DSX}}
{: #crt-add-notebook}

- Scarica il seguente file:

    - [Working with Watson Machine Learning ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Dalla scheda **Asset** nel progetto {{site.data.keyword.DSX}}, fare clic sul pulsante **Aggiungi al progetto** e selezionare **Notebook** dal menu a discesa:

  ![Aggiungi connessione](images/add_notebook.png)

- Selezionare **Da file**:

  ![Nuovo modulo notebook](images/new_notebook_name.png)

- Quindi, fare clic sul pulsante **Seleziona file** e selezionare il file notebook "german_credit_lab.ipynb" scaricato:

  ![Nuovo modulo notebook](images/new_notebook_name2a.png)

- Nella sezione **Seleziona runtime**, selezionare un'opzione Python 3.5 with Spark:

- Fare clic su **Crea notebook**.

### Modificare ed eseguire il notebook `Working with Watson Machine Learning`
{: #crt-edit-notebook}

Il notebook `Working with Watson Machine Learning` contiene le istruzioni dettagliate per ciascuna fase nel codice Python che si sta per eseguire. Durante l'esecuzione del notebook, è opportuno dedicare del tempo alla comprensione delle funzioni di ciascun comando.
{: tip}

- Dalla scheda **Asset** nel progetto Watson Studio, fare clic sull'icona **Modifica** accanto al notebook `Working with Watson Machine Learning` per modificarlo.

- Nella sezione "Eseguire il provisioning dei servizi e configurare le credenziali", effettuare le seguenti modifiche:

    - Seguire le istruzioni per creare, copiare e incollare una chiave API {{site.data.keyword.cloud_notm}}.

    - Sostituire le credenziali del servizio WML (Watson Machine Learning) con quelle create in precedenza.

    - Sostituire le credenziali DB con quelle create per Databases for PostgreSQL.

    - Se in precedenza è stato configurato {{site.data.keyword.aios_short}} per utilizzare un database interno PostgreSQL gratuito come data mart, è possibile passare a un nuovo data mart che utilizza il proprio servizio Databases for PostgreSQL. Per eliminare la vecchia configurazione PostgreSQL e crearne una nuova, impostare la variabile KEEP_MY_INTERNAL_POSTGRES su `False`.

        Il notebook rimuoverà il data mart PostgreSQL interno esistente e creerà un nuovo data mart con le credenziali DB fornite. **Non si verificherà alcuna migrazione dei dati**.
        {: important}

- Una volta eseguito il provisioning dei servizi e immesse le credenziali, il notebook è pronto per l'esecuzione. Fare clic sulla voce di menu **Kernel** e selezionare **Riavvia & cancella output** dal menu:

  ![Riavvia e cancella](images/restart_and_clear.png)

- Ora, eseguire ogni passo del notebook in sequenza. Notare cosa succede a ogni passo, come descritto. Completare tutti i passi, fino a e inclusi i passi nella sezione "Ulteriori dati per aiutare il debugging".

Il risultato finale è la creazione, addestramento e distribuzione del modello **Spark German Risk Deployment** nell'istanza del servizio {{site.data.keyword.aios_short}}. {{site.data.keyword.aios_short}} verrà configurato per controllare la distorsione del modello rispetto a sesso (in questo caso femminile) o età (in questo caso, da 18 a 25 anni).

## Visualizzazione dei risultati
{: #crt-view-results}

### Visualizzare gli insight per la distribuzione
{: #crt-view-insights}

Utilizzando il dashboard [{{site.data.keyword.aios_short}} ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, fare clic sulla scheda **Insight**:

  ![Insight](images/insight-dash-tab.png)

La pagina Insight fornisce una panoramica delle metriche per i modelli distribuiti. È possibile visualizzare facilmente gli avvisi per le metriche Correttezza o Accuratezza che sono scese al di sotto della soglia impostata quando si esegue il notebook. Per i dati e le impostazioni utilizzati in questo supporto didattico verranno create le metriche Accuratezza e Correttezza simili a quelle mostrate qui.

  ![Panoramica su Insight](images/insight-overview-adv-tutorial-2.png)

### Visualizzare i dati di monitoraggio per la distribuzione
{: #crt-view-mon-data}

1. Per visualizzare i dettagli di monitoraggio, dalla pagina **Insight**, fare clic sul riquadro che corrisponde alla distribuzione. Vengono mostrati i dati di monitoraggio per tale distribuzione. 
2. Scorrere il puntatore nel grafico per selezionare i dati per una finestra di un'ora specifica. 
3. Fare clic sul link **Visualizza dettagli**.

  ![Monitoraggio dati](images/insight-monitor-data2.png)

Ora, è possibile esaminare i grafici per i dati monitorati. Per questo esempio è possibile vedere che per la funzione "Sesso", il gruppo `femmine` ha ricevuto il risultato favorevole  "Nessun rischio" inferiore del (68%) rispetto al gruppo `maschi` (78%).

  ![Panoramica su Insight](images/insight-review-charts2.png)

### Visualizzare l'esplicabilità per una transazione del modello
{: #crt-view-explain}

Per ogni distribuzione, è possibile vedere i dati di esplicabilità per transazioni specifiche.

Se si sa già quale transazione si desidera visualizzare, un modo veloce per cercarla è con l'ID transazione. Dopo aver fatto clic sul riquadro di distribuzione, dal navigator, fare clic sull'icona **Spiega una transazione**![scheda Spiega una transazione](images/insight-transact-tab.png), immettere l'ID transazione e premere **Invio**.
{: tip}

Se si utilizza la versione lite interna di PostgreSQL, potrebbe non essere possibile richiamare le credenziali del database. Questo potrebbe impedire la visualizzazione delle transazioni.
{: note}

1. Dai grafici per i dati distorti più recenti, fare clic sul pulsante **Visualizza transazioni**.

  ![Visualizza transazioni](images/view_transactions.png)

  Viene visualizzato un elenco delle transazioni in cui la distribuzione ha contribuito alla distorsione. 
  
2. Selezionare una delle transazioni e, dalla colonna **AZIONE**, fare clic sul link **Spiega**.

  ![Elenco transazioni](images/transaction_list_cr.png)

Viene visualizzata una spiegazione di come il modello è arrivato alla sua conclusione, incluso il livello di confidenza del modello, i fattori che hanno contribuito al livello di confidenza e gli attributi forniti al modello.

  ![Visualizza transazione](images/view_transaction_cr.png)
  
## Passi successivi
{: #crt-next-steps}

- Ulteriori informazioni sulla [visualizzazione e interpretazione dei dati](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e sul [monitoraggio dell'esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
