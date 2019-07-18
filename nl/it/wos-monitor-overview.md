---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: deployment, monitors, data

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

# Preparazione dei monitor per una distribuzione
{: #mo-config}

Configurare e abilitare i monitor per ogni distribuzioni di cui si sta tenendo traccia con {{site.data.keyword.aios_short}}.
{: shortdesc}

## Selezione di una distribuzione
{: #mo-select-deploy}

1. Dalla scheda **Insight**, fare clic sul pulsante **Aggiungi distribuzioni**. 

   ![Pagina Seleziona distribuzione](images/config-select-deploy.png)

   Viene visualizzato un elenco di distribuzioni di modelli disponibili.

   ![Preparazione per il monitoraggio](images/wos-select-model-deployment.png)

2. Fare clic su una distribuzione di modello, quindi su **Configura**.

   Se ci sono più distribuzioni per un dato modello, quando si configura una distribuzione, vengono configurate anche tutte le altre distribuzioni per lo stesso modello.

   Dopo che le selezioni vengono salvate, si è pronti a configurare i monitor che includono la registrazione del payload, l'accuratezza e la correttezza. 

2. Per iniziare, fare clic su **Configura monitor**.

## Fornire i dettagli della registrazione del payload
{: #mo-work-data}

È necessario fornire informazioni sui dati del modello e di training. Per ulteriori informazioni sui dati di training, consultare [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Preparazione alla spiegazione](images/config-what-monitor.png)

- Se si utilizza un'istanza {{site.data.keyword.pm_full}} che si trova nella stessa regione dell'istanza {{site.data.keyword.aios_short}}, anche se è necessario selezionare il tipo di dati e il tipo di algoritmo, alcune informazioni di registrazione del payload sono configurate automaticamente. 
- Altrimenti dalla scheda e dalle finestre **Registrazione payload**, è necessario immettere le informazioni sui tipi di dati e di algoritmi e la registrazione del payload. 

   Ci sono requisiti specifici a seconda delle selezioni. Per ulteriori informazioni, consultare [Dati numerici/categoriali](https://test.cloud.ibm.com/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan).

   Prima di poter configurare i monitor, è necessario copiare uno dei frammenti di codice da eseguire. Eseguire il comando cURL nell'applicazione client o il comando Python nel notebook di data science. Questo fornisce un modo per registrare le richieste di distribuzione modello e per scrivere i dati di risposta nel database di payload.
   
Dopo aver inviato i dettagli di registrazione del payload, utilizzando il metodo {{site.data.keyword.pm_full}} locale o utilizzando l'API, è necessario tornare alla schermata **Registrazione payload** e fare clic su **Ho terminato**.

![è raffigurata la schermata di registrazione payload](images/payload-logging-gosales001.png)

Se il calcolo del punteggio viene inviato correttamente a {{site.data.keyword.aios_short}}, viene visualizzato il seguente pannello dopo aver fatto clic sul pulsante **Ho terminato**. Il pulsante è nascosto e si vede il messaggio, **Registrazione attivata correttamente**.

![è raffigurata la schermata di registrazione payload dopo un caricamento riuscito dei dati](images/payload-logging-gosales002.png)


### Fornire i dettagli sul modello
{: #mo-work-model-dets}

Fornire le informazioni sul modello in modo che {{site.data.keyword.aios_short}} possa accedere al database e comprendere come è configurato il modello.

Nello specifico, per configurare i monitor, è necessario eseguire le seguenti attività:

1. Specificare l'ubicazione dei dati di training. Immettere il percorso, il nome host o l'indirizzo IP, il nome del database e le informazioni di autenticazione.
2. All'interno del database, è necessario selezionare la tabella di training selezionando lo schema e la tabella.
3. Selezionare la colonna etichetta dalla tabella di training.
4. Selezionare le funzioni che sono state utilizzate per addestrare la distribuzione AI.
5. Selezionare le funzioni testo e categoriali.
6. Selezionare la colonna di previsione di distribuzione.
7. Infine, è possibile esaminare i dettagli del modello prima di salvarlo.

Le seguenti sezioni forniscono alcune informazioni specifiche che si incontrano in base al tipo di modello, [Dati numerici/categoriali](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan) o [Immagini e testo non strutturato](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datai).


### Dati numerici/categoriali
{: #mo-nuca}

Per i dati numerici o categoriali, è necessario fornire informazioni sui dati di training per il modello, per poter configurare i monitor.

- **Configura manualmente i monitor** - Richiede di fornire informazioni di connessione ai dati di training.

    - Selezionare il [tipo di algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) e fare clic su **Avanti**:

      Il formato dei dati di training deve corrispondere al modello. Ad esempio, se il modello prevede `M` e `F` per la funzione `Gender`, i dati di training devono avere `M` e `F`, non `Male` e `Female`.  La release corrente di {{site.data.keyword.aios_short}} supporta solo le ubicazioni database Db2 o Cloud Object Storage.
        {: important}

    - Specificare l'ubicazione (`Db2` o `Cloud Object Storage`), quindi:

        - Per un database Db2, immettere le seguenti informazioni:

            - Nome host o indirizzo IP
            - Porta
            - Database (nome)
            - Nome utente
            - Password

        - Per Cloud Object Storage, immettere le seguenti informazioni:

            - URL di accesso: l'URL di accesso deve corrispondere all'impostazione della regione del bucket in cui si trovano i dati di training. Si specificherà il bucket di dati di training nel passo successivo.
            - Istanza risorsa (ID)
            - Chiave API

    - Per assicurarsi che la connessione sia valida, fare clic sul pulsante **Verifica** per connettersi ai dati di training.
    - Specificare l'esatta ubicazione nel database Db2 o Cloud Object Storage in cui si trovano i dati di training.

        - Per un database Db2, selezionare sia uno schema che una tabella di training che includa le colonne previste dal modello.
        - Per Cloud Object Storage, selezionare un bucket e un dataset.

- **Carica un file di configurazione** - Scegliere questa opzione se si preferisce mantenere privati i dati di training. È possibile utilizzare un notebook Python personalizzato per fornire a {{site.data.keyword.aios_short}} informazioni per analizzare i dati di training senza fornire accesso ai dati di training stessi.

  L'esecuzione del notebook Python consente di catturare i valori distinti nelle colonne dello schema, così come i nomi delle colonne. Inoltre, è possibile utilizzare il notebook per pre-configurare il monitor di correttezza.

   - Scaricare il [notebook personalizzato](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external} e sostituire le credenziali con le proprie.
   - Esaminare attentamente il notebook, specificando i dati per il proprio modello, dove opportuno. Salvare il notebook.
   - Eseguire il notebook per generare un file di configurazione in formato JSON.
   - Caricare il file di configurazione JSON.

     ![Caricare il JSON di configurazione](images/config-json-monitor.png)

- {{site.data.keyword.aios_short}} localizza i dati di training dai metadati memorizzati con il modello in {{site.data.keyword.pm_full}}. Scegliere la colonna etichetta nei dati di training che contengono i valori di previsione.
- Selezionare le colonne utilizzate per addestrare il modello - queste sono le funzioni che la distribuzione modello prevede in una richiesta.
- Infine, selezionare le colonne che contenevano testo e sono state convertite in numeri interi. Ad esempio, se i dati di training originali contenevano `Male` e `Female` per `Gender`, e ora sono stati mappati rispettivamente a `0` e `1`, i dati di training ora contengono i valori `0` e `1` per la colonna `Gender`. Identificare le colonne che ora contengono numeri interi, ma originariamente contenevano valori testo.

### Immagini e testo non strutturato
{: #mo-imun}

- **Immagini**

  Per i modelli che accettano immagini come input, l'immagine deve essere rappresentata in formato (altezza) x (larghezza) x (# canali), dove ogni punto rappresenta valori monocromo o RGB per ogni pixel.

- **Testo non strutturato**

   Per i modelli che accettano il testo come input, è previsto che il modello accetti tutto il testo e non una rappresentazione vettorizzata del testo.

## Esaminare e salvare la configurazione
{: #mo-save}

Esaminare il riepilogo delle selezioni e fare clic su **Salva** per continuare.

  ![Selezionare tabella dati](images/config-summary-monitor.png)

### Passi successivi
{: #mo-next}

Per continuare la configurazione dei monitor, fare clic sulla scheda **Accuratezza** e fare clic su **Inizia**.Per ulteriori informazioni, consultare [Configurazione dei monitor Accuratezza o Qualità](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
