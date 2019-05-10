---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: deployment, monitors, data

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

# Preparazione dei monitor per una distribuzione
{: #mo-config}

Configurare e abilitare i monitor per ogni distribuzioni di cui si sta tenendo traccia con {{site.data.keyword.aios_short}}.
{: shortdesc}

## Selezione di una distribuzione
{: #mo-select-deploy}

1.  Prima di tutto, è necessario selezionare una distribuzione.

    Se ci sono più distribuzioni per un dato modello, quando si configura una distribuzione, vengono configurate anche tutte le altre distribuzioni per lo stesso modello.
    {: note}

    ![Pagina Seleziona distribuzione](images/config-select-deploy.png)

1.  Selezionare il riquadro *Preparazione per il monitoraggio*.

    ![Preparazione per il monitoraggio](images/config-prep-monitor.png)

## Gestione dei dati
{: #mo-work-data}

1.  Ora devono essere fornite le informazioni sul modello e i dati di training; fare clic su **Avanti**.

    ![Preparazione alla spiegazione](images/config-what-monitor.png)

1.  Dal menu a discesa, selezionare il tipo di dati che la distribuzione analizza, e fare clic su **Avanti**.

    ![Selezionare tipo di input](images/config-input-monitor.png)

### Dati numerici/categoriali
{: #mo-nuca}

Per i dati numerici o categoriali, è necessario fornire informazioni sui dati di training per il modello, per poter configurare i monitor.

  ![Selezionare tipo di configurazione](images/config-manual-monitor.png)

- **Configura manualmente i monitor** - Richiede di fornire informazioni di connessione ai dati di training.

    - Selezionare il [tipo di algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) e fare clic su **Avanti**:

      ![Multiclasse](images/multiclass.png)

      Accertarsi che il formato dei dati di training sia esattamente uguale a quello previsto dal modello. Ad esempio, se il modello prevede `M` e `F` per la funzione *Gender*, i dati di training devono avere `M` e `F`, non `Male` e `Female`. Attualmente {{site.data.keyword.aios_short}} supporta solo le ubicazioni database Db2 o Cloud Object Storage.
        {: important}

    - Specificare l'ubicazione (`Db2` o `Cloud Object Storage`), quindi:

        - Per un database Db2, indicare le seguenti informazioni:

            - Nome host o indirizzo IP
            - Porta
            - Database (nome)
            - Nome utente
            - Password

            ![Specificare l'ubicazione Db2 della pagina dati di training](images/config-train-db2-monitor.png)

        - Per Cloud Object Storage, indicare le seguenti informazioni:

            - URL di accesso

              L'URL di accesso deve corrispondere all'impostazione della regione del bucket in cui si trovano i dati di training. Si specificherà il bucket di dati di training nel passo successivo.
              {: important}

            - Istanza risorsa (ID)
            - Chiave API

            ![Pagina Specifica ubicazione Cloud Object Storage dei dati di training](images/config-train-cos-monitor.png)

    - Assicurarsi che la connessione sia valida facendo clic sul pulsante **Verifica** per connettersi ai dati di training. Fare clic su **Avanti**.

    - Specificare l'esatta ubicazione nel database Db2 o Cloud Object Storage in cui si trovano i dati di training. 

        - Per un database Db2, selezionare sia uno schema che una tabella di training che includa le colonne previste dal modello:

          ![Specificare ubicazione Db2 di schema e tabella di training](images/fair-config-table-db2.png)

        - Per Cloud Object Storage, selezionare un bucket e un dataset:

          ![Specifica ubicazione Cloud Object Storage del dataset](images/fair-config-dset-cos.png)

          Fare clic su **Avanti** per procedere al Passo 5 di seguito.

- **Carica un file di configurazione** - Scegliere questa opzione se si preferisce mantenere privati i dati di training. È possibile utilizzare un notebook Python personalizzato per fornire a {{site.data.keyword.aios_short}} informazioni per analizzare i dati di training senza fornire accesso ai dati di training stessi.

  L'esecuzione del notebook Python consente di catturare i valori distinti nelle colonne dello schema, così come i nomi delle colonne. Inoltre, è possibile utilizzare il notebook per pre-configurare il monitor di correttezza.

    - Scaricare il [notebook personalizzato![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: new_window}, e sostituire le credenziali con le proprie. 

    - Esaminare attentamente il notebook, specificando i dati per il proprio modello, dove opportuno. Salvare il notebook.

    - Eseguire il notebook per generare un file di configurazione in formato JSON. 

    - Caricare il file di configurazione JSON.

        ![Caricare il JSON di configurazione](images/config-json-monitor.png)

    - Fare clic su **Avanti**.

- {{site.data.keyword.aios_short}} localizzerà i dati di training dai metadati memorizzati con il modello in WML. Scegliere la colonna etichetta nei dati di training che contengono i valori di previsione e fare clic su **Avanti**.

  ![Selezionare etichetta colonna](images/fair-config-column.png)

- Selezionare le colonne utilizzate per addestrare il modello - queste sono le funzioni che la distribuzione modello prevede in una richiesta. Fare clic su **Avanti**.

    ![Selezionare etichetta colonna](images/explain-select-column.png)

- Infine, selezionare le colonne che contenevano testo e sono state convertite in numeri interi. Ad esempio, se i dati di training originali contenevano `Male` e `Female` per *Gender*, e ora sono stati mappati rispettivamente a `0` e `1`, i dati di training ora contengono i valori `0` e `1` per la colonna *Gender*. Identificare le colonne che ora contengono numeri interi, ma originariamente contenevano valori testo. Fare clic su **Avanti**.

    ![Selezionare tabella dati](images/explain-text-column.png)

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

Per iniziare la configurazione dei monitor, selezionare una categoria e fare clic su **Inizia**.
