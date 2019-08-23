---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Python, install, python module, setup, set up, insights, explainability

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

# Installazione di un modulo Python per configurare {{site.data.keyword.aios_short}}
{: #as-module}

Per automatizzare il provisioning e la configurazione dei servizi {{site.data.keyword.cloud_notm}} richiesti e consultare un'applicazione {{site.data.keyword.aios_full}}, inclusi i dati di esempio, è possibile installare un modulo Python.
{: shortdesc}

## Informazioni su questo modulo
{: #as-about}

- Il modulo fornisce un modo alternativo per gli utenti tecnici per visualizzare un'istanza di {{site.data.keyword.aios_short}} in esecuzione senza dover eseguire il provisioning e la configurazione dei servizi da soli, come descritto nel supporto didattico [Introduzione](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted).
- Il modulo Python percorre il processo di controllo dei servizi di cui si dispone e di creazione di quelli necessari, tra cui {{site.data.keyword.aios_short}}. Dopo che il modulo è stato eseguito correttamente, dal dashboard {{site.data.keyword.cloud_notm}} è possibile avviare {{site.data.keyword.aios_short}} per visualizzare il modo in cui monitora un modello.

## Prima di iniziare
{: #as-prereqs}

1. [Creare una chiave API {{site.data.keyword.cloud_notm}} e scaricarla](/docs/iam?topic=iam-userapikey#create_user_key){: external}. Sarà necessario immettere la chiave API in un passo successivo.

2. [Installare qualsiasi release di Python 3](https://www.python.org/downloads/){: external}.

  Python 3 include il sistema di gestione del pacchetto pip richiesto.
  {: note}

3. Installare il pacchetto `ibm-ai-openscale-cli` mediante l'esecuzione del seguente comando:

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    Se sul sistema è installata più di una versione di pip, potrebbe essere necessario eseguire `pip3` invece di `pip`, ad esempio `pip3 install -U ibm-ai-openscale-cli`.
    {: tip}

4. Se si dispone già di un'istanza del servizio {{site.data.keyword.pm_short}}, controllare il dashboard [{{site.data.keyword.cloud_notm}}](https://{DomainName}){: external} per verificare che il servizio sia gestito da {{site.data.keyword.iamshort}} (IAM), non da Cloud Foundry.

  **Importante**: il modulo cerca un'istanza di {{site.data.keyword.pm_short}}. Se si dispone di un'istanza, il modulo la utilizza. Se l'istanza è gestita da Cloud Foundry, è necessario [migrarla a un gruppo di risorse IAM prima di poter eseguire il modulo. ](/docs/resources?topic=resources-migrate#migrate).

## Esecuzione del modulo
{: #as-run}

Eseguire il comando riportato di seguito:

```
ibm-ai-openscale-cli --apikey <la chiave API>
```
{: codeblock}

## Visualizzazione dei risultati in
{{site.data.keyword.aios_short}}
{: #as-open}

Per visualizzare le informazioni sulla correttezza e l'accuratezza del modello, i dettagli dei dati monitorati e l'analisi di una singola transazione, aprire il dashboard [{{site.data.keyword.aios_short}}](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}.

- Per comprendere lo scenario per i dati di esempio, leggere [Caso di utilizzo e valore di {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use).

### Visualizzazione delle informazioni
{: #as-insights}

Dal [dashboard {{site.data.keyword.aios_short}}](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}, fare clic sulla scheda **Insight**, che mostra una panoramica delle metriche per i modelli distribuiti: ![Insight](images/insight-dash-tab.png)

- La pagina Insight mostra in un'unica vista tutti i problemi di correttezza e accuratezza, come determinato dalle soglie configurate.

- Ogni distribuzione viene mostrata come un riquadro. Se si segue uno qualsiasi dei supporti didattici, nel dashboard, si vede una distribuzione denominata `GermanCreditRiskModel`. Il seguente esempio mostra un dashboard con molti modelli distribuiti e monitorati:

    ![il dashboard Insight con molte distribuzioni, ognuna mostrata come un riquadro](images/insight-dashboard.png)


### Visualizzazione dei dati di monitoraggio
{: #as-monitoring}

1. Dalla pagina Insight, fare clic sul riquadro `GermanCreditRiskModel` per visualizzare i dettagli relativi ai dati monitorati.
2. Scorrere il puntatore nel grafico per visualizzare un periodo di giorni e ore che mostrano dati e fare clic sul link **Visualizza dettagli**.

   - Ad esempio, la figura che segue mostra i dati per una data e ora specifica. Le date e le ore variano, a seconda di quando si esegue il modulo.

   - Per informazioni sull'interpretazione del grafico delle serie temporali, consultare [Acquisizione degli insight](/docs/services/ai-openscale?topic=ai-openscale-it-ov).

    ![vengono visualizzati i dati del monitor ](images/setup02-0206.png)

3. Per visualizzare i dettagli relativi al monitoraggio dei dati `Età`, assicurarsi che `Età` sia selezionato dal menu a discesa.

  - Notare che nella seguente immagine, non esiste alcuna distorsione.

  - Per informazioni sull'interpretazione del grafico dei punti di dati a un'ora specifica, consultare [Visualizzazione dei dati per un'ora specifica](/docs/services/ai-openscale?topic=ai-openscale-it-vdet).

    ![sono visualizzati i dettagli della vista](images/setup03-0206.png)

### Visualizzazione spiegazione
{: #as-explain}

Per comprendere i fattori che contribuiscono quando una distorsione è presente per un dato periodo di tempo, dal pannello di visualizzazione nella sezione precedente, selezionare il pulsante **Visualizza transazioni**.

Vengono elencati gli ID transazione per l'ultima ora per le transazioni che hanno distorsione. Per il modello utilizzato in questo modulo, non esistono distorsioni per le richieste disponibili. Pertanto, non viene visualizzata alcuna transazione per il periodo di tempo nell'immagine che segue.

  ![Elenco transazioni senza transazioni](images/setup06-0206.png)

Per informazioni relative alla ricerca e alla spiegazione delle transazioni, consultare [Spiegazione delle transazioni](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view).

## Informazioni correlate
{: #as-info}

- Per informazioni sulle distorsioni, consultare [Correttezza](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
- Per informazioni sulla bontà dei risultati previsionali del modello, consultare [Accuratezza](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Per informazioni sull'interpretazione dei grafici e dei dati, consultare [Acquisizione degli insight](/docs/services/ai-openscale?topic=ai-openscale-it-ov).
- Per informazioni su come i fattori sottostanti influenzino i risultati, consultare [Monitoraggio esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
