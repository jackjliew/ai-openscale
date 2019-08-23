---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: dashboard, navigating, navigation, insights

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

# Acquisizione degli insight con {{site.data.keyword.aios_short}}
{: #io-ov}

È possibile tenere traccia di tutte le distribuzioni che si stanno monitorando tramite il dashboard {{site.data.keyword.aios_full}}. Il dashboard è la vista principale in {{site.data.keyword.aios_short}} e fornisce i mezzi per ottenere gli insight su come stanno funzionando i modelli.
{: shortdesc}

## Insight
{: #io-ins}

La scheda **Insight** (![dashboard Insight](images/insight-dash-tab.png)) fornisce una vista di alto livello del monitoraggio della distribuzione.

  ![dashboard Insight](images/insight-dashboard.png)

- ***Deployments Monitored*** - In questo esempio, si stanno monitorando 10 distribuzioni in totale. Otto delle dieci seguenti distribuzioni sono mostrate come singoli riquadri.

- ***Quality Alerts*** - Un totale di 3 avvisi di qualità (precedentemente denominati avvisi di accuratezza) sono rappresentati nei seguenti riquadri. In questo esempio, le distribuzioni `Driver Performance`, `Market Analytics` e `Pricing Risk` mostrano i valori di accuratezza di `60%`, `65%`,  e `79%`, rispettivamente.

- ***Fairness Alerts*** - C'è un totale di 6 avvisi di correttezza, rappresentati nei seguenti riquadri e da una piccola etichetta `BIAS`. In questo esempio, le distribuzioni `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization` e `Damage Cost Estimator` mostrano valori di correttezza di `59%`, `68%`, `62%`, `64%`, `79%`, e `63%`, rispettivamente.

Ogni riquadro fornisce un riepilogo dell'attività di monitoraggio per quella distribuzione. Notare che il riquadro della distribuzione `Call Center Routing` non mostra alcun problema, ciò indica un modello abbastanza stabile e accurato.


## Insight su correttezza, qualità, prestazioni, accuratezza e analytics
{: #it-ov}

Selezionare uno dei riquadri di distribuzione per visualizzare altri dettagli sulla distribuzione. Vengono visualizzati in una serie di grafici i dati di monitoraggio per le singole distribuzioni. I grafici tracciano le metriche, come ad esempio la correttezza, le richieste medie al minuto, e la precisione in giorni, settimane o mesi.

- [Visualizzazione dei dati per una distribuzione](/docs/services/ai-openscale?topic=ai-openscale-it-vdep)
- [Visualizzazione dei dati per un'ora specifica](/docs/services/ai-openscale?topic=ai-openscale-it-vdet)
- [Correttezza](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)
- [Qualità](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)
- [Deviazione](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
- [Prestazioni](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_performance)
- [Analytics](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)
- [Opzioni di annullamento distorsione](/docs/services/ai-openscale?topic=ai-openscale-it-dbo)

## Esplicabilità
{: #io-tran}

Utilizzare la scheda **Spiega una transazione** (![scheda Spiega una transazione](images/insight-transact-tab.png)) per ricercare un ID di transazione specifico per spiegare una specifica transazione di distribuzione.

- [Spiegazione transazioni](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)
- [Spiegazione di modelli categoriali](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Spiegazione di modelli immagine](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Spiegazione di modelli di testo non strutturato](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Spiegazioni contrastanti](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)

## Passi successivi
{: #io-next}

- [Aggiungere ulteriori distribuzioni da monitorare](/docs/services/ai-openscale?topic=ai-openscale-dpl-select).

