---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: machine learning, services, ml, custom 

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

# Angepasste ML-Serviceinstanz angeben
{: #co-connect}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Serviceinstanz an. In Ihrer Serviceinstanz speichern Sie Ihre AI-Modelle und -Bereitstellungen.
{: shortdesc}

## Angepasste Serviceinstanz verbinden
{: #co-config}

{{site.data.keyword.aios_short}} stellt die Verbindung zu AI-Modellen und Bereitstellungen in einer Serviceinstanz her.

1.  Klicken Sie auf der Startseite des {{site.data.keyword.aios_short}}-Tools auf **Beginnen**.

    ![Startseite](images/gs-config-start.png)

2.  Wählen Sie die Kachel **Angepasst** aus und klicken Sie auf **Weiter**.

    !['Angepasst' auswählen](images/connect-custom.png)

3.  Stellen Sie eine Verbindung zu Bereitstellungen her, indem Sie eine der folgenden Optionen auswählen:

    !['Angepasst' auswählen](images/connect-custom-deploy.png)

4.  Wenn Sie die Kachel 'Individuelle Scoring-Endpunkte eingeben' ausgewählt haben, geben Sie Ihre Berechtigungsnachweise ein:

    ![Serviceberechtigungsnachweise eingeben](images/connect-custom-cred.png)

5.  Klicken Sie auf **Weiter**.

    - Wenn Sie die Kachel 'Individuelle Scoring-Endpunkte eingeben' ausgewählt haben, müssen Sie einen Bereitstellungsnamen und einen Endpunkt angeben:

      ![Serviceberechtigungsnachweise eingeben](images/connect-custom-endpoint.png)

      Klicken Sie auf **Weiter**.

    - Wenn Sie die Kachel 'Bereitstellungsliste anfordern' ausgewählt haben, müssen Sie einen Hostnamen oder eine IP-Adresse und eine Portnummer angeben:

      ![Serviceberechtigungsnachweise eingeben](images/connect-custom-apiendpoint.png)

      Klicken Sie auf **Weiter**.

      Treffen Sie anschließend in der Liste der Bereitstellungen Ihre Auswahl:

      ![Serviceberechtigungsnachweise eingeben](images/connect-custom-apiendpoint2.png)

6.  Überprüfen Sie die ausgewählten Bereitstellungen.

    ![Serviceberechtigungsnachweise eingeben](images/connect-custom-deploy2.png)

7.  Klicken Sie auf **Weiter**.

### Funktionsweise
{: #co-works}

Diese Abbildung stellt die Unterstützung für die Umgebung 'Angepasst' dar:

![Funktionsweise von 'Angepasst'](images/custom-how-works.png)

Sie können sich auch auf die folgenden Links beziehen:

[API für die Protokollierung von AIOS-Nutzdaten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[API für angepasste Bereitstellung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[Bindungs-SDK für Python-Clients ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[Mit der angepassten ML-Engine arbeiten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[Python-SDK für IBM Watson OpenScale ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

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

  Wenn es sich bei der Eingabe um einen Tensor/Matrix handelt, der aus dem Eingabemerkmalbereich transformiert wird (was bei Deep Learning - also 'tiefgehendem Lernen' - aus Text oder Bildern oft der Fall ist), kann dieses Modell von der {{site.data.keyword.aios_short}}-Plattform im aktuellen Release nicht verarbeitet werden. Im weiteren Sinne können Deep-Learning-Modelle mit Text- oder Bildeingaben nicht zur Erkennung und Entschärfung von Verzerrungen verwendet werden.

  Zusätzlich sollten zur Unterstützung der Erklärbarkeit Trainingsdaten geladen werden.

  Zur Erklärbarkeit von Text sollte der gesamte Text eines der Merkmale sein. Die Erklärbarkeit von Bildern für ein Modell vom Typ 'Angepasst' wird im aktuellen Release nicht unterstützt.
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

  Im vorliegenden Beispiel sind `"personal”` und `"camping"` die möglichen Klassen und die Bewertungen in jeder Scoring-Ausgabe werden beiden Klassen zugewiesen. Wenn die Vorhersagewahrscheinlichkeiten fehlen, funktioniert zwar die Erkennung von Verzerrungen, nicht aber die automatische Entzerrung.

  Der Zugriff auf die obige Scoring-Ausgabe sollte über einen Live-Scoring-Endpunkt möglich sein, den {{site.data.keyword.aios_short}} über REST aufrufen könnte. Für AzureML, SageMaker und WML stellt {{site.data.keyword.aios_short}} eine direkte Verbindung zu den nativen Scoring-Endpunkten her, sodass Sie sich keine Gedanken über die Implementierung der Scoring-Spezifikationen machen müssen.

### Weitere Schritte
{: #co-next}

{{site.data.keyword.aios_short}} ist jetzt so eingerichtet, dass Sie eine [Datenbank angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-db) können.
