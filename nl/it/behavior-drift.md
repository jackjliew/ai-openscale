---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

Nel corso del tempo, l'importanza e l'impatto di alcune funzioni in un modello cambiano. Ciò influisce sulle applicazioni associate e sugli esiti risultanti. Attraverso il rilevamento della deviazioe, {{site.data.keyword.aios_short}} fornisce un modo per tracciare le metriche del modello, le prestazioni del modello e il modo in cui i pesi delle funzioni cambiano nel tempo. La deviazione è il degrado delle prestazioni predittive nel tempo a causa di contesto nascosto. Man mano che i dati cambiano nel tempo, la capacità del modello di fare previsioni accurate può degradare. {{site.data.keyword.aios_short}} rileva ed evidenzia la deviazione in modo da poter intraprendere un'azione correttiva.
{: shortdesc}

{{site.data.keyword.aios_short}} analizza tutte le transazioni per trovare quelli che contribuiscono alla deviazione. Successivamente, raggruppa i record in base ai valori attributo che più significativamente hanno contribuito alla deviazione. 

## Deviazione a colpo d'occhio
{: #behavior-drift-glance}




## Interpretazione del pannello
{: #behavior-drift-display}

![grafico delle metriche di correttezza che mostra la deviazione al di sotto della soglia impostata](images/fairness_metrics_001.png)


## Calcolo matematico
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} calcola la deviazione 
