---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Im Dashboard navigieren
{: #io-ov}

Sie können alle Bereitstellungen, die Sie überwachen, über das {{site.data.keyword.aios_short}}-Dashboard verfolgen. Das Dashboard liefert die Hauptansicht von {{site.data.keyword.aios_short}}. Das Dashboard besteht aus fünf Registerkarten:

  ![Registerkarte 'Einsichten'](images/insight-tabs.png)

{: shortdesc}

## Einsichten
{: #io-ins}

Die Registerkarte **Einsichten** ( ![Dashboard für Einsichten](images/insight-dash-tab.png) ) liefert eine allgemeine Ansicht Ihrer Bereitstellungsüberwachung.

  ![Dashboard für Einsichten](images/insight-dashboard.png)

- ***Überwachte Bereitstellungen***: In diesem Beispiel werden insgesamt 10 Bereitstellungen überwacht. Acht der zehn Bereitstellungen sind unten als einzelne Kacheln dargestellt.

- ***Genauigkeitsalerts***: Es werden insgesamt drei Genauigkeitsalerts in den Kacheln unten durch purpurrote Schattierung dargestellt. In diesem Beispiel weisen die Bereitstellungen `Treiberleistung`, `Marktanalyse` und `Preisrisiko` Genauigkeitswerte in Höhe von `60 %`, `65 %` bzw. `79 %` auf.

- ***Fairnessalerts***: Es sind insgesamt 6 Fairnessalerts vorhanden, die in den Kacheln unten sowohl durch purpurrote Schattierung als auch durch einen kleinen Tag für `VERZERRUNG` kenntlich gemacht sind. In diesem Beispiel weisen die Bereitstellungen `Treiberleistung`, `Marktanalyse`, `Einhaltung gesetzlicher Bestimmungen`, `Betrugserkennung`, `Premium-Optimierung` und `Kostenschätzer für Schaden` Fairnesswerte von `59 %`, `68 %`, `62 %`, `64 %`, `79 %` und `63 %` auf.

Jede Kachel liefert eine Zusammenfassung der Überwachungsaktivitäten für diese Bereitstellung. Beachten Sie, dass die Kachel für die Bereitstellung `Call-Center-Routing` keine Probleme aufweist, was auf ein recht stabiles, genaues Modell hinweist.

### Weitere Schritte
{: #io-next}

Wählen Sie eine beliebige einzelne Bereitstellungskachel aus, damit weitere Details zu dieser Bereitstellung angezeigt werden. Weitere Informationen enthalten die Abschnitte [Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-it-ov) und [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Konfiguration
{: #io-conf}

Die Registerkarte **Konfigurieren** ( ![Registerkarte 'Konfigurieren'](images/insight-config-tab.png) ) öffnet eine Zusammenfassung der Konfiguration für die ausgewählte Bereitstellung.

  ![Konfigurationszusammenfassung](images/insight-config-summary.png)

Von hier aus können Sie die Konfigurationseinstellungen für Ihre Bereitstellungsüberwachung direkt bearbeiten.

## Transaktionen
{: #io-tran}

Mit der Registerkarte **Transaktion erklären** (![Registerkarte 'Transaktion erklären'](images/insight-transact-tab.png)) können Sie nach einer bestimmten Transaktions-ID suchen, um eine Erklärung einer bestimmten Bereitstellungstransaktion zu erhalten. Weitere Informationen hierzu enthält der Abschnitt [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## AI-Tools
{: #io-too}

Verwenden Sie die Registerkarte **AI-Tools** (![Registerkarte 'AI-Tools'](images/aitools.png)), um einen Dialog zu öffnen, der einen Link zu weiteren Optionen für IBM AI-Tools enthält.

- *[Watson Studio-Lite-Plan ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*: Watson Studio bietet Ihnen die Umgebung und die Tools, um Daten zu analysieren und zu visualisieren, Daten zu bereinigen und zu formen (Shapedaten), Streamingdaten einzupflegen oder Machine Learning-Modelle zu erstellen, zu trainieren und bereitzustellen. Klicken Sie auf den Link 'Registrierung für kostenlosen Watson Studio-Lite-Plan durchführen', um Watson Studio abzurufen.

## Registerkarte 'Hilfe'
{: #io-help}

Die Registerkarte 'Hilfe' ( ![Registerkarte 'Hilfe'](images/insight-help-tab.png) ) liefert zusätzliche Informationen, die Sie bei der Verwendung von {{site.data.keyword.aios_short}} unterstützen.
