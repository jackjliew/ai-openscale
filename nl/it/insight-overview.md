---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Navigazione nel dashboard
{: #io-ov}

È possibile tenere traccia di tutte le distribuzioni che si stanno monitorando tramite il dashboard {{site.data.keyword.aios_short}}. Il dashboard è la vista principale in {{site.data.keyword.aios_short}}. Il dashboard è costituito dalle seguenti schede:

  ![Schede Insight](images/insight-tabs.png)

{: shortdesc}

## Insight
{: #io-ins}

La scheda **Insight** (![dashboard Insight](images/insight-dash-tab.png)) fornisce una vista di alto livello del monitoraggio della distribuzione.

  ![dashboard Insight](images/insight-dashboard.png)

- ***Deployments Monitored*** - In questo esempio, si stanno monitorando 10 distribuzioni in totale. Otto delle dieci distribuzioni sono mostrate come singoli riquadri sotto.

- ***Accuracy Alerts*** - Un totale di 3 avvisi di accuratezza sono rappresentati nei riquadri sotto con ombreggiatura viola. In questo esempio, le distribuzioni `Driver Performance`, `Market Analytics` e `Pricing Risk` mostrano i valori di accuratezza di `60%`, `65%`,  e `79%`, rispettivamente.

- ***Fairness Alerts*** - C'è un totale di 6 avvisi di correttezza, rappresentati nei riquadri sotto con ombreggiatura viola e una piccola etichetta `BIAS`. In questo esempio, le distribuzioni `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization` e `Damage Cost Estimator` mostrano valori di correttezza di `59%`, `68%`, `62%`, `64%`, `79%`, e `63%`, rispettivamente.

Ogni riquadro fornisce un riepilogo dell'attività di monitoraggio per quella distribuzione. Notare che il riquadro della distribuzione `Call Center Routing` non mostra alcun problema, ciò indica un modello abbastanza stabile e accurato.

### Passi successivi
{: #io-next}

Selezionare uno dei riquadri di distribuzione per visualizzare altri dettagli sulla distribuzione. Per ulteriori informazioni, consultare [Monitoraggio della correttezza, Richieste medie al minuto e Accuratezza](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e [Monitoraggio esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Configurazione
{: #io-conf}

La scheda **Configura** (![scheda Configura](images/insight-config-tab.png)) apre un Riepilogo di configurazione per la distribuzione selezionata.

  ![Riepilogo configurazione](images/insight-config-summary.png)

Da qui, è possibile modificare direttamente le impostazioni di configurazione per il monitor di distribuzione.

## Transazioni
{: #io-tran}

Utilizzare la scheda **Spiega una transazione** (![scheda Spiega una transazione](images/insight-transact-tab.png)) per ricercare un ID di transazione specifico per spiegare una specifica transazione di distribuzione. Per ulteriori informazioni, consultare [Monitoraggio esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Scheda Guida
{: #io-help}

La scheda Guida (![scheda Transazioni](images/insight-help-tab.png)) fornisce ulteriori informazioni di aiuto per utilizzare {{site.data.keyword.aios_short}}.
