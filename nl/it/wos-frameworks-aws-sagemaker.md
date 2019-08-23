---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Framework Amazon SageMaker
{: #frmwrks-aws-sage}

È possibile utilizzare Amazon SageMaker per eseguire la registrazione del payload, del feedback e per misurare l'accuratezza delle prestazioni, il rilevamento della distorsione al run-time, l'esplicabilità e la funzione di annullamento della distorsione automatico in {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} supporta completamente i seguenti framework Amazon SageMaker:
{: shortdesc}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| Nativo | Classificazione | Strutturato |
| Nativo | Regressione<sup>1</sup> | Strutturato |
{: caption="Dettagli supporto framework" caption-side="top"}

<sup>1</sup>Il supporto per i modelli di regressione non include l'evidenziazione della deviazione. 

## Aggiunta di Amazon SageMaker a {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

È possibile configurare {{site.data.keyword.aios_short}} per lavorare con Amazon SageMaker utilizzando uno dei seguenti metodi:

- Se è la prima volta che si aggiunge un provider di machine learning a {{site.data.keyword.aios_short}}, è possibile utilizzare l'interfaccia di configurazione. Per ulteriori informazioni, consultare [Specifica di un'istanza Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. È necessario utilizzare questo metodo se si desidera avere più di un provider. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Notebook di esempio
{: #frmwrks-aws-sage-smpl-ntbks}

I seguenti notebook mostrano come operare con Amazon SageMaker:

- [Creazione e distribuzione del modello di previsione del rischio di credito](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Creazione data mart, monitoraggio distribuzione modello e analisi dati](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## Specifica di un'istanza del servizio Amazon SageMaker ML
{: #csm-connect}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza del servizio Amazon SageMaker. L'istanza del servizio Amazon SageMaker è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

È anche possibile aggiungere il provider di machine learning utilizzando l'SDK Python. Per ulteriori informazioni sull'esecuzione programmatica di questa azione, consultare [Collegare il motore di machine learning Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

### Connessione dell'istanza del servizio Amazon SageMaker
{: #csm-config}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza del servizio Amazon SageMaker.

1.  Dalla scheda **Configura**, nel riquadro di navigazione, fare clic su **Provider di machine learning**.

    ![viene visualizzato il pannello per la selezione del provider del servizio di machine learning con i riquadri per i motori di machine learning supportati](images/wos-machine-learning-providers-selection.png)

1.  Fare clic sul pulsante **Aggiungi provider di machine learning** e fare clic sul riquadro **Amazon SageMaker**.

    ![Immettere le credenziali del servizio Amazon SageMaker](images/connect-sage-cred.png)

1.  Immettere e salvare le credenziali:

    - ID chiave di accesso: l'ID chiave di accesso AWS, `aws_access_key_id`, che verifica chi è l'utente e autentica e autorizza le chiamate che si fanno a AWS.
    - Chiave di accesso segreta: la chiave di accesso segreta AWS, `aws_secret_access_key`, che è richiesta per verificare chi è l'utente e per autenticare e autorizzare le chiamate che si fanno a AWS.
    - Regione: immettere la regione in cui è stato creato l'ID chiave di accesso. Le chiavi sono memorizzate e utilizzate nella regione in cui sono state create e non possono essere trasferite in un'altra regione.

1.  {{site.data.keyword.aios_short}} elenca i modelli distribuiti; selezionare quelli che si desidera monitorare.

## Registrazione del payload con il motore di machine learning Amazon SageMaker
{: #cml-smconfig}

### Collegare il motore di machine learning Amazon SageMaker
{: #cml-smbind}

- Un motore non {{site.data.keyword.pm_full}} viene collegato come Personalizzato, che indica che contiene solo metadati; non esiste un'integrazione diretta con il servizio non {{site.data.keyword.pm_full}}.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  È possibile visualizzare il bind del servizio con il seguente comando:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Bind di SageMaker ML](images/ml-sagemaker-bind.png)

### Aggiungere la sottoscrizione Amazon SageMaker ML
{: #cml-smsub}

- Aggiungere la sottoscrizione

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
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
{: #cml-smenlog}

- Abilitare la registrazione del payload nella sottoscrizione

    ```python
    subscription.payload_logging.enable()
    ```

- Richiamare i dettagli della registrazione

    ```python
    subscription.payload_logging.get_details()
    ```

### Calcolare il punteggio e registrare il payload
{: #cml-smscore}

- Calcolare il punteggio del modello. Per un esempio completo, consultare il notebook [Working with SageMaker Machine Learning Engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}.


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
{: #csm-next}

- {{site.data.keyword.aios_short}} ora è pronto per poter [configurare i monitor](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [Monitorare il machine learning Sagemaker con Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
