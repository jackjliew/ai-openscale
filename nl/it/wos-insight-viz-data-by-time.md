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

# Visualizzazione dei dati per un'ora specifica
{: #it-vdet}

Per visualizzare i dettagli dietro una determinata statistica di correttezza, fare clic sul grafico per un orario specifico. Si apre una visualizzazione dei punti di dati per una funzione monitorata all'ora selezionata. In seguito all'esempio precedente viene visualizzata la funzione Age nel seguente esempio.
{: shortdesc}

Notare i tre filtri in alto nella pagina (Funzione, Data e Ora) che permettono di selezionare una funzione o un tempo diversi per esaminare i dettagli.

![Viene visualizzato il grafico delle serie temporali con colonne che rappresentano il payload e i dati perturbati per età e numero di risultati favorevoli](images/wos-insight-data-detail.png)

## Interpretazione del grafico
{: #it-intp}

Il grafico mostra più cose:

- Si può osservare la popolazione che sperimenta la distorsione (i clienti tra i 18 e i 23 anni). Il grafico mostra anche la percentuale di risultati previsti per questa popolazione.

- Il grafico mostra anche la percentuale di risultati previsti (70%) per la popolazione di riferimento. Questa è la media dei risultati previsti in tutte le popolazioni di riferimento.

- Il grafico indica la presenza di distorsione, perché il rapporto tra la percentuale di risultati previsti per le popolazioni di età tra i 18 e i 23 anni e la percentuale di risultati previsti per la popolazione di riferimento che supera la soglia. In altre parole, 0.52/0.7 = 0.74, che è inferiore alla soglia 0.8.

- Il grafico mostra anche la distribuzione dei valori di riferimento e monitorati per ogni valore distinto dell'attributo nei dati della tabella payload che è stata analizzata per identificare la distorsione. In altre parole, se l'algoritmo di rilevamento della distorsione ha analizzato gli ultimi 1790 record dalla tabella di payload, per 120 di questi record l'età del cliente era tra i 18 e i 23, e fuori da quella distribuzione i risultati `Approvato` e `Denied` sono rappresentati dal grafico a barre. La distribuzione dei dati di payload viene visualizzata per ogni valore distinto dell'attributo di correttezza (sono visualizzati anche i valori di riferimento). Queste informazioni possono essere utilizzate per correlare la distorsione con la quantità di dati ricevuti dal modello.

- Il grafico mostra inoltre che la popolazione con età compresa tra i 31 e i 35 anni ha ricevuto il 91% di risultati previsti. Ciò indica l'origine della distorsione, il che significa che tali dati in questo gruppo hanno reso asimmetrici i risultati e hanno portato ad un aumento della percentuale dei risultati previsti per la classe di riferimento. Queste informazioni possono essere utilizzate per identificare parti dei dati che possono poi essere sotto-campionate quando si riesegue il training del modello.

- Un'altra cosa importante che il grafico mostra è il nome della tabella contenente i dati che sono stati identificati per l'etichettatura manuale. Ogni volta che l'algoritmo rileva la distorsione in un modello, identifica anche i punti di dati che possono essere inviati per l'etichettatura manuale da parte di persone. Questi dati etichettati manualmente possono poi essere utilizzati con i dati di training originali per rieseguire il training del modello. Questo modello risottoposto a training è probabile che non abbia la distorsione. La tabella di etichettatura manuale è presente nel database associato con all'istanza {{site.data.keyword.aios_short}}.
