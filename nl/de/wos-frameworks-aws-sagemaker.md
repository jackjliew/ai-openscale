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

# Amazon SageMaker-Frameworks
{: #frmwrks-aws-sage}

Mit Amazon SageMaker können Sie Nutzdatenprotokollierung, Rückmeldungsprotokollierung sowie Messungen der Leistungsgenauigkeit, Verzerrungserkennung zur Laufzeit, der Erklärbarkeit und der Funktion für automatische Verzerrungsbereinigung in {{site.data.keyword.aios_full}} ausführen.

{{site.data.keyword.aios_full}} unterstützt die folgenden Amazon SageMaker-Frameworks vollständig:
{: shortdesc}

Tabelle 1. Details der Frameworkunterstützung

| Framework | Problemtyp | Datentyp |
|:---|:---:|:---:|
| Nativ | Klassifizierung | Strukturiert |
| Nativ | Regression<sup>1</sup> | Strukturiert |
{: caption="Details der Frameworkunterstützung" caption-side="top"}

<sup>1</sup>Die Unterstützung für Regressionsmodelle umfasst nicht das Ausmaß der Drift.

## Amazon SageMaker zu {{site.data.keyword.aios_short}} hinzufügen
{: #frmwrks-aws-sage-add}

Sie können {{site.data.keyword.aios_short}} auf eine der folgenden Weisen für die Verwendung von Amazon SageMaker konfigurieren:

- Wenn Sie zum ersten Mal einen Machine Learning-Provider zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen hierzu finden Sie im Abschnitt [Amazon SageMaker-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- Sie können Ihren Machine-Learning-Anbieter auch mit dem Python-SDK hinzufügen. Diese Methode müssen Sie verwenden, wenn mehrere Anbieter zur Verfügung stehen sollen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Amazon SageMaker-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Beispielnotebooks
{: #frmwrks-aws-sage-smpl-ntbks}

Die folgenden Notebooks enthalten Informationen zur Verwendung von Amazon SageMaker:

- [Erstellen und Bereitstellen von Vorhersagemodellen für Kreditrisiken](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Datamart-Erstellung, Überwachung der Modellbereitstellung und Datenanalyse](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## Amazon SageMaker ML-Serviceinstanz angeben
{: #csm-connect}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Amazon SageMaker-Serviceinstanz an. In Ihrer Amazon SageMaker-Serviceinstanz speichern Sie Ihre AI-Modelle und -Bereitstellungen.
{: shortdesc}

Sie können Ihren Machine-Learning-Anbieter auch mit dem Python-SDK hinzufügen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Amazon SageMaker-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

### Verbindung zur Amazon SageMaker-Serviceinstanz herstellen
{: #csm-config}

{{site.data.keyword.aios_short}} stellt die Verbindung zu AI-Modellen und Bereitstellungen in einer Amazon SageMaker-Serviceinstanz her.

1.  Klicken Sie auf der Registerkarte **Konfigurieren** im Navigationsfenster auf **Machine Learning-Provider**.

    ![Darstellung der Anzeige für die Auswahl des Machine Learning-Providers, mit Kacheln für die unterstützten Machine Learning-Engines.](images/wos-machine-learning-providers-selection.png)

1.  Klicken Sie auf die Schaltfläche **Machine Learning-Provider hinzufügen** und dann auf die Kachel **Amazon SageMaker**.

    ![Berechtigungsnachweise für Amazon SageMaker-Service eingeben](images/connect-sage-cred.png)

1.  Geben Sie Ihre Berechtigungsnachweise ein und speichern Sie sie:

    - Zugriffsschlüssel-ID: Ihre AWS-Zugriffsschlüssel-ID, `aws_access_key_id`, die Sie identifiziert und Ihre AWS-Aufrufe authentifiziert und autorisiert.
    - Geheimer Zugriffsschlüssel: Ihr geheimer AWS-Zugriffsschlüssel, `aws_secret_access_key`, der erforderlich ist, um Ihre Identität zu verifizieren und Ihre AWS-Aufrufe zu authentifizieren und zu autorisieren.
    - Region: Geben Sie die Region ein, in der Ihre Zugriffsschlüssel-ID erstellt wurde. Schlüssel werden in der Region gespeichert und verwendet, in der sie erstellt wurden, und können nicht an eine andere Region übertragen werden.

1.  In {{site.data.keyword.aios_short}} sind die bereitgestellten Modelle aufgelistet. Wählen Sie die Modelle aus, die Sie überwachen möchten.

## Nutzdatenprotokollierung mit der Amazon SageMaker Machine Learning-Engine
{: #cml-smconfig}

### Bindung für Amazon SageMaker Machine Learning-Engine erstellen
{: #cml-smbind}

- Eine Nicht-{{site.data.keyword.pm_full}}-Engine wird als 'Angepasst' gebunden, was bedeutet, dass nur die Metadaten gebunden werden und somit keine direkte Integration mit dem Nicht-{{site.data.keyword.pm_full}}-Service besteht.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Sie können Ihre Servicebindung mit dem folgenden Befehl anzeigen:

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker Machine Learning-Bindung](images/ml-sagemaker-bind.png)

### Amazon SageMaker Machine Learning-Abonnement hinzufügen
{: #cml-smsub}

- Abonnement hinzufügen

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Abonnementliste abrufen

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Nutzdatenprotokollierung aktivieren
{: #cml-smenlog}

- Nutzdatenprotokollierung im Abonnement aktivieren

    ```python
    subscription.payload_logging.enable()
    ```

- Protokollierungsdetails abrufen

    ```python
    subscription.payload_logging.get_details()
    ```

### Scoring und Nutzdatenprotokollierung
{: #cml-smscore}

- Führen Sie ein Scoring für Ihr Modell durch. Ein vollständiges Beispiel finden Sie in [Notebook 'Mit der SageMaker Machine Learning-Engine arbeiten'](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}.


- Anforderung und Antwort in der Nutzdatenprotokollierungstabelle speichern:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Hinweis**: Für andere Sprachen als Python können Sie die Nutzdatenprotokollierung auch direkt über eine REST-API durchführen.

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

## Weitere Schritte
{: #csm-next}

- Nun können Sie in {{site.data.keyword.aios_short}} die [Überwachungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [Sagemaker-Machine Learning mit Watson OpenScale überwachen](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
