---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: release notes, what's new 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Novità
{: #rn-relnotes}

Questo documento descrive le nuove funzioni e i problemi noti per {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 5 marzo 2019
{: #rn-5March2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

### Nuove funzioni e modifiche
{: #rn-5March2019nf}

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  precedente release includono:

- __*Nuovo modello di rischio di credito*__: è supportato un esempio/supporto didattico per un nuovo modello di rischio di credito per tutti i motori di calcolo del punteggio. Per ulteriori informazioni, consultare gli argomenti [Introduzione](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) e [Risorse aggiuntive](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Elaborazione dell'annullamento della distorsione*__: è possibile alternare tra il modello di produzione e un modello con distorsione annullata creato da {{site.data.keyword.aios_short}}. Consultare [Modello di produzione e modello con distorsione annullata](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) e [Come funziona l'annullamento della distorsione](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) per ulteriori informazioni.

## 22 febbraio 2019
{: #rn-22February2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

### Nuove funzioni e modifiche
{: #rn-22February2019nf}

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  precedente release includono:

- __*Aggiornamenti IU*__: è possibile importare un file JSON per configurare programmaticamente tutti i monitor e le funzioni durante la creazione della sottoscrizione. È anche possibile esportare il file di configurazione. Consultare l'argomento [Configurazione della sottoscrizione di distribuzione utilizzando i file JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) per ulteriori informazioni.

## 7 febbraio 2019
{: #rn-7February2019}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

### Nuove funzioni e modifiche
{: #rn-7February2019nf}

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  precedente release includono:

- __*Aggiornamenti IU*__: sono stati apportati diversi miglioramenti all'interfaccia utente di {{site.data.keyword.aios_short}}, tra cui un modo per [verificare la correttezza e l'accuratezza su richiesta](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep) e la possibilità di visualizzare un elenco di transazioni dal [grafico dei dettagli della correttezza](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Miglioramenti dell'esplicabilità*__: tutti i numeri ora hanno la stessa precisione/scala tra i valori Pertinenti Positivi (PP) e Pertinenti Negativi (PN). 

- __*Supporto SSL Db2*__: {{site.data.keyword.aios_short}} supporta i certificati autofirmati (codificati in Base-64) con le credenziali DB2.

- __*Supporto di IBM Cloud Database*__: {{site.data.keyword.aios_short}} ora supporta i database per PostgreSQL, oltre a Compose per PostgreSQL e Db2)

### Problemi noti
{: #rn-7February2019ki}

- **Istanza del servizio ML personalizzata**

    - Il [modulo Python](/docs/services/ai-openscale?topic=ai-openscale-as-module) attualmente non dispone di una Esplicabilità funzionante per l'istanza del servizio personalizzata. Questo perché l'istanza del servizio personalizzata richiede una previsione numerica nei dati di risposta, che non è inclusa con lo script del modulo.

## 14 dicembre 2018
{: #rn-14December2018}

Sono disponibili le seguenti nuove funzioni, modifiche e problemi noti per il servizio.

### Nuove funzioni e modifiche
{: #rn-12nf}

Le funzioni {{site.data.keyword.aios_short}} che sono state aggiunte o migliorate dalla  release beta includono:

- __*Disponibilità generale*__: la release GA (General Availability) di {{site.data.keyword.aios_full_notm}} come piano IBM Cloud Standard (a pagamento).

- __*IBM Cloud Private for Data V1.2*__: se si utilizza {{site.data.keyword.aios_short}} su IBM Cloud Private for Data V1.2, consultare la documentazione, incluse le istruzioni di installazione, qui: [Checklist di installazione](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Supporto per il proprio tipo di modello*__: oltre alle distribuzioni di modelli AI in Watson Machine Learning, {{site.data.keyword.aios_short}} supporta le distribuzioni di modelli in Microsoft Azure, Amazon SageMaker e ambienti personalizzati. Consultare [Tipi di modello supportati](/docs/services/ai-openscale?topic=ai-openscale-in-ov) per ulteriori informazioni. 

- __*Database "lite" gratuito*__: un database gestito "lite" gratuito fornisce tutto quello che occorre per iniziare ad utilizzare {{site.data.keyword.aios_short}}. Consultare i [{{site.data.keyword.aios_short}}piani dei prezzi![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/watson-openscale){: new_window} per i dettagli. 

- __*Monitoraggio della distorsione*__: supporto per gli attributi protetti di tipo `mobile` e `doppio`, e di rilevamento della distorsione sui modelli di regressione lineare. E {{site.data.keyword.aios_short}} può automaticamente annullare la distorsione del modello AI. Consultare [Informazioni sulla correttezza](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) per ulteriori informazioni. 

- __*Esplicabilità*__: supporto per i modelli di regressione, le funzioni Python e spiegazioni contrastanti complementari. Consultare [Monitoraggio dell'esplicabilità](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) per ulteriori informazioni. 

- __*Datastore*__: monitoraggio della qualità senza dipendere da Watson Machine Learning, e la possibilità di utilizzare il proprio database, sia che sia Db2, Postgres o Db2 on Cloud.

- __*NeuNetS (Beta)*__: IBM Neural Network Synthesizer (NeuNetS) è disponibile come release beta (solo cloud pubblico). Consultare la [documentazione NeuNetS![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window} per ulteriori informazioni. 

- __*IU potenziata*__: l'interfaccia utente di {{site.data.keyword.aios_short}} è stata migliorata per includere una distribuzione istogramma di runtime con alternanza per dati di training, ID & versione modello e una tabella di ID transazione dall'istogramma. Consultare [Visualizzazione dei dati per un'ora specifica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) per ulteriori informazioni.

- __*Opzione alternativa di configurazione del supporto didattico*__: per automatizzare il provisioning e la configurazione dei servizi IBM Cloud richiesti e per vedere un'applicazione IBM {{site.data.keyword.aios_full}}, incluso dati di campionamento, è possibile installare ed eseguire un modulo Python. Consultare [Installazione di un modulo Python per configurare {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

### Problemi noti
{: #rn-12ki}

- **Microsoft Azure**

    - Dei due tipi di servizi Web di Azure Machine Learning, solo il tipo `Nuovo` è supportato da {{site.data.keyword.aios_short}}. Il tipo `Classico` non è supportato.

    - __*Deve essere utilizzato il nome di input predefinito*__: nel servizio Web Azure, il nome di input predefinito è `"input1"`. Attualmente questo campo è obbligatorio per {{site.data.keyword.aios_short}} e, se manca, {{site.data.keyword.aios_short}} non funzionerà.

      Se il servizio Web Azure non utilizza il nome predefinito, modificare il nome del campo di immissione in `"input1"`, così il codice funzionerà.

- **AWS SageMaker**

    - __*Algoritmo BlazingText non supportato*__: il formato di payload di input dell'algoritmo AWS SageMaker BlazingText non è supportato nella release corrente di {{site.data.keyword.aios_short}}.

## 17 settembre 2018
{: #rn-17September2018}

### Nuove funzioni e modifiche
{: #rn-17nf}

- **Anteprima release Beta** - Benvenuti nell'anteprima della release beta di {{site.data.keyword.aios_full_notm}}.
