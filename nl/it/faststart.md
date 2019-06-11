---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, getting started, tutorial, understanding, fast start

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
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

# Configurazione automatizzata
{: #wos-fast-start}

Per vedere rapidamente come {{site.data.keyword.aios_short}} monitora un modello, eseguire l'opzione di scenario demo fornita quando si accede per la prima volta all'interfaccia utente {{site.data.keyword.aios_short}}.  Consultare [Utilizzo della demo IU](#wos-work-demo).
{: shortdesc}

## Prima di iniziare
{: #wos-prereqs}

Prima di iniziare il tour, è necessario disporre delle seguenti risorse configurate:

- {{site.data.keyword.ibmid}}
- {{site.data.keyword.aios_full}}

## Utilizzo della demo IU
{: #wos-work-demo}

1.  Accedere all'istanza {{site.data.keyword.aios_short}} su {{site.data.keyword.bluemix_full}}.
1.  Per utilizzare lo scenario demo, fare clic su **Esegui demo**.

   ![Demo - Benvenuti](images/fastpath_demo_11.31.04.png)

   Mentre viene eseguito il provisioning dei servizi {{site.data.keyword.aios_short}}, è possibile riesaminare lo scenario demo:

   ![Demo - Anteprima](images/fastpath_demo_11.31.58.png)

Quando il provisioning è completo, fare clic sul pulsante **Andiamo** per eseguire il tour del dashboard  {{site.data.keyword.aios_short}}, quindi procedere con [Visualizzazione dei risultati in {{site.data.keyword.aios_short}}](#wos-open).

   ![Demo - Andiamo](images/fastpath_demo_11.33.45.png)


## Visualizzazione dei risultati in
{{site.data.keyword.aios_short}}
{: #wos-open}

Per visualizzare le informazioni sulla correttezza e l'accuratezza del modello, i dettagli dei dati monitorati e l'analisi di una singola transazione, aprire il dashboard {{site.data.keyword.aios_short}}. Ogni distribuzione viene mostrata come un riquadro. Il tour ha configurato una distribuzione denominata `GermanCreditRiskModel`, come mostrato nella seguente figura:


   ![Demo - Andiamo](images/fastpath_demo_11.33.54.png)


### Visualizzazione delle informazioni
{: #wos-insights}

La pagina Insight mostra in un'unica vista tutti i problemi di correttezza e accuratezza, come determinato dalle soglie configurate.

   ![Demo - Andiamo](images/fastpath_demo_11.34.00.png)

### Visualizzazione dei dati di monitoraggio
{: #wos-monitoring}

1.  Dalla pagina Insight, fare clic sul riquadro `GermanCreditRiskModelICP` per visualizzare i dettagli relativi ai dati monitorati.
1.  Fare clic e trascinare il puntatore nel grafico per visualizzare un periodo di giorni e ore che mostrano dati e fare clic sul link **Visualizza dettagli**. In alternativa, è possibile  fare clic su un periodo di tempo differente nel grafico per modificare i dati visualizzati.

     - Ad esempio, la figura che segue mostra i dati per una data e ora specifica. Le date e le ore variano, a seconda di quando si esegue il modulo.

     - Per informazioni sull'interpretazione del grafico delle serie temporali, consultare [Monitoraggio della correttezza, Richieste medie al minuto e Accuratezza](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).

   ![Demo - Andiamo](images/fastpath_demo_11.34.17.png)

1.  Per visualizzare i dettagli relativi al monitoraggio dei dati `Sesso`, assicurarsi che `Sesso` sia selezionato dal menu a discesa.

    - Notare che nella seguente immagine, la distorsione esiste.
    
   ![Demo - Andiamo](images/fastpath_demo_11.34.27.png)

    - Per informazioni sull'interpretazione del grafico dei punti di dati a un'ora specifica, consultare [Visualizzazione dei dati](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual).


### Visualizzazione spiegazione
{: #wos-explain}

Per comprendere i fattori che contribuiscono quando una distorsione è presente per un dato periodo di tempo, dal pannello di visualizzazione nella sezione precedente, fare clic sul pulsante di opzione **Transazioni con distorsione**.

   ![Demo - Andiamo](images/fastpath_demo_11.35.06.png)

Vengono elencati gli ID transazione per l'ultima ora per le transazioni che hanno distorsione. Per il modello utilizzato in questo modulo, esistono distorsioni per le richieste disponibili.

   ![Demo - Andiamo](images/fastpath_demo_11.35.12.png)

Per informazioni relative alla ricerca e alla spiegazione delle transazioni, consultare [Monitoraggio esplicabilità](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov).

   ![Demo - Andiamo](images/fastpath_demo_11.35.50.png)

## Completamento del tour
{: #wos-done-demo}

1. Fare clic sul pulsante **Eseguito**.

   ![Demo - Andiamo](images/fastpath_demo_11.37.22.png)

2. Fare clic sul pulsante **Andiamo** per iniziare a lavorare con {{site.data.keyword.aios_short}}.

   ![Demo - Andiamo](images/fastpath_demo_11.33.45.png)


## Informazioni correlate
{: #wos-info}

- Per informazioni sulle distorsioni, consultare [Correttezza](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor).
- Per informazioni sulla bontà dei risultati previsionali del modello, consultare [Accuratezza](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- Per informazioni sull'interpretazione di grafici, dati e transazioni, consultare [Monitoraggio della correttezza, Richieste medie al minuto e Accuratezza](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).
