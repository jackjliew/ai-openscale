---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Motore di machine learning personalizzato
{: #fmrk-workaround-customengine}

Un motore di machine learning personalizzato fornisce l'infrastruttura e le capacità di hosting per i modelli di machine learning e le applicazioni web. I motori di machine learning personalizzati supportati da {{site.data.keyword.aios_short}} devono essere conformi ai seguenti requisiti:

- Esporre due tipi di endpoint API REST:

   * endpoint di rilevamento (fornisce l'elenco di distribuzioni e i dettagli)
   * endpoint di calcolo del punteggio (calcolo del punteggio online e in tempo reale)

- Per essere supportati, tutti gli endpoint devono essere compatibili con la specifica swagger.

- Il payload di input e l'output da o verso la distribuzione devono essere compatibili con il formato file JSON descritto nella specifica.

In questa fase sono supportati solo i formati `BasicAuth` o `none`.
{: Note}

Il seguente esempio mostra la specifica degli endpoint API REST:

![Viene visualizzata la specifica degli endpoint API REST dal documento swagger](images/wosdeployments.png)


Il seguente esempio mostra il formato per un payload di input:

![Viene visualizzato l'esempio di payload di input](images/wosinputdata.png)


## Quando un motore di machine learning personalizzato rappresenta la scelta migliore?
{: #fmrk-workaround-enging-choice}

Un motore di machine learning personalizzato rappresenta la scelta migliore quando le seguenti situazioni sono vere:

- Non si utilizza alcun prodotto pronto all'uso disponibile per servire i modelli di machine learning. È stato appena sviluppato il proprio sistema per farlo. Non c'è e non ci sarà alcun supporto diretto in {{site.data.keyword.aios_short}} per questo.
- Il motore di servizio che si sta utilizzando da un fornitore di terze parti non è ancora supportato da {{site.data.keyword.aios_short}}. In questo caso, considerare di sviluppare un motore di machine learning personalizzato come un wrapper per le distribuzioni originali o native.

## Passi successivi
{: #fmrk-workaround-nxt-steps-over}

Implementare la propria soluzione utilizzando uno di questi [Esempi di machine learning personalizzato](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).
