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

- Wenn Sie zum ersten Mal einen Machine Learning-Anbieter zu {{site.data.keyword.aios_short}} hinzufügen, können Sie die Konfigurationsschnittstelle verwenden. Weitere Informationen finden Sie im Abschnitt [Microsoft Azure ML Service-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice).
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

- [Datamart-Erstellung, Überwachung der Modellbereitstellung und Datenanalyse](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Scoring-Beispiele für MS Azure Service-Modelle](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Weiterführende Informationen
{: #frmwrks-azureservice-mediumblogs}

- [Wie unterscheidet sich Azure Machine Learning Service von Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
