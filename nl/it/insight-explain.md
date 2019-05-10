---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

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

# Monitoraggio esplicabilità
{: #ie-ov}

Per ogni distribuzione, è possibile vedere i dati di esplicabilità per transazioni specifiche.
{: shortdesc}

## Spiegazione transazioni
{: #ie-view}

Nel riquadro della distribuzione selezionata, selezionare la scheda **Spiega una transazione** (![scheda Spiega una transazione](images/insight-transact-tab.png)) nel navigator e immettere un ID transazione.

Ogni volta che i dati vengono inviati al modello per il calcolo del punteggio, imposta un ID transazione nell'intestazione HTTP impostando il campo `X-Global-Transaction-Id`. Questo ID di transazione viene memorizzato nella tabella payload. Per trovare una spiegazione del funzionamento del modello per un particolare calcolo del punteggio, specificare l'ID transazione associato alla richiesta di calcolo del punteggio. Si noti che questo comportamento si applica solo alle transazioni WML (Watson Machine Learning) e non è applicabile alle transazioni non WML.
{: note}

### Ricerca di un ID transazione in {{site.data.keyword.aios_short}}
{: #ie-find}

1.  Dal grafico temporale per la propria distribuzione, scorrere il puntatore nel grafico e fare clic sul link **Visualizza dettagli** per [visualizzare i dati per un'ora specifica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Fare clic sul pulsante **Visualizza transazioni** per [visualizzare l'elenco di ID transazione](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copiare uno degli ID transazione dall'elenco, incollarlo nella casella di ricerca sulla pagina **Spiega una transazione** e premere Invio.

    L'elenco di ID transazione offre anche la possibilità di fare semplicemente clic sul link **Spiega** nella colonna Azione per qualsiasi ID di transazione, ciò aprirà quella transazione nella scheda Esplicabilità.
    {: note}

  Consultare le seguenti sezioni per esempi di spiegazioni per diversi tipi di modelli.

  ![Esplicabilità - ID transazione](images/insight-explain-trans-id.png)

## Esempio di modello categoriale
{: #ie-class}

Questo esempio di esplicabilità è per un modello di classificazione binaria che approva o rifiuta le richieste di risarcimento. È possibile visualizzare i fattori che hanno contribuito in modo positivo o negativo al risultato finale di `DENIED` in questo caso.

La funzione *POLICY AGE* che ha un valore di `< 1 year` ha avuto l'impatto massimo nel modello per decidere un risultato DENIED. Le altre funzioni che hanno contribuito a questo risultato sono state *CLAIM FREQUENCY* (`High`) e *AGE* (`18`), con solo un impatto minore da *CAR VALUE* (`$50,000`).

![Esplicabilità - classificazione binaria](images/insight-explain-binary.png)

Mentre i grafici sono utili nel mostrare i fattori più significativi che hanno determinato il risultato di una transazione, i modelli di classificazione possono includere anche spiegazioni avanzate, dettagliate nelle sezioni `Minimum changes for Approved outcome` e `Minimum changes for this outcome`.

Spiegazioni avanzate non sono disponibili per modelli di regressione, immagini e testo non strutturato.
{: note}

Il campo `Minimum changes for Approved outcome` indica che, se i valori delle funzioni sono cambiati nei valori elencati in questa sezione, la previsione del modello cambierà. 

Allo stesso modo, il campo `Minimum changes for this outcome` indica che, anche se i valori delle funzioni fossero stati modificati in quelli elencati in questa sezione, la previsione del modello non sarebbe cambiata.

Pertanto, questi due valori indicano il comportamento del modello nelle vicinanze del punto di dati per il quale si genera la spiegazione.

![Esplicabilità - classificazione binaria](images/insight-explain-binary2.png)

## Esempio di modello immagine
{: #ie-image}

Per un esempio di esplicabilità di un modello di classificazione immagine, si possono vedere quali parti di un'immagine hanno contribuito positivamente al risultato previsto e quali hanno contribuito negativamente. Nell'esempio sotto riportato, l'immagine sulla destra mostra le parti che hanno impattato positivamente la previsione e l'immagine a sinistra mostra le parti di immagini che hanno avuto un impatto negativo sul risultato.

Attualmente le spiegazioni non possono essere generate per le immagini di dimensione maggiore di 1 MB.
{: note}

![Esplicabilità - classificazione immagine](images/insight-explain-image.png)

## Esempio di modello di testo non strutturato
{: #ie-unstruct}

Infine, questo esempio di esplicabilità mostra un modello di classificazione che valuta il testo non strutturato. La spiegazione mostra le parole chiave che hanno avuto un impatto positivo oltre che un impatto negativo sulla previsione del modello. Viene anche mostrata la posizione delle parole chiave identificate nel testo originale che è stato inserito come input nel modello.

![Esplicabilità - classificazione immagine](images/insight-explain-text.png)
