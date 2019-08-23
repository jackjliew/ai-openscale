---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# Invio di una richiesta di calcolo del punteggio
{: #cdb-score}

Per configurare i monitor, {{site.data.keyword.aios_short}} richiede l'invio di un payload di calcolo del punteggio, per poter iniziare a registrare i dati che verranno monitorati.

- I modelli distribuiti in {{site.data.keyword.pm_full}}, vengono automaticamente inviati a {{site.data.keyword.aios_short}}. Per le richieste di calcolo del punteggio che vengono inviate automaticamente, non è necessario completare questa attività e non vengono visualizzati frammenti di codice.
- Per altri motori di machine learning, come Microsoft Azure, Amazon SageMaker, o un motore di machine learning personalizzato, il payload di calcolo del punteggio deve essere inviato utilizzando l'API Registrazione payload. Per questo, è necessario utilizzare un frammento di codice in formato cURL o Python, che è possibile richiamare dalla pagina di registrazione del payload. Per ulteriori informazioni, consultare [Registrazione payload per istanze di servizio non {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

## Procedura per la registrazione del payload
{: #cdb-score-apisteps}

1. Dal dashboard {{site.data.keyword.aios_short}}, fare clic su un riquadro di distribuzione.
2. Fare clic su **Configura monitor**. 
3. Nel riquadro di navigazione, fare clic su **Registrazione payload**.
2. Scegliere se utilizzare il codice `cURL` o `Python` facendo clic sulla scheda `cURL` o `Python`.
3. Fare clic su **Copia negli appunti** e incollare per registrare i dati della richiesta di distribuzione modello e della risposta. Per ulteriori informazioni, consultare [Registrazione payload per istanze di servizio non {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

I campi e i valori nei frammenti di codice devono essere sostituiti con i propri valori reali, in quanto quelli forniti sono solo esempi.
{: important}

![Selezionare il database](images/config-send-scoring.png)

Dopo aver eseguito la registrazione del payload, viene visualizzato un segno di spunta nella colonna **Pronto a monitorare** per la distribuzione selezionata. Fare clic su **Configura monitor** per continuare.

## Conoscere il numero di richieste di calcolo del punteggio
{: #cdb-score-capacity}

Le richieste di calcolo del punteggio sono parte integrante dell'elaborazione di {{site.data.keyword.aios_short}}. Ogni record di transazione che si invia al modello per il calcolo del punteggio genera un'ulteriore elaborazione in modo che il servizio {{site.data.keyword.aios_short}} possa eseguire la perturbazione e creare le spiegazioni.

- Per i modelli tabella, testo e immagine la seguente richiesta di base genera i punti di dati:

   -ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service richiesta di calcolo del punteggio genera 5000 punti di dati.

- Solo per i modelli di classificazione tabella, ci sono ulteriori richieste di calcolo del punteggio che vengono fatte per una spiegazione contrastante. Le seguenti richieste sono aggiunte alla richiesta di base precedente:

   - 100 richieste di calcolo del punteggio generano 51 punti di dati aggiuntivi per richiesta.
   - 101 richieste di calcolo del punteggio generano sai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service punti di dati aggiuntivi per richiesta.


## Passi successivi
{: #cdb-score-next-steps-scoringreq}

[Configurare i monitor](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config).
