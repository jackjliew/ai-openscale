---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

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

# Framework Microsoft Azure ML Studio
{: #frmwrks-azure}

È possibile utilizzare Microsoft Azure ML Studio per eseguire la registrazione del payload, del feedback e per misurare l'accuratezza delle prestazioni, il rilevamento della distorsione al run-time, l'esplicabilità e la funzione di annullamento della distorsione automatico in {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} supporta completamente i seguenti framework Microsoft Azure Machine Learning Studio:
{: shortdesc}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| Nativo | Classificazione | Strutturato |
| Nativo | Regressione | Strutturato |
{: caption="Dettagli supporto framework" caption-side="top"}

## Aggiunta di Microsoft Azure ML Studio a {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

È possibile configurare {{site.data.keyword.aios_short}} per lavorare con Microsoft Azure ML Studio utilizzando uno dei seguenti metodi:

- Se è la prima volta che si aggiunge un provider di machine learning a {{site.data.keyword.aios_short}}, è possibile utilizzare l'interfaccia di configurazione. Per ulteriori informazioni, consultare [Specifica di un'istanza Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. È necessario utilizzare questo metodo se si desidera avere più di un provider. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


## Notebook di esempio
{: #frmwrks-azure-smpl-ntbks}

I seguenti notebook mostrano come operare con Microsoft Azure ML Studio:

- [Creazione data mart, monitoraggio distribuzione modello e analisi dati](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Esempi di calcolo del punteggio del modello MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Scopri di più
{: #frmwrks-azure-mediumblogs}

-[Monitorare il machine learning Azure con Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [In che modo il servizio Azure Machine Learning differisce da Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Utilizzo di un modello di machine learning Azure distribuito come servizio web](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## Specifica di un'istanza di Microsoft Azure ML Studio
{: #connect-azure}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza di Microsoft Azure ML Studio. L'istanza di Azure ML Studio è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

### Connessione dell'istanza di Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza di Azure ML Studio.

1.  Dalla scheda **Configura**, nel riquadro di navigazione, fare clic su **Provider di machine learning**.

    ![viene visualizzato il pannello per la selezione del provider del servizio di machine learning con i riquadri per i motori di machine learning supportati](images/wos-machine-learning-providers-selection.png)

1.  Fare clic sul pulsante **Aggiungi provider di machine learning** e fare clic sul riquadro **Microsoft Azure ML Studio**.

    ![Immettere le credenziali Azure ML Studio](images/connect-azure-cred.png)

1.  Immettere e salvare le credenziali:

    - ID client: il valore stringa effettivo dell'ID client, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno ad Azure Studio.
    - Segreto client: il valore stringa effettivo del segreto, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno ad Azure Studio.
    - Tenant: l'ID tenant corrisponde alla propria organizzazione ed è un'istanza dedicata di Azure AD. Per trovare l'ID tenant, passare il puntatore sul nome account per ottenere l'ID tenant/directory oppure selezionare Azure Active Directory > Proprietà > ID directory nel portale Azure.
    - ID sottoscrizione: le credenziali di sottoscrizione che identificano in modo univoco la propria sottoscrizione Microsoft Azure. L'ID sottoscrizione forma parte dell'URI per ogni chiamata al servizio.

    Consultare [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} per istruzioni su come ottenere le credenziali di Microsoft Azure.
    {: note}

1.  {{site.data.keyword.aios_short}} elenca i modelli distribuiti; selezionare quelli che si desidera monitorare e fare clic su **Configura**.

Sono state selezionate correttamente le distribuzioni.

## Registrazione del payload con il motore Microsoft Azure Machine Learning Studio
{: #cml-azconfig}

### Collegare il motore di machine learning Microsoft Azure
{: #cml-azbind}

- Un motore non {{site.data.keyword.pm_full}} viene collegato come Personalizzato, che indica che contiene solo metadati; non esiste un'integrazione diretta con il servizio non {{site.data.keyword.pm_full}}.

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  È possibile visualizzare il bind del servizio con il seguente comando:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Bind di Azure ML](images/ml-azure-bind.png)

### Aggiungi sottoscrizione a Microsoft Azure ML Studio
{: #cml-azsub}

- Aggiungere la sottoscrizione

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Richiamare l'elenco di sottoscrizioni

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Abilitare la registrazione del payload
{: #cml-azenlog}

- Abilitare la registrazione del payload nella sottoscrizione

    ```python
    subscription.payload_logging.enable()
    ```

- Richiamare i dettagli della registrazione

    ```python
    subscription.payload_logging.get_details()
    ```

### Calcolare il punteggio e registrare il payload
{: #cml-azscore}

- Calcolare il punteggio del modello. Per un esempio completo, consultare il notebook [Working with Azure Machine Learning Studio Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

- Memorizzare la richiesta e la risposta nella tabella di registrazione del payload:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Nota**: per i linguaggi diversi da Python, è possibile anche eseguire direttamente la registrazione del payload, utilizzando un'API REST.

    ```json
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

    ```json
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


## Passi successivi
{: #ca-next}

{{site.data.keyword.aios_short}} ora è pronto per poter [configurare i monitor](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
