---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Configurazione del monitor Correttezza
{: #mf-monitor}

In {{site.data.keyword.aios_full}}, il monitor della correttezza esegue la scansione della distribuzione alla ricerca della distorsione, per garantire risultati corretti tra popolazioni differenti.
{: shortdesc}

## Informazioni sulla correttezza
{: #mf-understand}

{{site.data.keyword.aios_short}} controlla il modello distribuito alla ricerca di distorsioni in fase di runtime. Per rilevare la distorsione per un modello distribuito, è necessario definire gli attributi di correttezza, come età o genere, come dettagliato nella seguente sezione [Configurazione del monitor Correttezza](#mf-config).

È obbligatorio specificare lo schema di output per un modello o funzione in Watson {{site.data.keyword.pm_short}}, affinché il controllo della distorsione sia abilitato in {{site.data.keyword.aios_short}}. Lo schema di output può essere specificato utilizzando la proprietà `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` nella parte dei metadati dell'API `store_model`. Per ulteriori informazioni, consultare la [Documentazione per il client {{site.data.keyword.pm_full}}](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}.

### Funzionamento
{: #mf-works}

Prima di configurare il monitor Correttezza, è importante conoscere alcuni concetti chiave:

- Gli attributi di correttezza sono gli attributi del modello per i quali è probabile che il modello esibisce distorsione. Come esempio, per l'attributo di correttezza **`Gender`**, il modello potrebbe essere distorto rispetto ai valori di genere specifici (`Female`, `Transgender`, ecc.) Un altro esempio di attributo di correttezza è **`Age`**, dove il modello potrebbe esibire distorsione rispetto alle persone in un gruppo di età, come `18-25`.

- Valori di riferimento e monitorati: i valori degli attributi di correttezza sono divisi in due categorie distinte: riferimento e monitorato. I valori monitorati sono quelli rispetto ai quali probabilmente avverrà la discriminazione. Nel caso di un attributo di correttezza come **`Gender`**, i valori monitorati potrebbero essere `Female` e `Transgender`. Per un attributo di correttezza numerico, come ad esempio **`Age`**, i valori monitorati potrebbero essere `[18-25]`. Tutti gli altri valori per un determinato attributo di correttezza quindi considerati come valori di riferimento, ad esempio `Gender=Male` o `Age=[26,100]`.

- Risultati favorevoli e non favorevoli: l'output del modello è categorizzato come Favorevole o Non favorevole. Come esempio, se un modello deve prevedere se una persona può ottenere un prestito o meno, il risultato favorevole può essere `Loan Granted` o `Loan Partially Granted`, mentre il risultato non favorevole può essere `Loan Denied`. Così, il risultato favorevole viene considerato un risultato positivo, mentre il risultato sfavorevole è considerato negativo.

L'algoritmo {{site.data.keyword.aios_short}} calcola la distorsione su base oraria, utilizzando gli ultimi `N` record presenti nella tabella di registrazione del payload; il valore di `N` viene specificato durante la configurazione della correttezza. L'algoritmo perturba questi ultimi `N` record per generare dati aggiuntivi.

La perturbazione viene effettuata modificando il valore dell'attributo di correttezza da Riferimento a Monitorato, o viceversa. I dati perturbati vengono poi inviati al modello per valutarne il comportamento. L'algoritmo considera gli ultimi `N` record nella tabella del payload, e il comportamento del modello sui dati perturbati, per decidere se il modello agisce in modo distorto.

Un modello è considerato distorto se, in questo dataset combinato, la percentuale di risultati favorevoli per la classe monitorata è inferiore alla percentuale di risultati favorevoli per la classe di riferimento, per qualche valore di soglia. Questo valore di soglia deve essere specificato quando si configura la correttezza.

I valori di correttezza possono essere più del 100%. Ciò significa che il gruppo monitorato ha ricevuto più risultati favorevoli rispetto al gruppo di riferimento. Inoltre, se non vengono inviate nuove richieste di punteggio, il valore di correttezza rimarrà costante.
{: note}

### Calcolo matematico
{: #mf-bias-math}

La metrica di correttezza utilizzata in {{site.data.keyword.aios_short}} ha impatto eterogeneo, cioé una misurazione di come la frequenza con cui un gruppo non privilegiato riceve un certo risultato o il risultato viene confrontato con la frequenza con cui un gruppo privilegiato riceve quello stesso risultato.

La seguente formula matematica viene utilizzata per il calcolo dell'impatto eterogeneo:

```
                     (num_positives(privileged=False) / num_instances(privileged=False))
Impatto eterogeneo =   ______________________________________________________________________

                     (num_positives(privileged=True) / num_instances(privileged=True))
```

dove `num_positives` è il numero di individui nel gruppo (privileged=False, cioé non privilegiati o privileged=True, cioé privilegiati) che hanno ricevuto un risultato positivo e num_instances è il numero totale di individui nel gruppo.

Il numero risultante sarà una percentuale, cioé la percentuale della frequenza con cui il gruppo non privilegiato riceve il risultato positivo rispetto alla frequenza con cui il gruppo privilegiato riceve il risultato positivo. Ad esempio, se un modello di rischio di credito assegna la previsione “nessun rischio” all'80% di richiedenti non privilegiati e al 100% di richiedenti privilegiati, il modello avrà un impatto eterogeneo (presentato come punteggio di correttezza in {{site.data.keyword.aios_short}}) dell'80%.

In {{site.data.keyword.aios_short}}, i risultati positivi sono designati come risultati favorevoli e i risultati negativi come risultati non favorevoli. Il gruppo privilegiato è designato come gruppo di riferimento e il gruppo non privilegiato come gruppo monitorato.


### Visualizzazione distorsione ![tag beta](images/beta.png)
{: #mf-monitor-bias-viz}

Quando viene rilevata una potenziale distorsione, {{site.data.keyword.aios_short}} esegue diverse funzioni per confermare se la distorsione è reale. {{site.data.keyword.aios_short}} perturba i dati invertendo il valore monitorato con quello di riferimento ed eseguendo questo nuovo record nel modello. Successivamente, visualizza l'output risultante come output senza distorsione. {{site.data.keyword.aios_short}} inoltre addestra un modello shadow senza distorsione che viene poi utilizzato per rilevare quando un modello sta per effettuare una previsione distorta. 

Vengono utilizzati due diversi dataset per il calcolo della correttezza e dell'accuratezza. La correttezza è calcolata utilizzando i dati del payload + i dati perturbati. L'accuratezza è calcolata utilizzando i dati di feedback. Per calcolare l'accuratezza, {{site.data.keyword.aios_short}} necessita di dati etichettati manualmente, che sono presenti solo nella tabella di feedback.

I risultati di tali determinazioni sono disponibili nella visualizzazione della distorsione, che include le seguenti viste: 

- **Payload + Perturbati**: include la richiesta di calcolo del punteggio ricevuta per l'ora selezionata più record aggiuntivi da ore precedenti se non è stato soddisfatto il numero minimo di record richiesti per la valutazione. Include altri record perturbati/sintetizzati utilizzati per testare la risposta del modello quando il valore della funzione monitorata cambia.

   Prendere nota dei seguenti dettagli su payload e perturbati:

   - Numero di record letti in questa ora dalla tabella di payload
   - Record aggiuntivi letti nelle ore precedenti (ad esempio, se il valore `min_records` nella configurazione di correttezza è impostato su 1000, e tra le 2pm e le 3pm  vengono aggiunti solo 10 record, per soddisfare il requisito minimo, il sistema leggerà ulteriori 990 record dalle ore precedenti.)
   - Record perturbati per attributo di correttezza
   - Data/ora record più vecchio nel frame di dati per cui deve essere calcolata la distorsione
   - Data/ora record più recente nel frame di dati per cui deve essere calcolata la distorsione

  ![esempio di payload più perturbati](images/payload&perturbed.png)



- **Payload**: le richieste di calcolo del punteggio effettive ricevute dal modello per l'ora selezionata.

   Prendere nota dei seguenti dettagli sul payload:
   
   - Numero di record letti sui quali viene eseguita l'operazione di annullamento distorsione dalla tabella di payload
   - Data/ora record più vecchio nel frame di dati per cui deve essere calcolata la distorsione
   - Data/ora record più recente nel frame di dati per cui deve essere calcolata la distorsione


  ![esempio di dati  payload](images/payload.png)

- **Training**: i record dei dati di training utilizzati per addestrare il modello.

   Prendere nota dei seguenti dettagli sul training:
   
   - Numero di record di dati di training. I dati di training sono letti una sola volta e la distribuzione è memorizzata nella variabile `sottoscrizione/configurazione_correttezza`. Durante l'elaborazione della distribuzione è anche possibile trovare il numero di record di dati di training e conservarlo nella stessa distribuzione. Inoltre, quando i dati di training vengono modificati, cioè se il comando `POST /distribuzione_dati` viene rieseguito, questo valore viene aggiornato nella variabile `configurazione_correttezza/distribuzione_dati_training`. Quando si invia la metrica, è opportuno inviare anche questo valore.
   - L'ora in cui i dati di training sono stati elaborati l'ultima volta (prima volta e successivi aggiornamenti)

  ![esempio di dati di training](images/training.png)
   

   
- **Distorsione annullata**: l'output dell'algoritmo di annullamento distorsione dopo l'elaborazione dei dati di runtime e perturbati.

   Prendere nota dei seguenti dettagli sulla distorsione annullata:
   
   - Numero di record letti sui quali viene eseguita l'operazione di annullamento distorsione dalla tabella di payload
   - Record aggiuntivi letti per eseguire la distorsione, e quindi annullarla. Stesso numero nella selezione `Payload + Perturbati`
   - Record perturbati per attributo di correttezza
   - Data/ora record più vecchio nel frame di dati per cui deve essere calcolata la distorsione
   - Data/ora record più recente nel frame di dati per cui deve essere calcolata la distorsione
   - I valori di correttezza prima e dopo sono visualizzati nella porzione di intestazione della vista Distorsione annullata. 
      - Il valore di accuratezza **dopo** è calcolato prendendo i dati di feedback e inviandoli all'API di annullamento distorsione attiva. Questa API restituisce la previsione senza distorsione. I dati di feedback contengono anche l'etichetta manuale. L'etichetta manuale è confrontata con la previsione senza distorsione per calcolare l'accuratezza. Questa API restituisce la previsione senza distorsione. La tabella di feedback contiene anche l'etichetta manuale. L'etichetta manuale è confrontata con la previsione senza distorsione per calcolare l'accuratezza. 
      - Il valore di accuratezza **prima** è calcolata utilizzando gli stessi dati di feedback. Per il calcolo dell'accuratezza prima, i dati di feedback sono inviati al modello per ottenerne la previsione e il valore previsto è confrontato con l'etichetta manuale per ottenere l'accuratezza.

  ![esempio di dati senza distorsione](images/debiased.png)
  
### Esempio:
{: #mf-ex1}

Considerare un punto di dati in cui, per `Gender=Male` (valore di riferimento), il modello prevede un risultato favorevole, ma quando il record è perturbato dalla modifica di `Gender` in `Female` (valore monitorato), pur mantenendo tutti gli altri valori funzione, il modello prevede un risultato non favorevole. Un modello complessivo è considerato distorto se ci sono sufficienti punti di dati (negli ultimi `N` record nella tabella del payload, più i dati perturbati) in cui il modello agiva in modo distorto.

### Modelli supportati
{: #mf-supmo}

 {{site.data.keyword.aios_short}} supporta il rilevamento della distorsione solo per i modelli e le funzioni Python che prevedono tipi di dati strutturati nel vettore funzione.

## Configurazione del monitor Correttezza
{: #mf-config}

Dalla scheda **Correttezza**, sulla pagina **Cos'è il monitor Correttezza?** fare clic su **Inizia** per avviare il processo di configurazione. 

![Pagina Cos'è il monitor Correttezza?](images/fair-what-is.png)

Attraverso questo processo, {{site.data.keyword.aios_full}} analizza il modello ed effettua raccomandazioni in base al risultato più logico. Sulle pagine successive della scheda **Correttezza**, è necessario eseguire le seguenti attività:

1. Selezionare le funzioni da monitorare. Sono supportate solo le funzioni di tipo di dati di correttezza categoriali, numerici (interi), mobili o doppi. Le funzioni con altri tipi di dati non sono supportate.

1. Specificare i gruppi di riferimento e monitorati.

   Ciascuna funzione dispone di requisiti specifici da configurare. Ad esempio, se si sceglie `age` come una delle funzioni monitorate, è necessario definire gli intervalli di età per un **Gruppo di riferimento** e un **Gruppo monitorato** immettendo i valori direttamente in ogni gruppo.

1.  Impostare la soglia di avviso per la correttezza della funzione.

    Una soglia di correttezza viene utilizzata per specificare una differenza accettabile tra la percentuale di risultati favorevoli per il gruppo monitorato rispetto alla percentuale di risultati favorevoli per il gruppo di riferimento.

    Considerare un modello che prevede chi dovrebbe ottenere un prestito (`favorable outcome=loan granted`) e chi non dovrebbe (`unfavorable outcome=loan denied`). Inoltre, il valore monitorato per l'età è `[18,25]` e il valore di riferimento è `[26,100]`. Quando l'algoritmo di rilevamento della distorsione viene eseguito, se trova che la percentuale di risultati favorevoli per le persone nel gruppo di età `[18,25]` negli ultimi `N` record più i dati perturbati è `50%`, mentre la percentuale di risultati favorevoli per le persone nel gruppo di età `[26,100]` è `70%`, allora la correttezza viene calcolata come 50*100/70 = 71.42.

    Se la soglia di correttezza è impostata sull'80%, l'algoritmo segnalerà il modello come distorto, perché la correttezza calcolata supera la soglia. Tuttavia, se la soglia è impostata sul 70% , il modello non verrà indicato come distorto.

     I valori immessi in questi pannelli devono essere quelli inviati all'endpoint di calcolo del punteggio del modello (e, di conseguenza, verranno aggiunti alla tabella payload). Se i dati vengono manipolati prima di inviarli all'endpoint di calcolo del punteggio, immettere i valori modificati. Ad esempio, se i dati originali avevano valori `Male` e `Female` per *Gender* e sono stati manipolati in modo che i dati inviati all'endpoint di calcolo del punteggio erano `M` e `F`, immettere `M` e `F` sin questa schermata.

1.  Specificare i valori che rappresentano un risultato favorevole per il modello. I valori sono derivati dalla colonna `label` nei [dati di training](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata), se lo schema di output del modello contiene una colonna di associazione. In {{site.data.keyword.pm_full}}, la colonna `prediction` ha sempre un valore doppio. La colonna di associazione viene utilizzata per specificare la mappatura di questo valore `prediction` con l'etichetta classe.

    Ad esempio, se il valore di `prediction` è `1.0`, la colonna di associazione potrebbe avere un valore di `Loan denied`; questo implica che la previsione del modello è `Loan denied`. Quindi, se lo schema di output del modello contiene una colonna di associazione, specificare valori favorevoli e non favorevoli utilizzando quelli presenti nella colonna di associazione.

    Se, tuttavia, la colonna di associazione non è presente nello schema di output del modello, i valori favorevoli e non favorevoli devono essere specificati utilizzando il valore della colonna `prediction` (`0.0`, `1.0`, ecc.)

1.  Infine, impostare una dimensione minima del campione, per prevenire la misurazione della correttezza fino a quando non sia disponibile un numero minimo di record nel dataset di valutazione. Ciò garantisce che la dimensione del campione non sia troppo piccola per l'asimmetria dei risultati. A ogni esecuzione del controllo della distorsione, verrà utilizzata la dimensione minima del campione per decidere il numero di record in base al quale eseguire il calcolo della distorsione.

    Viene visualizzato un riepilogo delle selezioni per la revisione. Se si desidera modificare qualsiasi cosa, fare clic sul link **Modifica** per quella sezione, altrimenti, fare clic su **Salva**. 

    È anche possibile fare clic su **Aggiungi un'altra funzione** per ritornare al pannello di selezione delle funzioni e aggiungere ulteriori funzioni, come `City`, `Zip code` o `Account Balance` al monitor Correttezza.

### Come funziona l'annullamento della distorsione
{: #mf-debias}

Per controllare l'endpoint di annullamento distorsione, fare clic sul pulsante **Endpoint di annullamento distorsione**. È possibile quindi visualizzare e copiare l'enpoint in diversi formati, come cURL, Java o Python. 

L'endpoint di calcolo del punteggio senza distorsione può essere utilizzato esattamente come un normale endpoint di calcolo del punteggio del modello distribuito. Oltre a restituire la risposta del modello distribuito, restituisce anche le colonne `debiased_prediction` e `debiased_probability`.

- La colonna `debiased_prediction` contiene il valore di previsione senza distorsione. Nel caso di {{site.data.keyword.pm_full}}, si tratta di una rappresentazione codificata della previsione. Ad esempio, se la previsione del modello è "Loan Granted" o "Loan Denied", {{site.data.keyword.pm_full}} può codificare questi due valori rispettivamente in "0.0" e "1.0". La colonna `debiased_prediction` contiene una rappresentazione codificata della previsione senza distorsione.

- La colonna `debiased_probability`, invece, rappresenta la probabilità della previsione senza distorsione. Si tratta di un array di valori doppi, dove ogni valore rappresenta la probabilità della previsione senza distorsione appartenente a una delle classi di previsione.

Viene restituita anche un'altra colonna, `debiased_decoded_target`, nel caso in cui si ha una colonna nello schema di output che contiene una colonna con `modeling-role` come `decoded-target`.

- La colonna `debiased_decoded_target` contiene la rappresentazione stringa della previsione senza distorsione. Nell'esempio precedente, dove il valore di previsione era "0.0" o "1.0", `debiased_decoded_target` conterrà "Loan Granted" o "Loan Denied".

Idealmente, si può richiamare direttamente questo endpoint dall'applicazione di produzione, invece di chiamare direttamente l'endpoint di calcolo del punteggio del modello distribuito nel motore di servizi modello ({{site.data.keyword.pm_full}}, Amazon Sagemaker, Microsoft Azure ML Studio, ecc.). In questo modo, {{site.data.keyword.aios_short}} memorizzerà anche i valori `debiased` nella tabella di registrazione del payload della distribuzione modello. Poi, verrà automaticamente eseguito l'annullamento della distorsione di tutti i calcoli di punteggio fatti attraverso questo endpoint.

Poiché questo endpoint si occupa della distorsione al runtime, continuerà a eseguire controlli in background degli ultimi dati di punteggio dalla tabella di registrazione del payload, e continuerà ad aggiornare il modello di mitigazione della distorsione utilizzato per annullare la distorsione delle richieste di calcolo del punteggio inviate. In questo modo, {{site.data.keyword.aios_short}} è sempre aggiornato con i dati in entrata più recenti e con il suo comportamento per rilevare e mitigare la distorsione.

Infine, {{site.data.keyword.aios_short}} utilizza una soglia per decidere che i dati ora sono accettabili e considerati senza distorsione. Quella soglia viene presa come valore minimo dalle soglie impostate nel monitor di correttezza per tutti gli attributi di correttezza configurati.

## Passi successivi
{: #mf-next}

Dalla pagina **Configura monitor**, è possibile selezionare un'altra categoria di monitoraggio.
