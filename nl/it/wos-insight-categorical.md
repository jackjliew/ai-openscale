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

# Spiegazione di un modello categoriale
{: #ie-class}

Questo esempio di esplicabilità è per un modello di classificazione binaria che approva o rifiuta le richieste di risarcimento. È possibile visualizzare i fattori che hanno contribuito in modo positivo o negativo al risultato finale di `DENIED` in questo caso.
{: shortdesc}

La funzione *POLICY AGE* che ha un valore di `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear` ha avuto l'impatto massimo nel modello per decidere un risultato DENIED. Le altre funzioni che hanno contribuito a questo risultato sono state *CLAIM FREQUENCY* (`High`) e *AGE* (`18`), con solo un impatto minore da *CAR VALUE* (`$50,000`).

![viene visualizzata la classificazione binaria dell'esplicabilità con i dettagli sulle richieste negate e approvate](images/insight-explain-binary.png)

Mentre i grafici sono utili nel mostrare i fattori più significativi che hanno determinato il risultato di una transazione, i modelli di classificazione possono includere anche spiegazioni avanzate, dettagliate nelle sezioni `Minimum changes for Approved outcome` e `Minimum changes for this outcome`.

Spiegazioni avanzate non sono disponibili per modelli di regressione, immagini e testo non strutturato.
{: note}

Il campo `Minimum changes for Approved outcome` indica che, se i valori delle funzioni sono cambiati nei valori elencati in questa sezione, la previsione del modello cambierà.

Allo stesso modo, il campo `Minimum changes for this outcome` indica che, anche se i valori delle funzioni fossero stati modificati in quelli elencati in questa sezione, la previsione del modello non sarebbe cambiata.

Pertanto, questi due valori indicano il comportamento del modello nelle vicinanze del punto di dati per il quale si genera la spiegazione.

![dettagli della classificazione binaria dell'esplicabilità con le modifiche minime che servirebbero per cambiare i risultati](images/insight-explain-binary2.png)
