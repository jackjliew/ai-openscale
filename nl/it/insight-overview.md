---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

È possibile tenere traccia di tutte le distribuzioni che si stanno monitorando tramite il dashboard {{site.data.keyword.aios_short}}. Il dashboard è la vista principale in {{site.data.keyword.aios_short}}. Il dashboard è composto di cinque schede: 

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

La scheda **Spiega una transazione** (![scheda Spiega una transazione](images/insight-transact-tab.png)) consente di ricercare un ID di transazione specifico per spiegare una specifica transazione di distribuzione. Per ulteriori informazioni, consultare [Monitoraggio esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Strumenti AI
{: #io-too}

La scheda **Strumenti AI** (![scheda Strumenti AI](images/aitools.png)) apre una finestra di dialogo che fornisce un link a opzioni aggiuntive di strumenti AI di IBM:

- *[Piano Lite Watson Studio ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*: Watson Studio fornisce l'ambiente e gli strumenti per analizzare e  visualizzare i dati, per ripulire e modellare i dati, per inserire i dati streaming, o per creare, addestrare e distribuire modelli di machine learning. Fare clic sul link "Registrati per il piano Lite gratuito di Watson Studio" per andare a Watson Studio.

- *[NeuNetS ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}* (*Beta*): Neural Network Synthesizer, o "NeuNetS", correntemente in beta release, permette di sintetizzare i modelli AI utilizzando la tecnologia {{site.data.keyword.aios_short}} in Watson Studio. Fare clic sul pulsante "Sintetizza un modello" per utilizzare NeuNetS.

  ![finestra di dialogo NeuNetS](images/neunets-dialog.png)

## Scheda Guida
{: #io-help}

La scheda Guida (![scheda Transazioni](images/insight-help-tab.png)) fornisce ulteriori informazioni di aiuto per utilizzare {{site.data.keyword.aios_short}}.
