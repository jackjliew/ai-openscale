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

# Spiegazione di modelli di testo non strutturato
{: #ie-unstruct}

{{site.data.keyword.aios_short}} supporta l'esplicabilità per i dati di testo non strutturato.
{: shortdesc}

## Utilizzo di modelli di testo non strutturato
{: #ie-unstruct-steps}

1. Configurare l'ambiente.
   2. Installare i pacchetti {{site.data.keyword.aios_short}} e {{site.data.keyword.pm_full}}.
   3. Configurare le credenziali.
   4. Installare le librerie necessarie per la creazione dei modelli e l'esecuzione dell'analisi. Queste includono le seguenti librerie:
      - `pandas`
      - `pyspark` (se non si utilizza {{site.data.keyword.DSX}})

1. Creare e distribuire il modello basato sull'immagine.
   2. Caricare i dati di training in un frame pandas.
   2. Addestrare il modello sui dati.
   3. Pubblicare il modello.
   4. Distribuire e calcolare il punteggio del modello.

7. Configurare {{site.data.keyword.aios_short}} assegnando `APIClient`, sottoscrivendo l'asset e calcolando il punteggio del modello.
8. Configurare l'esplicabilità.
   9. Abilitare l'esplicabilità.
   10. Ottenere le spiegazioni per le transazioni.

## Spiegazione di transazioni di testo non strutturato
{: #ie-unstruct-xplan}

Il seguente esempio di esplicabilità mostra un modello di classificazione che valuta il testo non strutturato. La spiegazione mostra le parole chiave che hanno avuto un impatto positivo oltre che un impatto negativo sulla previsione del modello. Viene anche mostrata la posizione delle parole chiave identificate nel testo originale che è stato inserito come input nel modello.

![Viene visualizzato il grafico Esplicabilità - classificazione immagine, con i livelli di confidenza per il testo non strutturato](images/insight-explain-text.png)

## Esempio di modello di testo non strutturato
{: #ie-unstruct-ntbkssample}

Utilizzare il seguente notebook per visualizzare esempi di codice dettagliati e sviluppare le proprie distribuzioni {{site.data.keyword.aios_short}}:

- [Supporto didattico sulla generazione di una spiegazione per un modello basato sul testo](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

