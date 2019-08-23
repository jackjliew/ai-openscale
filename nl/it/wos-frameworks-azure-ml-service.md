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

È possibile utilizzare Microsoft Azure ML Service per eseguire la registrazione del payload, del feedback e per misurare l'accuratezza delle prestazioni, il rilevamento della distorsione al run-time, l'esplicabilità e la funzione di annullamento della distorsione automatico in {{site.data.keyword.aios_full}}.

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

- [Esempi di calcolo del punteggio del modello MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## Specifica di un'istanza di Microsoft Azure ML Service
{: #connect-azureservice}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza di Microsoft Azure ML Service. L'istanza di Azure ML Service è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Microsoft Azure Service](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Connessione dell'istanza di Azure ML Service
{: #ca-connect}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza di Azure ML Service.

1.  Dalla scheda **Configura**, nel riquadro di navigazione, fare clic su **Provider di machine learning**.
1.  Fare clic sul pulsante **Aggiungi provider di machine learning** e fare clic sul riquadro **Microsoft Azure ML Service**.
1.  Immettere e salvare le credenziali:

    - ID client: il valore stringa effettivo dell'ID client, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno ad Azure Service.
    - Segreto client: il valore stringa effettivo del segreto, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno ad Azure Service.
    - Tenant: l'ID tenant corrisponde alla propria organizzazione ed è un'istanza dedicata di Azure AD. Per trovare l'ID tenant, passare il puntatore sul nome account per ottenere l'ID tenant/directory oppure selezionare Azure Active Directory > Proprietà > ID directory nel portale Azure.
    - ID sottoscrizione: le credenziali di sottoscrizione che identificano in modo univoco la propria sottoscrizione Microsoft Azure. L'ID sottoscrizione forma parte dell'URI per ogni chiamata al servizio.

    Consultare [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} per istruzioni su come ottenere le credenziali di Microsoft Azure.
    {: note}

1.  {{site.data.keyword.aios_short}} elenca i modelli distribuiti; selezionare quelli che si desidera monitorare e fare clic su **Configura**.

Sono state selezionate correttamente le distribuzioni.

## Registrazione del payload con il motore Microsoft Azure ML Service
{: #cml-azsrvconfig}

### Collegare il motore Microsoft Azure ML Service
{: #cml-azsrvbind}

Un motore non {{site.data.keyword.pm_full}} viene collegato come Personalizzato, che indica che contiene solo metadati; non esiste un'integrazione diretta con il servizio non {{site.data.keyword.pm_full}}.
   
```
AZURE_ENGINE_CREDENTIALS = {
"client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
}

binding_uid = client.data_mart.bindings.add('My Azure ML Service engine', AzureMachineLearningServiceInstance(AZURE_ENGINE_CREDENTIALS))


bindings_details = client.data_mart.bindings.get_details()
```
{: codeblock}

È possibile visualizzare il bind del servizio con il seguente comando:

```
client.data_mart.bindings.list()
```
{: codeblock}

L'output di esempio:

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### Aggiungere la sottoscrizione a Microsoft Azure ML Service
{: #cml-azsrvsub}

Aggiungere la sottoscrizione

```
client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
```
{: codeblock}

Richiamare l'elenco di sottoscrizioni

```
subscriptions = client.data_mart.subscriptions.get_details()

subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
```
{: codeblock}

### Abilitare la registrazione del payload
{: #cml-azsrvenlog}

Abilitare la registrazione del payload nella sottoscrizione

```
subscription.payload_logging.enable()
```
{: codeblock}

Richiamare i dettagli della registrazione

```
subscription.payload_logging.get_details()
```
{: codeblock}

### Calcolare il punteggio e registrare il payload
{: #cml-azsrvscore}

Calcolare il punteggio del modello. Per un esempio completo, consultare il notebook [Working with Azure Machine Learning Service Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

Memorizzare la richiesta e la risposta nella tabella di registrazione del payload:

```
records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

subscription.payload_logging.store(records=records_list)
```
{: codeblock}
{: python}
   
Per i linguaggi diversi da Python, è possibile anche eseguire direttamente la registrazione del payload, utilizzando un'API REST.
   
```
token_endpoint = "https://iam.cloud.ibm.com/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
}

data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
}
   
req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
```
{: codeblock}
{: json}


```
import requests, uuid
   
PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])
   
payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
}]

headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
```
{: codeblock}



## Passi successivi
{: #ca-next}

-{{site.data.keyword.aios_short}} ora è pronto per poter [configurare i monitor](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [In che modo il servizio Azure Machine Learning differisce da Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

