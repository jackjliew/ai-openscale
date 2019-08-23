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

# Opzioni di annullamento distorsione
{: #it-dbo}

{{site.data.keyword.aios_short}} utilizza due tipi di annullamento della distorsione: passivo e attivo. La modalità passiva permette di sapere l'entità della distorsione, mentre quella attiva impedisce la prosecuzione della distorsione modificando il modello in tempo reale per l'applicazione corrente.

- *Annullamento distorsione passivo* - l'annullamento distorsione passivo è il lavoro che OpenScale fa da solo, automaticamente, ogni ora. È considerato passivo perché si verifica senza l'intervento dell'utente. Quando {{site.data.keyword.aios_short}} esegue il controllo della distorsione effettua anche un annullamento della distorsione dei dati analizzando il comportamento del modello e identificando i dati in cui il modello contribuisce alla distorsione.

  {{site.data.keyword.aios_short}} poi creare un modello di machine learning per prevedere se è probabile che il modello contribuirà alla distorsione su un nuovo punto di dati fornito. {{site.data.keyword.aios_short}} poi analizza i dati ricevuti dal modello, su base oraria, e trova i punti di dati in cui {{site.data.keyword.aios_short}} crede che il modello stia contribuendo alla distorsione. Per questi punti di dati, l'attributo di correttezza è perturbato da minoranza a maggioranza, e i dati perturbati vengono inviati al modello originale per la previsione. Questa previsione del modello originale viene utilizzata come output con distorsione annullata.

  {{site.data.keyword.aios_short}} esegue questo annullamento della distorsione ogni ora, su tutti i dati che sono stati ricevuti dal modello nell'ultima ora. Calcola anche la correttezza per l'output con distorsione annullata e lo visualizza nella scheda **Modello con distorsione annullata**.

- *Annullamento distorsione attivo* - l'annullamento distorsione attivo dà all'utente la possibilità di richiedere e portare i risultati senza distorsione nell'applicazione attraverso l'endpoint API REST. È possibile indirizzare in modo attivo {{site.data.keyword.aios_short}} verso l'esecuzione dell'annullamento della distorsione e la modifica del modello in modo da poter eseguire l'applicazione senza distorsione. In modalità di annullamento distorsione attiva è possibile utilizzare un endpoint API REST di annullamento distorsione dall'applicazione. Questo endpoint API REST richiamerà internamente il modello e ne verificherà il comportamento.

  Se {{site.data.keyword.aios_short}} rileva che il modello sta contribuendo alla distorsione, perturba i dati, come descritto in precedenza, e li invia di nuovo al modello originale. L'output del modello originale sui dati perturbati sarà restituito come previsione senza distorsione. Se {{site.data.keyword.aios_short}} determina che il modello originale non sta agendo in modo distorto, {{site.data.keyword.aios_short}} restituirà la previsione del modello originale come previsione senza distorsione. Pertanto, utilizzando questo endpoint API REST, è possibile assicurarsi che l'applicazione non prenda decisione in base all'output distorto dei modelli.

Selezionare il link **Endpoint di calcolo del punteggio di distorsioni annullate** per trovare l'endpoint API REST di annullamento distorsione

![viene visualizzato il pannello Endpoint API annullamento distorsione con l'esempio cURL nella casella del frammento di codice](images/insight-debias-api.png)

## Passi successivi
{: #it-dbo-nextsteps}

- Per attenuare la distorsione, dopo che è stata rilevata, è necessario creare una nuova versione del modello che risolva il problema. {{site.data.keyword.aios_short}} memorizza i record distorti nella tabella di etichettatura manuale. Questi record distorti devono essere etichettati manualmente e poi il modello deve essere risottoposto a training utilizzando questi dati aggiuntivi per creare una nuova versione del modello che è senza distorsione. 


