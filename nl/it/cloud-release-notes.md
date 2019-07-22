---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: release notes, what's new 

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

# Novità
{: #rn-relnotes}

Questo documento descrive le nuove funzioni per {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 2 luglio 2019
{: #rn-2jul2019}

Sono disponibili le seguenti nuove funzioni e modifiche per {{site.data.keyword.aios_short}}.

- __*Rilevamento deviazione*__: ![tag beta](images/beta.png)

  {{site.data.keyword.aios_short}} ora supporta il rilevamento della deviazione.

   Per ulteriori informazioni, consultare [Rilevamento deviazione](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr).

- __*Supporto di Microsoft Azure ML Service*__: {{site.data.keyword.aios_short}} ora supporta Microsoft Azure ML Service, che fornisce un mezzo per integrare i propri modelli di AI del servizio Azure ML con la correttezza, l'accuratezza e l'esplicabilità di {{site.data.keyword.aios_short}}.

   Per ulteriori informazioni, consultare [Framework Microsoft Azure ML Service](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-frmwrks-azure-service).

- __*Flusso di lavoro migliorato*__: {{site.data.keyword.aios_short}} ha lavorato sul miglioramento del flusso di lavoro, così ora è possibile accelerare il lavoro grazie a un numero inferiori si selezioni e maggiore esplicabilità. Il pannello di navigazione permette di vedere dove ci si trova e rende facile andare avanti e indietro tra le attività di configurazione.

   Per ulteriori informazioni, consultare [Preparazione dei monitor per una distribuzione](/docs/services/ai-openscale?topic=ai-openscale-mo-config).

- __*Più provider di machine learning*__: perché essere vincolati a un solo provider o motore di machine learning? Con la versione più recente di {{site.data.keyword.aios_short}}, è possibile aggiungere più provider in modo da poter sfruttare le loro caratteristiche uniche o fornire continuità con le app legacy.

   Per ulteriori informazioni, consultare [Supporto per più motori di machine learning](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng).

- __*Metriche più pronte all'uso*__: con questa versione di {{site.data.keyword.aios_short}}, ci sono molte nuove metriche di correttezza, qualità, comportamento, prestazioni e analytics. Ci servirà più spazio!

   Per maggiori informazioni, consultare [Panoramica sulle metriche di qualità](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics) e fare clic sui vari elementi della pagina per conoscere le altre metriche: [Correttezza](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness), [Prestazioni](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through), [Analytics](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload) e [Comportamento](/docs/services/ai-openscale?topic=ai-openscale-behavior-ovr).

- __*Accelerazione sulla distorsione*__: con gli attributi di correttezza suggeriti e i valori automatici per la configurazione della distorsione, è facile vedere dove {{site.data.keyword.aios_short}} rileva i punti in cui si potrebbe verificare la violazione della soglia di correttezza nel modello distribuito. È possibile  accettare le funzioni consigliate per monitorare e modificare i valori.

   Per ulteriori informazioni, consultare [Panoramica sulle metriche di correttezza](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness).

## 11 giugno 2019
{: #rn-11June2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

- __*Funzionalità dashboard aggiornate*__: il dashboard {{site.data.keyword.aios_short}} ha subito diverse revisioni. Questa nuova versione contiene i seguenti miglioramenti:

    - Un nuovo pannello guida semplifica l'individuazione delle risorse, come StackOverflow, IBM Support e 
    - La globalizzazione è stata abilitata per il dashboard
    - Miglioramenti di utilizzabilità

## 7 giugno 2019
{: #rn-7June2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

- __*Interfaccia di riga comandi migliorata*__: l'interfaccia di riga comandi, ibm-ai-openscale-cli, è stata aggiornata e ora viene rilasciata la versione 0.2.148. Questa nuova versione contiene i seguenti miglioramenti:

    - Cronologia delle metriche di qualità aggiornata per includere la gamma completa di nuove metriche di qualità supportate da OpenScale
    - Supporto per la specifica di un certificato SSL direttamente quando si utilizza IBM DB2
    - Supporto per il nuovo SDK ibm-ai-openscale 2.1.8 Python
    - Correzione di altri bug e miglioramenti nella stabilità

   Installare da PyPI eseguendo il comando `pip install -U ibm-ai-openscale-cli` e richiamare la guida all'utilizzo eseguendo il comando `ibm-ai-openscale-cli --help`. Per ulteriori informazioni, consultare la [pagina del progetto PyPI](https://pypi.org/project/ibm-ai-openscale-cli).

## 29 maggio 2019
{: #rn-29May2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

- __*Miglioramenti nella visualizzazione della distorsione*__: ![tag beta tag](images/beta.png) la visualizzazione della distorsione include le seguenti viste: 

    - Payload + Perturbati: include la richiesta di calcolo del punteggio ricevuta per l'ora selezionata più record aggiuntivi da ore precedenti se non è stato soddisfatto il numero minimo di record richiesti per la valutazione. Include altri record perturbati/sintetizzati utilizzati per testare la risposta del modello quando il valore della funzione monitorata cambia.
    - Payload: le richieste di calcolo del punteggio effettive ricevute dal modello per l'ora selezionata.
    - Training: i record dei dati di training utilizzati per addestrare il modello.
    - Distorsione annullata: l'output dell'algoritmo di annullamento distorsione dopo l'elaborazione dei dati di runtime e perturbati.

   Per ulteriori informazioni, consultare [Visualizzazione distorsione](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz).

- __*Calcolo dell'accuratezza per output senza distorsione*__: il calcolo dell'accuratezza include l'output senza distorsione. È possibile confrontare l'accuratezza del modello senza distorsione con quella di un modello di produzione.

   Per ulteriori informazioni, consultare [Accuratezza](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view).

- __*Supporto per più motori di machine learning*__: {{site.data.keyword.aios_short}} supporta più motori di machine learning all'interno di una singola istanza a condizione che il provisioning venga eseguito tramite [l'SDK Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).

   Per ulteriori informazioni, consultare [Supporto per più motori di machine learning](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng).

- __*Supporto di internazionalizzazione*__: {{site.data.keyword.aios_short}} supporta le versioni localizzate e include dati di elaborazione nelle lingue supportate. L'interfaccia utente {{site.data.keyword.aios_short}}, la documentazione e i messaggi di errore sono attualmente tradotti nelle seguenti lingue: 
    - Tedesco
    - Francese
    - Italiano
    - Spagnolo
    - Portoghese brasiliano
    - Giapponese
    - Cinese semplificato
    - Cinese tradizionale
    - Coreano

   Per ulteriori informazioni (incluse le limitazioni), consultare [Lingue supportate per {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-sl-langs).

- __*Potenziamenti del framework {{site.data.keyword.pm_full}}*__: {{site.data.keyword.aios_short}} ora supporta i framework scikit-learn e XGBoost sul motore {{site.data.keyword.pm_full}}.

   Per ulteriori informazioni, consultare [Framework {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml).

## 25 aprile 2019
{: #rn-25April2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

Oltre ai miglioramenti di usabilità e agli aggiornamenti di sicurezza, i nostri sviluppatori si sono occupati di nuove funzionalità. Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate nelle ultime settimane includono:

- __*Tour di configurazione automatizzata*__: una nuova modalità assistita per configurazione l'ambiente {{site.data.keyword.aios_short}}. Utilizzare la [Configurazione automatizzata](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start) per eseguire il provisioning dei servizi e scaricare e configurare un modello. Si visualizzerà questa opzione quando si dispone di una nuova istanza di {{site.data.keyword.aios_short}}.
- __*Passaggio alla versione beta*__: ![tag beta](images/beta.png) La nuova funzione **Esplora la nuova versione beta**, permette di operare nell'ambiente beta, dove è possibile verificare tutte le ultime caratteristiche e le nuove funzionalità. Non ti piace quello che vedi? Puoi tornare indietro facendo clic su **Torna alla versione originale**. La configurazione e i monitor non saranno influenzati. Le seguenti funzionalità fanno parte del programma beta corrente:
    - __*Matrice di confusione*__: una [matrice di confusione visualizza](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx) i falsi positivi e i falsi negativi. Fare clic su una cella per visualizzare il sottoinsieme dei record di feedback.

## 10 aprile 2019
{: #rn-10April2019}

- __*Lo strumento Express Path ora supporta i modelli cliente*__: automatizza il processo di onboarding su {{site.data.keyword.aios_short}}.

   Per ulteriori informazioni, consultare [ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/).


## 5 marzo 2019
{: #rn-5March2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  precedente release includono:

- __*Nuovo modello di rischio di credito*__: è supportato un esempio/supporto didattico per un nuovo modello di rischio di credito per tutti i motori di calcolo del punteggio. Per ulteriori informazioni, consultare gli argomenti [Introduzione](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) e [Risorse aggiuntive](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Elaborazione dell'annullamento della distorsione*__: è possibile alternare tra il modello di produzione e un modello con distorsione annullata creato da {{site.data.keyword.aios_short}}. Consultare [Modello di produzione e modello con distorsione annullata](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) e [Come funziona l'annullamento della distorsione](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) per ulteriori informazioni.

## 22 febbraio 2019
{: #rn-22February2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  precedente release includono:

- __*Aggiornamenti IU*__: è possibile importare un file JSON per configurare programmaticamente tutti i monitor e le funzioni durante la creazione della sottoscrizione. È anche possibile esportare il file di configurazione. Consultare l'argomento [Configurazione della sottoscrizione di distribuzione utilizzando i file JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) per ulteriori informazioni.

## 7 febbraio 2019
{: #rn-7February2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  precedente release includono:

- __*Aggiornamenti IU*__: sono stati apportati diversi miglioramenti all'interfaccia utente di {{site.data.keyword.aios_short}}, tra cui un modo per [verificare la correttezza e l'accuratezza su richiesta](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep) e la possibilità di visualizzare un elenco di transazioni dal [grafico dei dettagli della correttezza](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Miglioramenti dell'esplicabilità*__: tutti i numeri ora hanno la stessa precisione/scala tra i valori Pertinenti Positivi (PP) e Pertinenti Negativi (PN).

- __*Supporto SSL Db2*__: {{site.data.keyword.aios_short}} supporta i certificati autofirmati (codificati in Base-64) con le credenziali DB2.

- __*Supporto {{site.data.keyword.Bluemix}} Database*__: {{site.data.keyword.aios_short}} ora supporta i database per PostgreSQL, oltre a Compose per PostgreSQL e Db2)

## 14 dicembre 2018
{: #rn-14December2018}

Sono disponibili le seguenti nuove funzioni, modifiche e problemi noti per il servizio.

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  release beta includono:

- __*Disponibilità generale*__: la release GA (General Availability) di {{site.data.keyword.aios_full_notm}} come piano {{site.data.keyword.Bluemix}} Standard (a pagamento).

- __*{{site.data.keyword.icp4dfull_notm}} V1.2*__: se si utilizza {{site.data.keyword.wos4d_full}} V1.2, consultare la documentazione, incluse le istruzioni di installazione, qui: [Checklist di installazione](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Supporto per il proprio tipo di modello*__: oltre alle distribuzioni di modelli AI in {{site.data.keyword.pm_full}}, {{site.data.keyword.aios_short}} supporta le distribuzioni di modelli in Microsoft Azure, Amazon SageMaker e ambienti personalizzati. Consultare [Tipi di modello supportati](/docs/services/ai-openscale?topic=ai-openscale-in-ov) per ulteriori informazioni.

- __*Database "lite" gratuito*__: un database gestito "lite" gratuito fornisce tutto quello che occorre per iniziare ad utilizzare {{site.data.keyword.aios_short}}. Consultare i [piani di determinazione dei prezzi {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external} per i dettagli.

- __*Monitoraggio della distorsione*__: supporto per gli attributi protetti di tipo `mobile` e `doppio`, e di rilevamento della distorsione sui modelli di regressione lineare. E {{site.data.keyword.aios_short}} può automaticamente annullare la distorsione del modello AI. Consultare [Informazioni sulla correttezza](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) per ulteriori informazioni.

- __*Esplicabilità*__: supporto per i modelli di regressione, le funzioni Python e spiegazioni contrastanti complementari. Consultare [Monitoraggio dell'esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) per ulteriori informazioni.

- __*Datastore*__: monitoraggio della qualità senza dipendere da {{site.data.keyword.pm_full}}, e la possibilità di utilizzare il proprio database, sia che sia Db2, Postgres o Db2 on Cloud.

- __*IU potenziata*__: l'interfaccia utente di {{site.data.keyword.aios_short}} è stata migliorata per includere una distribuzione istogramma di runtime con alternanza per dati di training, ID & versione modello e una tabella di ID transazione dall'istogramma. Consultare [Visualizzazione dei dati per un'ora specifica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) per ulteriori informazioni.

- __*Opzione alternativa di configurazione del supporto didattico*__: per automatizzare il provisioning e la configurazione dei servizi {{site.data.keyword.Bluemix}} richiesti e per vedere un'applicazione IBM {{site.data.keyword.aios_full}}, incluso dati di campionamento, è possibile installare ed eseguire un modulo Python. Consultare [Installazione di un modulo Python per configurare {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

## 17 settembre 2018
{: #rn-17September2018}

- **Anteprima release Beta** - Benvenuti nell'anteprima della release beta di {{site.data.keyword.aios_full_notm}}.

<p>&nbsp;</p>

## Passi successivi
{: #relnotes-in-next}

Altre domande?

- [Limitazioni](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [Problemi noti](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)