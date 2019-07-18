---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: drift, behavior, metrics

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

# Rilevamento deviazione ![tag beta](images/beta.png)
{: #behavior-drift-ovr}

Nel corso del tempo, l'importanza e l'impatto di alcune funzioni in un modello cambiano. Ciò influisce sulle applicazioni associate e sugli esiti risultanti. Attraverso il rilevamento della deviazioe, {{site.data.keyword.aios_short}} fornisce un modo per tracciare le metriche del modello, le prestazioni del modello e il modo in cui i pesi delle funzioni cambiano nel tempo. 
{: shortdesc}

## Cos'è il rilevamento deviazione
{: #behavior-drift-understand}

La deviazione è il degrado delle prestazioni predittive nel tempo a causa di contesto nascosto. Man mano che i dati cambiano nel tempo, la capacità del modello di fare previsioni accurate può degradare. {{site.data.keyword.aios_short}} rileva ed evidenzia la deviazione in modo da poter intraprendere un'azione correttiva.

### Funzionamento
{: #behavior-drift-works}

{{site.data.keyword.aios_short}} analizza tutte le transazioni per trovare quelli che contribuiscono alla deviazione. Successivamente, raggruppa i record in base ai valori attributo che più significativamente hanno contribuito alla deviazione.

### Calcolo matematico
{: #behavior-drift-math}

Ogni tre ore, {{site.data.keyword.aios_short}} calcola la deviazione analizzando gli stessi dati di training già analizzati dal modello predittivo. Poi confronta i risultati con le previsioni del modello. Dove ci sono modifiche o discrepanze, {{site.data.keyword.aios_short}} calcola l'entità della deviazione e, in base alla soglia che si imposta, avvisa dell'evento. 


### Visualizzazione della deviazione
{: #behavior-drift-display}

La visualizzazione alla deviazione comprende dati statistici sia grafici che numerici:

![grafico delle metriche di correttezza che mostra la deviazione al di sotto della soglia impostata](images/drift-example.png)

Facendo clic sul grafico, vengono visualizzate le specifiche transazioni che contribuiscono alla deviazione. Vengono visualizzati i motivi principali per la deviazione individuata e una descrizione in linguaggio naturale dell'osservazione così come l'elenco dei valori inattesi.

![grafico delle metriche di correttezza che mostra la deviazione al di sotto della soglia impostata](images/drift-detection-example.png)

Le transazioni con deviazione sono disponibili nella schermata dei dettagli della transazione, dove è possibile fare clic su **Spiega** per capire come una transazione specifica è finita nella categoria di deviazione:

![grafico delle metriche di correttezza che mostra la deviazione al di sotto della soglia impostata](images/drift-detection-transactions.png)


## Passi successivi

- Per informazioni su come interpretare la deviazione, consultare [Configurazione del monitor di rilevamento della deviazione](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)
- Aumentare l'IQ di deviazione leggendo [Comprensione della deviazione modello con IBM Watson OpenScale](https://medium.com/@manish.bhide/4c5401aa8da4)
