---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Spiegazione di modelli immagine
{: #ie-image}

{{site.data.keyword.aios_short}} supporta l'esplicabilità dei dati immagine.
{: shortdesc}

## Utilizzo di un modello immagine
{: #ie-image-working}

1. Configurare l'ambiente.
   2. Installare i pacchetti {{site.data.keyword.aios_short}} e {{site.data.keyword.pm_full}}.
   3. Configurare le credenziali.
   4. Installare le librerie necessarie per la creazione dei modelli e l'esecuzione dell'analisi. Queste includono le seguenti librerie:
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. Creare e distribuire il modello basato sull'immagine.
   2. Creare le cartelle per le immagini in base a come le si classifica.
       - All'interno della directory principale `data` è necessario avere le sottodirectory `train` e `validation`.
       - All'interno di ciascuna delle sottodirectory, è necessario avere le directory di classificazione.
  2. Standardizzare la dimensione dell'immagine e impostare le sottodirectory da utilizzare per il training e la convalida.
  3. Preprocessare i dati per ridimensionare e recuperare le immagini e le loro classi.
  4. Definire e addestrare il modello.
  5. Memorizzare il modello.
  6. Distribuire il modello.

7. Configurare {{site.data.keyword.aios_short}} assegnando `APIClient`, sottoscrivendo l'asset e calcolando il punteggio del modello.
8. Configurare l'esplicabilità.
   9. Abilitare l'esplicabilità.
   10. Ottenere le spiegazioni per le transazioni.
   11. Visualizzare le immagini spiegate. 

## Spiegazione delle transazioni modello immagine
{: #ie-image-workingviewing}

Per un esempio di esplicabilità di un modello di classificazione immagine, si possono vedere quali parti di un'immagine hanno contribuito positivamente al risultato previsto e quali hanno contribuito negativamente. Nel seguente esempio, l'immagine nel riquadro positivo mostra le parti che hanno impattato positivamente la previsione e l'immagine nel riquadro negativo mostra le parti di immagini che hanno avuto un impatto negativo sul risultato.

![Vengono visualizzati i dettagli per la confidenza di Esplicabilità - classificazione immagine, con l'immagine di un cane, con parti dell'immagine evidenziate per mostrare quale parte ha aiutato a determinare che l'immagine è un cane](images/insight-explain-image.png)

Per {{site.data.keyword.pm_full}}, l'input di calcolo del punteggio per i modelli di classificazione dell'immagine inviati per la registrazione del payload non può superare ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service MB. Per evitare problemi di timeout, le immagini non devono superare 125 x 125 pixel e devono essere inviate in sequenza in modo che la spiegazione per la seconda immagine sia richiesta quando la prima è completata.
{: note}


## Esempi di modello immagine
{: #ie-image-working-ntbks}

Utilizzare i seguenti due notebook per visualizzare esempi di codice dettagliati e sviluppare le proprie distribuzioni {{site.data.keyword.aios_short}}:

- [Supporto didattico sulla generazione di una spiegazione per un modello basato sull'immagine](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Supporto didattico sulla generazione di una spiegazione per un modello classificatore binario basato sull'immagine](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

