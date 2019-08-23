---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

## Passi
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

Per continuare la configurazione dei monitor, fare clic sulla scheda **Deviazione** e fare clic su **Inizia**. Per ulteriori informazioni, consultare [Configurazione del monitor Rilevamento deviazione](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
