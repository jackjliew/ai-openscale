---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Angepasste ML-Frameworks
{: #frmwrks-custom}

Mit Ihrem angepassten ML-Framework können Sie Nutzdatenprotokollierung, Rückmeldungsprotokollierung sowie Messungen der Leistungsgenauigkeit, Verzerrungserkennung zur Laufzeit, der Erklärbarkeit und der Funktion für automatische Verzerrungsbereinigung in {{site.data.keyword.aios_full}} ausführen. Das angepasste ML-Framework muss Äquivalenz zu {{site.data.keywor.pm_full}} besitzen.

{{site.data.keyword.aios_full}} unterstützt die folgenden angepassten ML-Frameworks vollständig:
{: shortdesc}

Tabelle 1. Details der Frameworkunterstützung

| Framework | Problemtyp | Datentyp |
|:---|:---:|:---:|
| Äquivalent zu {{site.data.keyword.pm_full}} | Klassifizierung | Strukturiert |
{: caption="Details der Frameworkunterstützung" caption-side="top"}

## Angepasste Machine Learning-Engine zu {{site.data.keyword.aios_short}} hinzufügen
{: #frmwrks-custom-add}

Sie können {{site.data.keyword.aios_short}} auf eine der folgenden Weisen für die Verwendung eines Anbieters für angepasstes Machine Learning konfigurieren:

- Wenn Sie zum ersten Mal einen Anbieter für angepasstes Machine Learning zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen finden Sie im Abschnitt [Angepasste Machine Learning-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Diese Methode müssen Sie verwenden, wenn mehrere Anbieter zur Verfügung stehen sollen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für angepasste Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Beispielnotebooks
{: #frmwrks-custom-smpl-ntbks}

- [Erstellung einer angepassten Machine Learning-Engine mit dem Kubernetes-Cluster](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Datamart-Erstellung, Überwachung der Modellbereitstellung und Datenanalyse](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Weiterführende Informationen
{: #frmwrks-custom-mediumblogs}

[Angepasste Machine Learning-Engine mit Watson OpenScale überwachen](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}

## Angepasste Machine Learning-Engine
{: #fmrk-workaround-customengine}

Eine angepasste Machine Learning-Engine stellt die Infrastruktur und Hosting-Funktionalität für Machine Learning-Modelle und -Webanwendungen bereit. Angepasste Machine Learning-Engines, die von {{site.data.keyword.aios_short}} unterstützt werden, müssen den folgenden Anforderungen entsprechen:

- Sie müssen zwei Typen von REST-API-Endpunkten zugänglich machen:

   * Erkennungsendpunkte (GET-Liste der Bereitstellungen und Details)
   * Scoring-Endpunkte (Online- und Echtzeit-Scoring)

- Alle Endpunkte müssen mit der Swagger-Spezifikation kompatibel sein, die unterstützt werden soll.

- Die Nutzdaten für die Eingabe in die Bereitstellung und für die Ausgabe aus der Bereitstellung müssen mit dem JSON-Dateiformat konform sein, das in der Spezifikation beschrieben wird.

Zum gegenwärtigen Zeitpunkt werden lediglich die Formate `BasicAuth` oder `none` (Keines) unterstützt.
{: Note}

Im folgenden Beispiel wird die Spezifikation für die REST-API-Endpunkte angezeigt:

![Anzeige der Spezifikation für die REST-API-Endpunkte aus dem Swagger-Dokument](images/wosdeployments.png)


Das folgende Beispiel veranschaulicht das Format für Eingabenutzdaten:

![Anzeige eines Beispiels für Eingabenutzdaten](images/wosinputdata.png)


## Wenn ist die Verwendung einer angepassten Machine Learning-Engine die Option der Wahl?
{: #fmrk-workaround-enging-choice}

Eine angepasste Machine Learning-Engine ist die beste Wahl, wenn die folgenden Situationen zutreffen:

- Sie verwenden keines der verfügbaren Out-of-the-box-Produkte für Ihre Machine Learning-Modelle. Für Ihre Modelle haben Sie gerade ein eigenes System entwickelt. Dafür gibt es weder gegenwärtig noch künftig direkte Unterstützung in {{site.data.keyword.aios_short}}.
- Die von Ihnen verwendete Bedienungsengine eines anderen Anbieters wird von {{site.data.keyword.aios_short}} gegenwärtig (noch) nicht unterstützt. In diesem Fall sollten Sie die Entwicklung einer angepassten Engine für maschinelles Lernen als Wrapper für Ihre ursprünglichen oder nativen Bereitstellungen in Betracht ziehen.

## Angepasste ML-Serviceinstanz angeben
{: #co-connect}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Serviceinstanz an. In Ihrer Serviceinstanz speichern Sie Ihre AI-Modelle und -Bereitstellungen.
{: shortdesc}

## Angepasste Serviceinstanz verbinden
{: #co-config}

{{site.data.keyword.aios_short}} stellt die Verbindung zu AI-Modellen und Bereitstellungen in einer Serviceinstanz her. Sie können eine Verbindung zu einem angepassten Service herstellen.

1.  Klicken Sie auf der Registerkarte **Konfigurieren** im Navigationsfenster auf **Machine Learning-Provider**.

   ![Darstellung der Anzeige für die Auswahl des Machine Learning-Providers, mit Kacheln für die unterstützten Machine Learning-Engines.](images/wos-machine-learning-providers-selection.png)

2. Klicken Sie auf die Schaltfläche **Machine Learning-Provider hinzufügen** und dann auf die Kachel **Angepasste Umgebung**.

   ![Darstellung der Konfigurationsanzeige für angepasste ML-Provider mit Feldern für Berechtigungsnachweise, Instanznamen und Beschreibung](images/ml-custom-provider.png)

3. Geben Sie einen Namen und eine Beschreibung für Ihren Anbieter für angepasstes Machine Learning ein und klicken Sie auf **Weiter**. 

4. Wählen Sie aus, ob Sie eine Verbindung zu Ihren Bereitstellungen herstellen möchten, indem Sie eine [Liste anfordern](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) oder indem Sie [einzelne Scoring-Endpunkte eingeben](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![Darstellung der Anzeige für die Verbindung zu Bereitstellungen, mit Optionen zur Anforderung einer Liste von Bereitstellungen oder zur Eingabe eines einzelnen Scoring-Endpunkts](images/ml-custom-connect-deployments.png)
    
5. Klicken Sie auf **Weiter**.

### Bereitstellungsliste anfordern
{: #co-config-request-list}

1. Geben Sie bei Auswahl der Kachel **Bereitstellungsliste anfordern** Ihre Berechtigungsnachweise und den API-Endpunkt ein und klicken Sie dann auf **Speichern**.

   ![Darstellung der Anzeige mit der Liste von Bereitstellungen, mit Feldern zur Eingabe von Serviceberechtigungsnachweisen und eines API-Endpunkts](images/connect-custom-cred.png)

2. Kehren Sie nach dem Speichern Ihrer Machine Learning-Konfiguration zum **Dashboard** zurück, klicken Sie auf die Registerkarte **Insights** und dann auf **Zum Dashboard hinzufügen** button.

3. Wählen Sie eine Bereitstellung in der Liste aus und klicken Sie auf **Konfigurieren**.

Nun können Sie die Überwachung konfigurieren.

### Einzelne Scoring-Endpunkte angeben
{: #co-config-scoring-endpoints}

1. Geben Sie bei Auswahl der Kachel **Individuelle Scoring-Endpunkte eingeben** Ihre Berechtigungsnachweise für den API-Endpunkt ein und klicken Sie dann auf **Speichern**.

2. Kehren Sie nach dem Speichern Ihrer Machine Learning-Konfiguration zum **Dashboard** zurück, klicken Sie auf die Registerkarte **Insights** und dann auf **Zum Dashboard hinzufügen** button.

3. Klicken Sie auf die Schaltfläche **Endpunkt hinzufügen**.

4. Wählen Sie im Dropdown-Menü die angepasste Umgebung aus, geben Sie den Namen der Bereitstellung und den API-Endpunkt ein und klicken Sie auf **Speichern**.

Nun können Sie die Überwachung konfigurieren.

### Funktionsweise
{: #co-works}

Die folgende Abbildung verdeutlicht die Unterstützung für die angepasste Umgebung:

![Darstellung des Diagramms zur Funktionsweise von 'Angepasst', mit Feldern für die angepasste Umgebung, Client-API und Watson OpenScale-API](images/custom-how-works.png)

Weitere Informationen können Sie auch über die folgenden Links aufrufen:

[{{site.data.keyword.aios_short}}-API für Nutzdatenprotokollierung](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[API für angepasste Bereitstellung](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[SDK für Python-Clientbindung](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[Mit der angepassten Machine Learning-Engine arbeiten](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[Python-SDK für IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **Eingabekriterien für das Modell zur Unterstützung von Überwachungen**

  Ihr Modell sollte einen Merkmalvektor als Eingabe verwenden. Dabei handelt es sich im Wesentlichen um eine Sammlung (Gruppe) von benannten Feldern und ihren Werten, wobei die Felder, die auf Verzerrung überwacht werden, eine Gruppe dieser Felder darstellen:

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  In diesem Beispiel könnte `"age"` ein Feld sein, das von jemandem auf Fairness hin ausgewertet wird.

  Wenn es sich bei der Eingabe um einen Tensor/Matrix handelt, der aus dem Eingabemerkmalbereich transformiert wird (was bei Deep Learning - also 'tiefgehendem Lernen' - aus Text oder Images oft der Fall ist), kann dieses Modell von der {{site.data.keyword.aios_short}}-Plattform im aktuellen Release nicht verarbeitet werden. Im weiteren Sinne können Deep-Learning-Modelle mit Text- oder Imageeingaben nicht zur Erkennung und Entschärfung von Verzerrungen verwendet werden.

  Zusätzlich sollten zur Unterstützung der Erklärbarkeit Trainingsdaten geladen werden.

  Zur Erklärbarkeit von Text sollte der gesamte Text eines der Merkmale sein. Die Erklärbarkeit von Images für ein Modell vom Typ 'Angepasst' wird im aktuellen Release nicht unterstützt.
  {: note}

- **Ausgabekriterien für das Modell zur Unterstützung von Überwachungen**

  Ihr Modell sollte neben den Vorhersagewahrscheinlichkeiten verschiedener Klassen in diesem Modell den Eingabemerkmalvektor ausgeben.

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  Im vorliegenden Beispiel sind `"personal”` und `"camping"` die möglichen Klassen und die Bewertungen in jeder Scoring-Ausgabe werden beiden Klassen zugewiesen. Wenn die Vorhersagewahrscheinlichkeiten fehlen, funktioniert zwar die Erkennung von Verzerrungen, nicht aber die automatische Verzerrungsbereinigung.

  Die vorhergehende Scoring-Ausgabe muss von einem Live-Scoring-Endpunkt aus zugänglich sein, der von {{site.data.keyword.aios_short}} über REST aufgerufen werden kann. Für AzureML, SageMaker und {{site.data.keyword.pm_full}} wird von {{site.data.keyword.aios_short}} direkt eine Verbindung zu nativen Scoring-Endpunkten aufgebaut, sodass Sie sich keine Gedanken um die Implementierung der Scoring-Spezifikation machen müssen.

## Angepasste Machine Learning-Engine - Beispiele
{: #fmrk-workaround-cstmmlsengex}

Orientieren Sie sich an den folgenden Beispielen, um Ihre eigene angepasste Machine Learning-Engine einzurichten.
{: shortdesc}

### Python und Flask
{: #fmrk-workaround-pandflask}

Das [auf Git veröffentlichte Beispiel einer angepassten Machine Learning-Engine](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external} verwendet Python und Flask, um das Modell 'scikit-learn' zu bedienen.

In der [README-Datei](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external} enthält eine Beschreibung zur lokalen Bereitstellung der App zu Testzwecken sowie als cf-Anwendung unter IBM Cloud. Die Implementierung von REST-API-Endpunkten finden Sie in der [app.py-Datei](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py){: external}.

### Node.js
{: #fmrk-workaround-nodejs}

Ein Beispiel für eine JSON geschriebene angepasste Machine Learning-Engine finden Sie im [Node.js-Beispiel](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs){: external}.

### End-to-End-Codemuster
{: #fmrk-workaround-e2ecode}

Das [Codemuster](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale){: external} veranschaulicht anhand eines End-to-End-Beispiels die durchgängige Bereitstellung und Integration einer angepassten Machine Learning-Engine mit {{site.data.keyword.aios_short}}.

## Nutzdatenprotokollierung mit der angepassten Machine Learning-Engine
{: #cml-cusconfig}

### Bindung für angepasste Machine Learning-Engine erstellen
{: #cml-cusbind}

- Eine Nicht-{{site.data.keyword.pm_full}}-Engine wird als 'Angepasst' gebunden, was bedeutet, dass nur die Metadaten gebunden werden und somit keine direkte Integration mit dem Nicht-{{site.data.keyword.pm_full}}-Service besteht. Mit der Methode `client.data_mart.bindings.add` können Sie mehr als eine Machine Learning-Engine an {{site.data.keyword.aios_short}} binden.

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  Sie können Ihre Servicebindung mit dem folgenden Befehl anzeigen:

    ```python
    client.data_mart.bindings.list()
    ```

    ![Generische ML-Bindung](images/ml-generic-bind.png)

### Angepasstes Abonnement
{: #cml-cussub}

- Abonnement hinzufügen

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- Abonnementliste abrufen

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Nutzdatenprotokollierung aktivieren
{: #cml-cusenlog}

- Nutzdatenprotokollierung im Abonnement aktivieren

    ```python
    subscription.payload_logging.enable()
    ```

- Protokollierungsdetails abrufen

    ```python
    subscription.payload_logging.get_details()
    ```

Weitere Informationen finden Sie in [Nutzdatenprotokollierung](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

### Scoring und Nutzdatenprotokollierung
{: #cml-cusscore}

- Führen Sie ein Scoring für Ihr Modell durch. Ein ausführliches Beispiel enthält das [Notebook für IBM {{site.data.keyword.aios_full}} & angepasste ML-Engines](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}.

- Anforderung und Antwort in der Nutzdatenprotokollierungstabelle speichern

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

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
{: #fmrk-workaround-nxt-steps-over}

Nun können Sie in {{site.data.keyword.aios_short}} die [Überwachungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config).

Implementieren Sie Ihre eigene Lösung, indem Sie eines der folgenden [Beispiele für angepasstes Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex) verwenden.
