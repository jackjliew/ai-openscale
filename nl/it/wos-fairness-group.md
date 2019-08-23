---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# Correttezza per un gruppo
{: #quality_group}

La correttezza per una metrica di gruppo dà la propensione del modello ad offrire risultati favorevoli ad un gruppo rispetto a un altro. È possibile utilizzare qualsiasi gruppo, ad es. age, sex o race.
{: shortdesc}

## Correttezza per un gruppo a colpo d'occhio
{: #quality_group-glance}

- **Descrizione**: la propensione del modello ad offrire risultati favorevoli ad un gruppo rispetto a un altro.
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**: l'endpoint di calcolo del punteggio senza distorsione che è possibile utilizzare nell'applicazione aziendale per ricevere risposte senza distorsione dal modello distribuito.
- **Tipo di problema**: tutti
- **Tipo di dati**: strutturati
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: sì

## Attributi protetti
{: #quality_group-atts}

{{site.data.keyword.aios_short}} identifica automaticamente se sono presenti attributi protetti noti in un modello. Quando {{site.data.keyword.aios_short}} rileva tali attributi, raccomanda automaticamente di configurare i monitor della distorsione per ogni attributo presente, per garantire che venga tracciata in produzione la distorsione su tali attributi potenzialmente sensibili. 

### sex
{: #quality_group-sex}

{{site.data.keyword.aios_short}} raccomanda che all'interno dell'attributo **Sex**, il monitor di distorsione sia configurato in modo tale che `Woman` e `Non-Binary` siano i valori monitorati e `Male` sia il valore di riferimento. 

### ethnicity
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}} raccomanda che all'interno dell'attributo **ethnicity**, il monitor di distorsione sia configurato in modo tale che `White-caucasian` sia il valore di riferimento mentre altre etnie siano valori monitorati.

### marital status
{: #quality_group-marital}

{{site.data.keyword.aios_short}} raccomanda che all'interno dell'attributo **marital status**, il monitor di distorsione sia configurato in modo tale che `married`  sia il valore di riferimento e `single` sia il valore monitorato.

### age
{: #quality_group-age}

{{site.data.keyword.aios_short}} raccomanda che all'interno dell'attributo **age**, il monitor di distorsione sia configurato in modo tale che l'intervallo di età produca annullamento di distorsione utile.

### zip code
{: #quality_group-zip}

{{site.data.keyword.aios_short}} raccomanda che all'interno dell'attributo **zip code**, il monitor di distorsione sia configurato in modo tale che sia effettuato il calcolo del punteggio dei singoli CAP.

## Interpretazione del pannello
{: #quality_group-display}

### Punteggio di correttezza per un gruppo
{: #quality_group-display-fairnessscore}



### Gruppi monitorati
{: #quality_group-display-monitoredgroups}



### Pianifica
{: #quality_group-display-schedule}

Il riquadro **Pianifica** mostra  



