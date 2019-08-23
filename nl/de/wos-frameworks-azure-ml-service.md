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

# Microsoft Azure ML Service-Frameworks
{: #frmwrks-azure-service}

Mit Microsoft Azure ML Service können Sie Nutzdatenprotokollierung, Rückmeldungsprotokollierung sowie Messungen der Leistungsgenauigkeit, Verzerrungserkennung zur Laufzeit, der Erklärbarkeit und der Funktion für automatische Verzerrungsbereinigung in {{site.data.keyword.aios_full}} ausführen.

{{site.data.keyword.aios_full}} unterstützt die folgenden Microsoft Azure Machine Learning Service-Frameworks vollständig:
{: shortdesc}

Tabelle 1. Details der Frameworkunterstützung

| Framework | Problemtyp | Datentyp |
|:---|:---:|:---:|
| Nativ | Klassifizierung | Strukturiert |
| scikit-learn | Klassifizierung | Strukturiert |
| scikit-learn | Regression | Strukturiert |
{: caption="Details der Frameworkunterstützung" caption-side="top"}

## Microsoft Azure ML Service zu {{site.data.keyword.aios_short}} hinzufügen
{: #frmwrks-azureservice-addsrvc}

Sie können {{site.data.keyword.aios_short}} auf eine der folgenden Weisen für die Verwendung von Microsoft Azure ML Service konfigurieren:

- Wenn Sie zum ersten Mal einen Machine Learning-Provider zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen finden Sie im Abschnitt [Microsoft Azure ML Service-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice).
- Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Diese Methode müssen Sie verwenden, wenn mehrere Anbieter zur Verfügung stehen sollen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Microsoft Azure-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).


{{site.data.keyword.aios_short}} ruft verschiedene REST-Endpunkte auf, die für die Interaktion mit Azure ML Service erforderlich sind. Um dies zu tun, müssen Sie eine Bindung für Azure Machine Learning Service in {{site.data.keyword.aios_short}} erstellen.

1. Erstellen Sie einen Azure Active Directory-Dienstprinzipal.
2. Geben Sie die Berechtigungsnachweisdetails an, wenn Sie die Bindung des Azure ML Service über die Benutzerschnittstelle oder das Python-SDK von {{site.data.keyword.aios_short}} hinzufügen.

## Voraussetzungen für JSON-Anforderungs- und -Antwortdateien
{: #frmwrks-azureservice-JSON}

Damit Azure ML Service in Verbindung mit {{site.data.keyword.aios_short}} verwendet werden kann, müssen die von Ihnen erstellten Web-Service-Bereitstellungen bestimmte Anforderungen erfüllen. Die von Ihnen erstellten Web-Service-Bereitstellungen müssen entsprechend den im Folgenden angegebenen Vorgaben JSON-Anforderungen akzeptieren und JSON-Antworten zurückgeben.

### Erforderliches JSON-Anforderungsformat für Web-Services
{: #frmwrks-azureservice-JSON-sample-request}

- Der Hauptteil der REST-API-Anforderung muss ein einziges JSON-Dokument sein, das ein JSON-Array mit JSON-Objekten enthält.
- Das JSON-Array muss den Namen `"input"` aufweisen.
- Jedes JSON-Objekt darf nur einfache Schlüssel/Wert-Paare enthalten. Zulässige Werte sind Zeichenfolgen, Zahlen, `true`, `false` und `null`.
- Bei den Werten darf es sich nicht um JSON-Objekte oder -Arrays handeln.
- Die einzelnen JSON-Objekte im Array müssen dieselben Schlüssel (und somit auch dieselbe Schlüsselanzahl) aufweisen, unabhängig davon, ob ein Wert verfügbar ist, bei dem es sich nicht um einen `Null`-Wert handelt.


Die folgende JSON-Beispieldatei entspricht den oben genannten Anforderungen und kann als Vorlage für die Erstellung eigener JSON-Anforderungsdateien verwendet werden:


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


### Erforderliches JSON-Antwortformat für Web-Services
{: #frmwrks-azureservice-JSON-sample-response}

Beachten Sie die folgenden Elemente, wenn Sie eine JSON-Antwortdatei erstellen:

- Der REST-API-Antworthauptteil muss ein JSON-Dokument sein, das ein JSON-Array mit JSON-Objekten enthält.
- Das JSON-Array muss den Namen `"output"` aufweisen.
- Jedes JSON-Objekt darf nur Schlüssel/Wert-Paare enthalten. Zulässige Werte sind Zeichenfolgen, Zahlen, `true`, `false`, `null` und Arrays, die keine anderen JSON-Objekte oder -Arrays enthalten.
- Bei den Werten darf es sich nicht um JSON-Objekte handeln.
- Die einzelnen JSON-Objekte im Array müssen dieselben Schlüssel (und dieselbe Schlüsselanzahl) aufweisen, unabhängig davon, ob ein Wert verfügbar ist, bei dem es sich nicht um einen `Null`-Wert handelt.
- Für Klassifizierungsmodelle: Der Web-Service muss ein Array mit Wahrscheinlichkeiten für die einzelnen Klasse zurückgeben und die Reihenfolge der Wahrscheinlichkeiten muss für jedes JSON-Objekt im Array konsistent sein.
  - Dazu ein Beispiel: Angenommen, Sie verfügen über ein binäres Klassifizierungsmodell zur Vorhersage des Kreditrisikos, das die Klassen `Risk` und `No Risk` enthält.
  - Bei jedem zurückgegebenen Ergebnis im Array "output" müssen die Objekte ein Schlüssel/Wert-Paar enthalten, bei dem die Wahrscheinlichkeiten die folgende festgelegte Reihenfolge aufweisen:
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

Im Hinblick auf die Konsistenz mit den in Azure ML Studio und Azure ML Service verwendeten grafisch orientierten Azure ML-Tools empfiehlt es sich, die folgenden Schlüsselnamen zu verwenden, auch wenn dies nicht unbedingt erforderlich ist:

- Schlüsselname `"Scored Labels"` für den Ausgabeschlüssel, der den vorhergesagten Wert des Modells angibt
- Schlüsselname `"Scored Probabilities"` für den Ausgabeschlüssel, der ein Array von Wahrscheinlichkeiten für die einzelnen Klassen angibt

Die folgende JSON-Beispieldatei entspricht den oben genannten Anforderungen und kann als Vorlage für die Erstellung eigener JSON-Antwortdateien verwendet werden:


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

## Beispielnotebooks
{: #frmwrks-azureservice-smpl-ntbks}

Die folgenden Notebooks enthalten Informationen zur Verwendung von Microsoft Azure ML Service:

- [Scoring-Beispiele für MS Azure Service-Modelle](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## Microsoft Azure ML Service-Instanz angeben
{: #connect-azureservice}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Microsoft Azure ML Service-Instanz an. In der Azure ML Service-Instanz werden die AI-Modelle und -Bereitstellungen gespeichert.
{: shortdesc}

Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Microsoft Azure Service Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Verbindung zur Azure ML Service-Instanz herstellen
{: #ca-connect}

{{site.data.keyword.aios_short}} stellt die Verbindung zu AI-Modellen und Bereitstellungen in einer Azure ML Service-Instanz her.

1.  Klicken Sie auf der Registerkarte **Konfigurieren** im Navigationsfenster auf **Machine Learning-Provider**.
1.  Klicken Sie auf die Schaltfläche **Machine Learning-Provider hinzufügen** und dann auf die Kachel **Microsoft Azure ML Service**.
1.  Geben Sie Ihre Berechtigungsnachweise ein und speichern Sie sie:

    - Client-ID: Der tatsächliche Zeichenfolgewert Ihrer Client-ID, der Ihre Identität nachweist und Ihre Azure Service-Aufrufe authentifiziert und autorisiert.
    - Geheimer Clientschlüssel: Der tatsächliche Zeichenfolgewert Ihres geheimen Clientschlüssels, der Ihre Identität nachweist und Ihre Azure Service-Aufrufe authentifiziert und autorisiert.
    - Tenant: Ihre Tenant-ID entspricht Ihrem Unternehmen und stellt eine dedizierte Azure AD-Instanz dar. Ermitteln Sie die Tenant-ID, indem Sie den Mauszeiger über Ihrem Kontonamen bewegen, um die Verzeichnis-/Tenant-ID zu erhalten, oder wählen Sie Azure Active Directory > Eigenschaften > Verzeichnis-ID im Azure-Portal aus.
    - Abonnement-ID: Abonnementberechtigungsnachweise, die Ihr Microsoft Azure-Abonnement eindeutig kennzeichnen. Die Abonnement-ID ist ein Bestandteil der URI für die einzelnen Serviceaufrufe.

    Anweisungen dazu, wie Sie Ihre Berechtigungsnachweise für Microsoft Azure beziehen, finden Sie in der zugehörigen Dokumentation unter [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.
    {: note}

1.  In {{site.data.keyword.aios_short}} sind die bereitgestellten Modelle aufgelistet. Wählen Sie die Modelle aus, die Sie überwachen möchten, und klicken Sie auf **Konfigurieren**.

Sie haben erfolgreich Bereitstellungen ausgewählt.

## Nutzdatenprotokollierung mit der Microsoft Azure ML Service-Engine
{: #cml-azsrvconfig}

### Bindung für Microsoft Azure ML Service-Engine erstellen
{: #cml-azsrvbind}

Eine Nicht-{{site.data.keyword.pm_full}}-Engine wird als 'Angepasst' gebunden, was bedeutet, dass nur die Metadaten gebunden werden und somit keine direkte Integration mit dem Nicht-{{site.data.keyword.pm_full}}-Service besteht.
   
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

Sie können Ihre Servicebindung mit dem folgenden Befehl anzeigen:

```
client.data_mart.bindings.list()
```
{: codeblock}

Beispielausgabe:

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### Microsoft Azure ML Service-Abonnement hinzufügen
{: #cml-azsrvsub}

Abonnement hinzufügen

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

Abonnementliste abrufen

```
subscriptions = client.data_mart.subscriptions.get_details()

subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
```
{: codeblock}

### Nutzdatenprotokollierung aktivieren
{: #cml-azsrvenlog}

Nutzdatenprotokollierung im Abonnement aktivieren

```
subscription.payload_logging.enable()
```
{: codeblock}

Protokollierungsdetails abrufen

```
subscription.payload_logging.get_details()
```
{: codeblock}

### Scoring und Nutzdatenprotokollierung
{: #cml-azsrvscore}

Führen Sie ein Scoring für Ihr Modell durch. Ein vollständiges Beispiel enthält das [Notebook 'Mit der Azure Machine Learning Service Engine arbeiten'](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

Anforderung und Antwort in der Nutzdatenprotokollierungstabelle speichern:

```
records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

subscription.payload_logging.store(records=records_list)
```
{: codeblock}
{: python}
   
Für andere Sprachen als Python können Sie die Nutzdatenprotokollierung auch direkt über eine REST-API ausführen.
   
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



## Weitere Schritte
{: #ca-next}

-Nun können Sie in {{site.data.keyword.aios_short}} die [Überwachungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [Wie unterscheidet sich Azure Machine Learning Service von Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

