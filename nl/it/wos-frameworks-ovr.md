---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# Motori, framework e modelli di machine learning supportati
{: #in-fram}

Il servizio {{site.data.keyword.aios_short}} supporta i seguenti motori di machine learning. Ogni runtime supporta modelli creati nei seguenti framework:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azureservice#frmwrks-azureservice)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Personalizzato](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) (disponibile solo in {{site.data.keyword.wos4d_full}})


Il supporto completo include le seguenti funzioni per il framework, il problema e il tipo di dati specifico:

- Registrazione payload	
- Registrazione feedback	
- Accuratezza prestazioni	
- Rilevamento distorsione runtime	
- Esplicabilità	
- Annullamento automatico distorsione

<p>&nbsp;</p>


## Tipi di modello supportati
{: #abt-models}

Tabella 1. Dettagli supporto modello

| Algoritmi | **Correttezza** | **Annullamento automatico distorsione** | **Spiega** | **Accuratezza** |
|:---|:---:|:---:|:---:|:---:|
| **Classificazione strutturata** | Sì | Sì<sup>1</sup> | Sì<sup>1</sup> | Sì |
| **Regressione strutturata**     | Sì | Prossimamente | Sì | Sì |
| **Classificazione testo**       | No - argomento ricerca attiva | No - argomento ricerca attiva | Sì<sup>1</sup> | No |
| **Classificazione immagine**      | No - argomento ricerca attiva | No - argomento ricerca attiva | Sì<sup>1</sup> | No ||
{: caption="Dettagli supporto modello" caption-side="top"}

<sup>1</sup> L'esplicabilità è supportata se il modello/framework emette probabilità previsionali.

<p>&nbsp;</p>

## Supporto dei browser
{: #in-brw}

Gli strumenti del servizio {{site.data.keyword.aios_short}} richiedono lo stesso livello di software browser richiesto da {{site.data.keyword.cloud_notm}}. Per i dettagli, consultare l'argomento Prerequisiti {{site.data.keyword.cloud_notm}} [](/docs/overview?topic=overview-prereqs-platform#browsers-platform).

<p>&nbsp;</p>

## Strumento CLI ModelOps
{: #in-mop}

Lo strumento CLI [{{site.data.keyword.aios_short}} per le operazioni sul modello](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external} consente di eseguire attività correlate alla gestione del ciclo di vita dei modelli di machine learning. Questo strumento è complementare allo strumento CLI {{site.data.keyword.cloud_notm}}, con l'aggiunta del [plugin di machine learning](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}.

<p>&nbsp;</p>

## Client Python
{: #in-pyc}

Il [{{site.data.keyword.aios_short}} client Python](http://ai-openscale-python-client.mybluemix.net/){: external} è una libreria Python che consente di lavorare direttamente con il servizio {{site.data.keyword.aios_short}} su {{site.data.keyword.cloud_notm}}. È possibile utilizzare il client Python, invece della IU del client  {{site.data.keyword.aios_short}}, per configurare direttamente un database di registrazione, collegare il motore di machine learning e selezionare e monitorare le distribuzioni. Per esempi di utilizzo del client Python a questo scopo, consultare i [notebook di esempio {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Passi successivi
{: #in-next}

- Visualizzare il [materiale Riferimento API](https://{DomainName}/apidocs/ai-openscale){: external}.

Altre domande? 

- [Novità](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contatta IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
