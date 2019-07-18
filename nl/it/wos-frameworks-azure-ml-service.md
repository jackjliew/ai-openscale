---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Framework per Microsoft Azure ML Service
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} supporta completamente i seguenti framework Microsoft Azure Machine Learning Service:
{: shortdesc}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| Nativo | Classificazione | Strutturato |
| scikit-learn | Classificazione | Strutturato |
| scikit-learn | Regressione | Strutturato |
{: caption="Dettagli supporto framework" caption-side="top"}

## Aggiunta di Microsoft Azure ML Service a {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

È possibile configurare {{site.data.keyword.aios_short}} per lavorare con Microsoft Azure ML Service utilizzando uno dei seguenti metodi:

- Se è la prima volta che si aggiunge un provider di machine learning a {{site.data.keyword.aios_short}}, è possibile utilizzare l'interfaccia di configurazione. Per ulteriori informazioni, consultare [Specifica di un'istanza Microsoft Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice).
- È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. È necessario utilizzare questo metodo se si desidera avere più di un provider. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).


{{site.data.keyword.aios_short}} richiama vari endpoint REST che sono necessari per interagire con Azure ML Service. A tale scopo, è necessario collegare Azure Machine Learning Service {{site.data.keyword.aios_short}}.

1. Creare un principal di Azure Active Directory Service. 
2. Specificare i dettagli delle credenziali quando si aggiunge il bind del servizio Azure ML Service, attraverso l'interfaccia utente o l'SDK {{site.data.keyword.aios_short}} Python.

## Requisiti per i file di richiesta e di risposta JSON
{: #frmwrks-azureservice-JSON}

Affinché {{site.data.keyword.aios_short}} lavori con Azure ML Service, le distribuzioni del servizio web create devono soddisfare determinati requisiti. Le distribuzioni del servizio web create devono accettare richieste JSON e restituire risposte JSON, in base ai requisiti descritti di seguito.

### Formato richiesto per la richiesta JSON del servizio web
{: #frmwrks-azureservice-JSON-sample-request}

- Il corpo della richiesta API REST deve essere un documento JSON che contiene un array JSON di oggetti JSON
- L'array JSON deve essere denominato `"input"`.
- Ogni oggetto JSON può includere solo coppie chiave-valore semplici, dove i valori possono essere solo una stringa, un numero, `true`, `false` o `null`
- I valori non possono essere un oggetto o un array JSON
- Ogni oggetto JSON nell'array deve avere le stesse chiavi (e quindi numero di chiavi) specificate, a prescindere dal fatto che ci sia o meno un valore non-`null` disponibile. 


Il seguente file JSON di esempio soddisfa i requisiti precedenti e può essere utilizzato come modello per la creazione dei propri file di richiesta JSON:


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### Formato richiesto per la risposta JSON del servizio web
{: #frmwrks-azureservice-JSON-sample-response}

Prendere nota dei seguenti elementi quando si crea un file di risposta JSON:

- Il corpo della risposta API REST deve essere un documento JSON che contiene un array JSON di oggetti JSON
- L'array JSON deve essere denominato `"output"`.
- Ogni oggetto JSON può includere solo coppie chiave-valore, dove i valori possono essere solo una stringa, un numero, `true`, `false`, `null` o un array che non contiene altri oggetti JSON o array
- I valori non possono essere un oggetto JSON
- Ogni oggetto JSON nell'array deve avere le stesse chiavi (e numero di chiavi) specificate, a prescindere dal fatto che ci sia o meno un valore non-`null` disponibile. 
- Per i modelli di classificazione: il servizio web deve restituire un array di probabilità per ogni classe e l'ordine delle probabilità deve essere congruente per ogni oggetto JSON nell'array
  - Esempio: supporre che si abbia un modello di classificazione binario che prevede il rischio di credito, dove le classi sono `Risk` o `No RisK`
  - Per ogni risultato restituito nell'array "output", l'oggetto deve contenere una coppia chiave-valore che include le probabilità in ordine fisso, nel formato:
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

Per essere congruenti con gli strumenti visivi di Azure ML utilizzati in Azure ML Studio e Service, si consiglia, anche se non è obbligatorio, di utilizzare i seguenti nomi chiave:

- il nome chiave `"Scored Labels"` per la chiave di output che denota il valore previsto del modello
- il nome chiave `"Scored Probabilities"` per la chiave di output che denota un array di probabilità per ogni classe

Il seguente file JSON di esempio soddisfa i requisiti precedenti e può essere utilizzato come modello per la creazione dei propri file di risposta JSON:


```JSON
{
  "output": [
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## Notebook di esempio
{: #frmwrks-azureservice-smpl-ntbks}

I seguenti notebook mostrano come operare con Microsoft Azure ML Service:

- [Creazione data mart, monitoraggio distribuzione modello e analisi dati](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Esempi di calcolo del punteggio del modello MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Scopri di più
{: #frmwrks-azureservice-mediumblogs}

- [In che modo il servizio Azure Machine Learning differisce da Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
