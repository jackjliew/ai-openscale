---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Informazioni su
{: #in-ov}

{{site.data.keyword.aios_full}} è un ambiente di livello aziendale per applicazioni che utilizzano l'AI, che fornisce alle aziende visibilità su come si crea e si utilizza l'AI e il ROI che ne deriva, relativamente alla propria attività di business.
{: shortdesc}

<p>&nbsp;</p>

## Implementazione
{: #in-imp}

Ecco come implementare {{site.data.keyword.aios_short}}:

- **Configurare {{site.data.keyword.aios_short}}**: con l'ambiente grafico di facile utilizzo, [configurare un database di registrazione del payload](/docs/services/ai-openscale?topic=ai-openscale-connect-db) e [l'istanza di Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-wml-connect) in cui sono memorizzati i modelli e le distribuzioni AI.

- **Gestire i monitor**: per ogni distribuzione, configurare il modo in cui {{site.data.keyword.aios_short}} monitorerà la distribuzione. È possibile eseguire il monitoraggio di:

    - [Correttezza](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [Accuratezza](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)
    - [Prestazioni](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics#anlz_metrics_performance)

- **Visualizzare e modificare i dati monitorati**: il dashboard {{site.data.keyword.aios_short}}[](/docs/services/ai-openscale?topic=ai-openscale-io-ov) consente di visualizzare facilmente le informazioni chiave e di identificare i problemi per le distribuzioni. La visualizzazione dei singoli punti di dati per ogni funzione monitorata fornisce ulteriori dettagli.

<p>&nbsp;</p>

## Limitazioni
{: #in-lim}

- La release corrente supporta solo un database, un'istanza di {{site.data.keyword.pm_full}} e un'istanza di {{site.data.keyword.aios_short}}

- Il database e l'istanza {{site.data.keyword.pm_full}} devono essere distribuiti nello stesso account {{site.data.keyword.cloud_notm}}.

- Il piano Lite (gratuito) ha i seguenti limiti mensili:

    - Due modelli distribuiti monitorati
    - 20 transazioni spiegate
    - 50.000 record di payload (cumulativi)
    - 50.000 record di feedback (cumulativi)

- {{site.data.keyword.aios_short}} utilizza un database PostgreSQL o Db2 per memorizzare i dati relativi al modello (dati di feedback, payload di calcolo del punteggio) e le metriche calcolate. I piani DB2 Lite non sono attualmente supportati.

- Esiste un limite di licenza di 20 modelli distribuiti per istanza di {{site.data.keyword.aios_short}}.

- Per {{site.data.keyword.pm_full}}, il payload delle immagini perturbate inviate tramite il gateway di machine learning non può superare 1 MB. Per evitare problemi di timeout, le immagini non devono superare 125 x 125 pixel e devono essere inviate in sequenza in modo che la spiegazione per la seconda immagine sia richiesta quando la prima è completata.


<p>&nbsp;</p>

## Problemi noti
{: #rn-12ki}

- **Microsoft Azure**

    - Dei due tipi di servizi Web di Azure Machine Learning, solo il tipo `Nuovo` è supportato da {{site.data.keyword.aios_short}}. Il tipo `Classico` non è supportato.

    - __*Deve essere utilizzato il nome di input predefinito*__: nel servizio Web Azure, il nome di input predefinito è `"input1"`. Attualmente questo campo è obbligatorio per {{site.data.keyword.aios_short}} e, se manca, {{site.data.keyword.aios_short}} non funzionerà.

      Se il servizio Web Azure non utilizza il nome predefinito, modificare il nome del campo di immissione in `"input1"`, così il codice funzionerà.

- **AWS SageMaker**

    - __*Algoritmo BlazingText non supportato*__: il formato di payload di input dell'algoritmo AWS SageMaker BlazingText non è supportato nella release corrente di {{site.data.keyword.aios_short}}.

- **Istanza del servizio ML personalizzata**

    - Il [modulo Python](/docs/services/ai-openscale?topic=ai-openscale-as-module) attualmente non dispone di una Esplicabilità funzionante per l'istanza del servizio personalizzata. Questo perché l'istanza del servizio personalizzata richiede una previsione numerica nei dati di risposta, che non è inclusa con lo script del modulo.

<p>&nbsp;</p>

## Motori e framework di machine learning supportati
{: #in-fram}

Il servizio {{site.data.keyword.aios_short}} supporta i seguenti motori di machine learning. Ogni runtime supporta modelli creati nei seguenti framework:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Personalizzato](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS (solo ICP)](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

Il supporto completo include le seguenti funzioni per il framework, il problema e il tipo di dati specifico:

- Registrazione payload	
- Registrazione feedback	
- Accuratezza prestazioni	
- Rilevamento distorsione runtime	
- Esplicabilità	
- Annullamento automatico distorsione

<p>&nbsp;</p>

## Supporto dei browser
{: #in-brw}

Gli strumenti del servizio {{site.data.keyword.aios_short}} richiedono lo stesso livello di software browser richiesto da {{site.data.keyword.cloud_notm}}. Per i dettagli, consultare l'argomento Prerequisiti {{site.data.keyword.cloud_notm}} [](/docs/overview?topic=overview-prereqs-platform#browsers-platform).

<p>&nbsp;</p>

## Strumento CLI ModelOps
{: #in-mop}

Lo strumento CLI [{{site.data.keyword.aios_short}} per le operazioni sul modello ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} consente di eseguire attività correlate alla gestione del ciclo di vita dei modelli di machine learning. Questo strumento è complementare allo strumento CLI {{site.data.keyword.cloud_notm}}, con l'aggiunta del [plugin di machine learning ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}.

<p>&nbsp;</p>

## Client Python
{: #in-pyc}

Il client [{{site.data.keyword.aios_short}} Python ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://ai-openscale-python-client.mybluemix.net/){: new_window} è una libreria Python che consente di lavorare direttamente con il servizio {{site.data.keyword.aios_short}} su {{site.data.keyword.cloud_notm}}. È possibile utilizzare il client Python, invece della IU del client  {{site.data.keyword.aios_short}}, per configurare direttamente un database di registrazione, collegare il motore di machine learning e selezionare e monitorare le distribuzioni. Per esempi di utilizzo del client Python a questo scopo, consultare i notebook di esempio [{{site.data.keyword.aios_short}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Passi successivi
{: #in-next}

- [Introduzione](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) al servizio.
- Consultare il [materiale di riferimento per le API![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/ai-openscale){: new_window}.

Altre domande? 

- [Novità](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contattare IBM ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
