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

# Microsoft Azure ML Studio-Frameworks
{: #frmwrks-azure}

Mit Microsoft Azure ML Studio können Sie Nutzdatenprotokollierung, Rückmeldungsprotokollierung sowie Messungen der Leistungsgenauigkeit, Verzerrungserkennung zur Laufzeit, der Erklärbarkeit und der Funktion für automatische Verzerrungsbereinigung in {{site.data.keyword.aios_full}} ausführen.

{{site.data.keyword.aios_full}} unterstützt die folgenden Microsoft Azure Machine Learning Studio-Frameworks vollständig:
{: shortdesc}

Tabelle 1. Details der Frameworkunterstützung

| Framework | Problemtyp | Datentyp |
|:---|:---:|:---:|
| Nativ | Klassifizierung | Strukturiert |
| Nativ | Regression | Strukturiert |
{: caption="Details der Frameworkunterstützung" caption-side="top"}

## Microsoft Azure ML Studio zu {{site.data.keyword.aios_short}} hinzufügen
{: #frmwrks-azure-add}

Sie können {{site.data.keyword.aios_short}} auf eine der folgenden Weisen für die Verwendung von Microsoft Azure ML Studio konfigurieren:

- Wenn Sie zum ersten Mal einen Machine Learning-Provider zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen finden Sie im Abschnitt [Microsoft Azure ML Studio-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Diese Methode müssen Sie verwenden, wenn mehrere Anbieter zur Verfügung stehen sollen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Microsoft Azure-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


## Beispielnotebooks
{: #frmwrks-azure-smpl-ntbks}

Die folgenden Notebooks enthalten Informationen zur Verwendung von Microsoft Azure ML Studio:

- [Datamart-Erstellung, Überwachung der Modellbereitstellung und Datenanalyse](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Scoring-Beispiele für MS Azure Service-Modelle](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Weiterführende Informationen
{: #frmwrks-azure-mediumblogs}

- [Azure Machine Learning mit Watson OpenScale überwachen](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [Wie unterscheidet sich Azure Machine Learning Service von Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Als Web-Service bereitgestelltes Azure Machine Learning-Modell verarbeiten](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## Microsoft Azure ML Studio-Instanz angeben
{: #connect-azure}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Microsoft Azure ML Studio-Instanz an. In der Azure ML Studio-Instanz werden die AI-Modelle und -Bereitstellungen gespeichert.
{: shortdesc}

Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Microsoft Azure-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

### Verbindung zu Azure ML Studio-Instanz herstellen
{: #ca-connect}

{{site.data.keyword.aios_short}} stellt eine Verbindung zu AI-Modellen und -Bereitstellungen in einer Azure ML Studio-Instanz her.

1.  Klicken Sie auf der Registerkarte **Konfigurieren** im Navigationsfenster auf **Machine Learning-Provider**.

    ![Darstellung der Anzeige für die Auswahl des Machine Learning-Providers, mit Kacheln für die unterstützten Machine Learning-Engines.](images/wos-machine-learning-providers-selection.png)

1.  Klicken Sie auf die Schaltfläche **Machine Learning-Provider hinzufügen** und dann auf die Kachel **Microsoft Azure ML Studio**.

    ![Azure ML Studio-Berechtigungsnachweise eingeben](images/connect-azure-cred.png)

1.  Geben Sie Ihre Berechtigungsnachweise ein und speichern Sie sie:

    - Client-ID: Der tatsächliche Zeichenfolgewert Ihrer Client-ID, der Ihre Identität nachweist und Ihre Azure Studio-Aufrufe authentifiziert und autorisiert.
    - Geheimer Clientschlüssel: Der tatsächliche Zeichenfolgewert Ihres geheimen Clientschlüssels, der Ihre Identität nachweist und Ihre Azure Studio-Aufrufe authentifiziert und autorisiert.
    - Tenant: Ihre Tenant-ID entspricht Ihrem Unternehmen und stellt eine dedizierte Azure AD-Instanz dar. Ermitteln Sie die Tenant-ID, indem Sie den Mauszeiger über Ihrem Kontonamen bewegen, um die Verzeichnis-/Tenant-ID zu erhalten, oder wählen Sie Azure Active Directory > Eigenschaften > Verzeichnis-ID im Azure-Portal aus.
    - Abonnement-ID: Abonnementberechtigungsnachweise, die Ihr Microsoft Azure-Abonnement eindeutig kennzeichnen. Die Abonnement-ID ist ein Bestandteil der URI für die einzelnen Serviceaufrufe.

    Anweisungen dazu, wie Sie Ihre Berechtigungsnachweise für Microsoft Azure beziehen, finden Sie in der zugehörigen Dokumentation unter [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.
    {: note}

1.  In {{site.data.keyword.aios_short}} sind die bereitgestellten Modelle aufgelistet. Wählen Sie die Modelle aus, die Sie überwachen möchten, und klicken Sie auf **Konfigurieren**.

Sie haben erfolgreich Bereitstellungen ausgewählt.

## Nutzdatenprotokollierung mit der Microsoft Azure Studio-Machine Learning-Engine
{: #cml-azconfig}

### Bindung für Microsoft Azure Machine Learning-Engine erstellen
{: #cml-azbind}

- Eine Nicht-{{site.data.keyword.pm_full}}-Engine wird als 'Angepasst' gebunden, was bedeutet, dass nur die Metadaten gebunden werden und somit keine direkte Integration mit dem Nicht-{{site.data.keyword.pm_full}}-Service besteht.

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
  Sie können Ihre Servicebindung mit dem folgenden Befehl anzeigen:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure Machine Learning-Bindung](images/ml-azure-bind.png)

### Microsoft Azure ML Studio-Abonnement hinzufügen
{: #cml-azsub}

- Abonnement hinzufügen

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
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
{: #cml-azenlog}

- Nutzdatenprotokollierung im Abonnement aktivieren

    ```python
    subscription.payload_logging.enable()
    ```

- Protokollierungsdetails abrufen

    ```python
    subscription.payload_logging.get_details()
    ```

### Scoring und Nutzdatenprotokollierung
{: #cml-azscore}

- Führen Sie ein Scoring für Ihr Modell durch. Ein vollständiges Beispiel finden Sie in [Notebook 'Mit der Azure Machine Learning Studio Engine arbeiten'](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

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
{: #ca-next}

Nun können Sie in {{site.data.keyword.aios_short}} die [Überwachungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
