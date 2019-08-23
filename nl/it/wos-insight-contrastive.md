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

# Le spiegazioni contrastanti usano i positivi e i negativi pertinenti
{: #ie-pp-pn}

Per le spiegazioni contrastanti, {{site.data.keyword.aios_short}} visualizza i valori positivi e negativi pertinenti.
{: shortdesc}

- I positivi pertinenti sono i risultati che sono fondamentali per determinare cos'è un elemento.
- I negativi Pertinenti sono non-risultati importanti per la loro assenza.

{{site.data.keyword.aios_short}} visualizza sempre un positivo pertinente, tuttavia, a volte non ci sono negativi pertinenti da visualizzare. In tal caso, i valori per questa funzione sono già alla media o la previsione non è cambiata successivamente al passaggio dei valori lontano dalla media.

Per capire meglio questo concetto, considerare che quando {{site.data.keyword.aios_short}} calcola il valore negativo pertinente, cambia i valori di tutte le funzioni lontane dal valore medio. Per i negativi pertinenti questo significa i valori di funzione che sono più lontani dalla media. Se i valori di un punto di dati sono già alla media o se anche dopo ilpassaggio del valore lontano dalla media, la previsione non cambia, quindi non ci sono negativi pertinenti da visualizzare. In caso di positivi pertinenti, {{site.data.keyword.aios_short}} trova la variazione massima nei valori di funzione verso la media cosicché previsione non cambia. Praticamente, questo significa che c'è quasi sempre un positivo pertinente per spiegare una transazione.

