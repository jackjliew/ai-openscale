---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Python, install, python module, setup, set up, insights, explainability

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Python-Modul zum Konfigurieren von {{site.data.keyword.aios_short}} installieren
{: #as-module}

Um die Einrichtung und Konfiguration der erforderlichen {{site.data.keyword.cloud_notm}}-Services zu automatisieren und eine {{site.data.keyword.aios_full}}-Anwendung (einschließlich Stichprobendaten) zu sehen, können Sie ein Python-Modul installieren.
{: shortdesc}

## Informationen zu diesem Modul
{: #as-about}

- Das Modul bietet technischen Benutzern eine alternative Möglichkeit, eine betriebsbereite Instanz von {{site.data.keyword.aios_short}} zu sehen, ohne jedoch die Services wie im Lernprogramm [Erste Schritte](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) beschrieben selbst einrichten und konfigurieren zu müssen.
- Das Python-Modul durchläuft einen Prozess zur Überprüfung der Services, über die Sie verfügen, und zur Erstellung der notwendigen Services einschließlich {{site.data.keyword.aios_short}}. Nachdem das Modul erfolgreich ausgeführt wird, können Sie {{site.data.keyword.aios_short}} über das {{site.data.keyword.cloud_notm}}-Dashboard starten, um zu erleben, wie die Überwachung eines Modells erfolgt.

## Vorbereitende Schritte
{: #as-prereqs}

1. [Erstellen Sie einen {{site.data.keyword.cloud_notm}}-API-Schlüssel und laden Sie ihn herunter](/docs/iam?topic=iam-userapikey#create_user_key). Diesen API-Schlüssel müssen Sie in einem späteren Schritt eingeben.

2. [Installieren Sie beliebiges Release von Python 3 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.python.org/downloads/){: new_window}.

  Python 3 beinhaltet das erforderliche Managementsystem für pip-Paketen.
  {: note}

3. Installieren Sie das Paket `ibm-ai-openscale-cli`, indem Sie folgenden Befehl ausführen:

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    Wenn mehr als nur eine Version von pip auf Ihrem System installiert ist, müssen Sie an Stelle von `pip` gegebenenfalls `pip3` wie in dem Befehl `pip3 install -U ibm-ai-openscale-cli` absetzen.
    {: tip}

4. Wenn Sie über eine vorhandene {{site.data.keyword.pm_short}}-Serviceinstanz verfügen, prüfen Sie das [{{site.data.keyword.cloud_notm}}-Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}){: new_window}, um sicherzustellen, dass der Service von {{site.data.keyword.iamshort}} (IAM) verwaltet wird und nicht von Cloud Foundry.

  **Wichtig**: Das Modul prüft, ob eine Instanz von {{site.data.keyword.pm_short}} vorhanden ist. Wenn Sie über eine solche Instanz verfügen, verwendet das Modul sie. Wenn Ihre Instanz jedoch von der Cloud Foundry verwaltet wird, müssen Sie zuerst die [Instanz vor Ausführen des Moduls zu einer IAM-Ressourcengruppe migrieren](/docs/resources?topic=resources-migrate#migrate).

## Modul ausführen
{: #as-run}

Führen Sie den folgenden Befehl aus:

```
ibm-ai-openscale-cli --apikey <Ihr API-Schlüssel>
```
{: codeblock}

## Ergebnisse in {{site.data.keyword.aios_short}} anzeigen
{: #as-open}

Um Einblicke in die Fairness und Genauigkeit des Modells, die Details der zu überwachenden Daten und die Erklärbarkeit für eine einzelne Transaktion zu erhalten, öffnen Sie das [{{site.data.keyword.aios_short}}-Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}.

- Um das Szenario für die Stichprobendaten zu verstehen, lesen Sie [Anwendungsfall und der Wert von {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use).

### Einsichten anzeigen
{: #as-insights}

Klicken Sie im [{{site.data.keyword.aios_short}}-Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} auf die Registerkarte **Einsichten**, auf der eine Übersicht der Metriken für bereitgestellte Modelle angezeigt wird: !['Einsichten'](images/insight-dash-tab.png)

- Die Seite 'Einsichten' zeigt auf einen Blick alle eventuellen Probleme mit Fairness und Genauigkeit wie durch die konfigurierten Schwellenwerte bestimmt an.

- Jede Bereitstellung wird als Kachel angezeigt. Das Modul hat eine Bereitstellung namens `GermanCreditRiskModel` konfiguriert, wie auf dem folgenden Screenshot zu sehen ist:

  ![Überblick über 'Einsichten'](images/setup01-0206.png)

### Überwachungsdaten anzeigen
{: #as-monitoring}

1. Klicken Sie auf der Seite 'Einsichten' auf die Kachel `GermanCreditRiskModel`, um Details zu den überwachten Daten anzuzeigen.
2. Verschieben Sie die Markierung auf dem Diagramm, um einen Tag und einen Zeitraum anzuzeigen, für den Daten vorhanden sind, und klicken Sie dann auf den Link **Details anzeigen**.

   - Die folgende Anzeige enthält beispielsweise Daten für ein bestimmtes Datum und eine bestimmte Uhrzeit. Die Daten und Zeiten variieren je nachdem, wann Sie das Modul ausführen.

   - Informationen zur Interpretation des Zeitreihendiagramms erhalten Sie in [Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-it-ov).

    ![Daten überwachen](images/setup02-0206.png)

3. Damit Details zur Überwachung von Daten zum `ALTER` angezeigt werden, stellen Sie sicher, dass im Dropdown-Menü die Option `ALTER` ausgewählt ist.

  - Beachten Sie, dass im folgenden Screenshot keine Verzerrung vorliegt.

  - Informationen zur Interpretation des Diagramms der Datenpunkte zu einer bestimmten Uhrzeit enthält der Abschnitt [Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp).

    ![Details anzeigen](images/setup03-0206.png)

### Erklärbarkeit anzeigen
{: #as-explain}

Um die Faktoren zu verstehen, die beteiligt sind, wenn eine Verzerrung für einen bestimmten Zeitraum vorliegt, wählen Sie in der im vorherigen Abschnitt dargestellten Visualisierungsanzeige die Schaltfläche the **Transaktionen anzeigen** aus.

Für diejenigen Transaktionen, die eine Verzerrung aufweisen, werden die Transaktions-IDs der letzten Stunde aufgelistet. Für das in diesem Modul verwendete Modell besteht keine Verzerrung für Anforderungen, die verfügbar sind. Daher werden im folgenden Screenshot für den Zeitraum keine Transaktionen angezeigt.

  ![Transaktionsliste ohne Transaktionen](images/setup06-0206.png)

Informationen dazu, wie Sie Transaktionen suchen und erläutern, finden Sie in [Transaktionen erklären](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view).

## Zugehörige Informationen
{: #as-info}

- Wenn Sie mehr über Verzerrungen erfahren möchten, können Sie in [Fairness](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) nachlesen.
- Informationen dazu, wie gut Ihr Modell Ergebnisse vorhersagt, finden Sie in [Genauigkeit](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Informationen zur Interpretation von Diagrammen und Daten enthält [Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-it-ov).
- Um zu erfahren, wie zugrunde liegende Faktoren die Ergebnisse beeinflussen, lesen Sie [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
