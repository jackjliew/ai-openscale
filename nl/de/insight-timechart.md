---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen
{: #it-ov}

Die Überwachungsdaten für die einzelnen Bereitstellungen werden in einem Zeitreihendiagramm dargestellt. In diesem Diagramm werden Fairness, die durchschnittliche Zahl der Anforderungen pro Minute und die Genauigkeit über den Zeitraum der letzten sieben Tage überwacht.
{: shortdesc}

## Daten für eine Bereitstellung anzeigen
{: #it-vdep}

Wählen Sie im Dashboard eine Bereitstellung aus, damit Überwachungsdaten für diese Bereitstellung angezeigt werden. Im oberen Bereich des Diagramms mit den Überwachungsdaten werden Informationen zu dem bereitgestellten Modell angezeigt, u. a. auch, wann das Modell auf Fairness und Genauigkeit hin ausgewertet wurde und wann die nächste Auswertung erfolgt.

![Zeitreihendiagramm](images/insight-time-chart.png)

Da die Algorithmusprüfungen nur in Intervallen von je einer Stunde ausgeführt werden, sind außerdem Schaltflächen vorhanden, die Ihnen die bedarfsgesteuerte Prüfung von Fairness und Genauigkeit ermöglichen. Wenn Sie nicht ausreichend Datensätze für Nutzdaten (Fairness) oder für Rückmeldedaten (Genauigkeit) zur Verfügung gestellt haben, wird beispielsweise die folgende Nachricht angezeigt:

![Schaltfläche 'Genauigkeit'](images/accuracy-button.png)

Verschieben Sie die Markierung auf dem Diagramm, um Statistiken für eine einzelne Stunde anzuzeigen. In diesem Beispiel wurde als Zeitpunkt 13:00 Uhr (CST, Central Standard Time) am 18. September ausgewählt, woraus die folgenden Statistiken hervorgehen:

![Detailansicht des Zeitreihendiagramms](images/insight-time-detail.png)

- ***Fairness***: Für zwei der drei Merkmale für Fairness, nämlich 'Fahrzeugwert' und 'Ortsnetzkennzahl', wurden die für die Genehmigung festgelegten Schwellenwerte erreicht. Das dritte Fairnessmerkmal - 'Alter' - wurde als verzerrt gekennzeichnet. Außerdem wird die Anzahl der erwarteten Ergebnisse, in diesem Fall Prozentsätze für 'Bewilligt' bzw. 'Abgelehnt', für eine einzelne Bevölkerungsgruppe in den auf Fairness überwachten Merkmalen angezeigt.
- ***Genauigkeit***: Die Genauigkeitsmetrik betrug durchschnittlich 78 %.
- ***Durchschnittliche Anf./Min.***: Im Durchschnitt wurden zwischen 13:00 und 14:00 Uhr (CST) 300 Datensätze pro Minute verarbeitet. Der Durchsatz wird minütlich berechnet und im Diagramm wird sein Durchschnittswert über den Verlauf der Stunde angezeigt.

## Visualisierung von Daten für eine bestimmte Uhrzeit anzeigen
{: #it-vdet}

Wenn die Detailinformationen angezeigt werden sollen, die sich hinter einer bestimmten Statistik für Fairness verbergen, klicken Sie für die ausgewählte Uhrzeit auf den Link **Details anzeigen**.

Es wird eine Visualisierung der Datenpunkte für ein überwachtes Merkmal zum ausgewählten Zeitpunkt geöffnet. Es wird das obige Beispiel des Merkmals 'Alter', das als verzerrt gekennzeichnet wurde, dargestellt.

Beachten Sie die drei Filter im oberen Bereich der Seite (Merkmal, Datum und Uhrzeit), die Ihnen die Auswahl eines anderen Merkmals oder eines anderen Datums bzw. einer anderen Uhrzeit zwecks Überprüfung von Details ermöglichen.

![Zeitreihendiagramm](images/insight-data-detail.png)

### Diagramm interpretieren
{: #it-intp}

Das Diagramm zeigt mehrere Dinge an:

- Es wird angezeigt, für welchen Anteil der Bevölkerung eine Verzerrung vorliegt (nämlich für Kunden im Alter von 18 bis 23 Jahren). Das Diagramm zeigt auch den Prozentsatz des erwarteten Ergebnisses (52 %) für diesen Bevölkerungsanteil an.

- Das Diagramm zeigt den Prozentsatz des erwarteten Ergebnisses (70 %) für den als Referenzgruppe verwendeten Bevölkerungsanteil an. Dies ist der Durchschnitt der erwarteten Ergebnisse über alle Referenzbevölkerungsgruppen hinweg.

- Die Grafik weist auf das Vorhandensein von Verzerrungen hin, da das Verhältnis des Prozentsatzes der erwarteten Ergebnisse für den Bevölkerungsanteil im Alter von 18 bis 23 Jahren zum Prozentsatz der erwarteten Ergebnisse für die Referenzbevölkerungsgruppe unter dem Schwellenwert liegt. Anders ausgedrückt ergibt die Berechnung 0,52/0,7 = 0,74 einen Wert, der unter dem Schwellenwert von 0,8 liegt.

- Das Diagramm zeigt auch die Verteilung der Referenz- und der Überwachungswerte für jeden einzelnen Wert des Attributs in den Daten aus der Nutzdatentabelle, die analysiert wurde, um Verzerrungen festzustellen. Anders ausgedrückt trifft Folgendes zu: Wenn der Erkennungslogarithmus für Verzerrung die letzten 1.790 Datensätze aus der Nutzdatentabelle analysiert hat, galt für 120 dieser Datensätze ein Kundenalter von 18 bis 23 Jahren, und aus dieser Verteilung stellt das Balkendiagramm die Ergebnisse `Bewilligt` und `Abgelehnt` dar. Die Verteilung der Nutzdaten im Bestand wird für jeden einzelnen Wert des Fairnessattributs angezeigt und es werden sogar Referenzwerte angezeigt. Mit diesen Informationen kann eine Korrelation zwischen der Verzerrung und der vom Modell empfangenen Menge an Daten hergestellt werden.

- Das Diagramm zeigt außerdem, dass für den Bevölkerungsanteil im Alter zwischen 31 und 35 Jahren 91 % der erwarteten Ergebnisse eingetroffen sind. Dies bedeutet diese die Quelle für die Verzerrung ist, was heißt, dass Daten in dieser Gruppe die Ergebnisse verfälscht haben zu einem Anstieg des Prozentsatzes der erwarteten Ergebnisse bei der Referenzklasse geführt haben. Anhand dieser Informationen können die Teile der Daten aufgedeckt werden, die dann beim Retraining des Modells durch einen geringeren Stichprobenanteil repräsentiert werden können.

- Als weiteren wichtigen Aspekt zeigt das Diagramm den Namen der Tabelle mit den Daten an, die für die manuelle Kennzeichnung angegeben wurde. Wann immer der Algorithmus Verzerrungen in einem Modell erkennt, identifiziert und gibt er auch die Datenpunkte an, dann zur manuellen Kennzeichnung durch den Menschen gesendet werden können. Diese manuell beschrifteten Daten können dann zusammen mit den ursprünglichen Trainingsdaten zum erneuten Trainieren (Retraining) des Modells verwendet werden. Dieses erneut trainierte Modell weist die Verzerrung wahrscheinlich nicht auf. Die Tabelle für die manuelle Kennzeichnung ist in der Datenbank enthalten, die der {{site.data.keyword.aios_short}}-Instanz zugeordnet ist.

## Laufzeit- und Trainingsdaten
{: #it-rtsw}

Der Schieberegler 'Laufzeitdaten/Trainingsdaten' ermöglicht Ihnen, zwischen der Anzeige der Unterschiede Ihres trainierten Modells und der zur Laufzeit erfassten Daten, die eine Verzerrungswarnung auslösen, hin- und herzuschalten. Weitere Informationen zu den Trainingsdaten finden Sie unter [Warum muss {{site.data.keyword.aios_short}} auf meine Trainingsdaten zugreifen?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Schieberegler zum Umschalten zwischen Laufzeit und Training](images/runtime_train_data.png)

## Transaktionen anzeigen
{: #it-tra}

Diese Option ermöglicht Ihnen, die einzelnen Transaktionen anzuzeigen, die zu einer Verzerrung beigetragen haben, wenn Sie auf die Schaltfläche **Transaktionen anzeigen** klicken.

![Transaktionen anzeigen](images/view_transactions.png)

Es wird eine Liste der Transaktionen aufgeführt, bei denen die Bereitstellung verzerrt agiert hat. Klicken Sie für Transaktions-IDs Ihrer Wahl auf den Link **Erklären**, damit in der Registerkarte 'Erklärbarkeit' Details zu der jeweiligen Transaktion angegeben werden. Weitere Informationen hierzu enthält der Abschnitt [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

Wählen Sie die Sicht **Alle Transaktionen** aus, damit alle Transaktionen für das ausgewählte Merkmal (in diesem Beispiel 'ALTER') und den ausgewählten Zeitpunkt (in diesem Beispiel '15. September 2018 13:00') angezeigt werden:

![Auflistung aller Transaktionen](images/transaction_list1.png)

Wählen Sie die Ansicht **Verzerrte Transaktionen** aus, damit nur die Untergruppe der Transaktionen angezeigt wird, bei denen eine Verzerrung der Ergebnisse festgestellt wurde. Jede verzerrte Transaktion wird mit einer ähnlichen, aber geringfügig abgewandelten (durch Perturbation gestörten) Transaktion verglichen, die aufzeigt, wie die Änderung des Wertes für das überwachte Merkmal (ALTER) ein günstiges Ergebnis für die verzerrte Transaktion nach sich zieht:

![Liste der verzerrten Transaktionen](images/transaction_list2.png)

## Produktionsmodell und verzerrungsbereinigtes Modell
{: #it-prdb}

Anhand dieser beiden Registerkarten können Sie zwischen Ihrem Produktionsmodell und einem von {{site.data.keyword.aios_short}} erstellten verzerrungsbereinigten Modell hin- und herschalten. Genaueres hierzu enthält der Abschnitt [Funktionsweise der Verzerrungsbereinigung verstehen](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

![Schieberegler zum Hin- und Herschalten zwischen Laufzeit und Training](images/bias-debias.png)

Bei Auswahl der Registerkarte **Verzerrungsbereinigtes Modell** werden die Änderungen im verzerrungsbereinigten Modell im Vergleich zum Produktionsmodell angezeigt. Im vorliegenden Beispiel wurde für Fairness im Modell eine Zunahme von 74 % auf 93 % verzeichnet, während die Genauigkeit lediglich um 1 % fiel. Das Diagramm spiegelt auch den verbesserten Ergebnisstatus für Gruppen im Alter von 18 bis 23 Jahren wider.

![Schieberegler zum Hin- und Herschalten zwischen Laufzeit und Training](images/insight-data-detail2.png)

### Optionen für die Verzerrungsbereinigung
{: #it-dbo}

- *Passive Verzerrungsbereinigung*: {{site.data.keyword.aios_short}} eine Verzerrungsprüfung vornimmt, führt es auch eine Verzerrungsbereinigung der Daten durch, indem es das Verhalten des Modells analysiert und die Daten aufdeckt, bei denen das Modell in verzerrter Weise handelt.

  {{site.data.keyword.aios_short}} erstellt dann ein Machine Learning-Modell, um vorherzusagen, ob das Modell an einem bestimmten neuen Datenpunkt wahrscheinlich auf verzerrte Weise reagieren wird. {{site.data.keyword.aios_short}} analysiert dann die Daten, die vom Modell in Stundenintervallen empfangen werden, und sucht die Datenpunkte, an denen {{site.data.keyword.aios_short}} meint, ein verzerrtes Verhalten feststellen zu können. Für derartige Datenpunkte wird der Wert des Attributs 'Fairness' durch Perturbation (Störung) von 'Minderheit' in 'Mehrheit' geändert und die durch Perturbation gestörten Daten werden zur Vorhersage an das ursprüngliche Modell gesendet. Diese Vorhersage des Originalmodells wird als verzerrungsbereinigte Ausgabe verwendet.

  {{site.data.keyword.aios_short}} führt diese Verzerrungsbereinigung stündlich für alle Daten durch, die in der letzten Stunde vom Modell empfangen wurden. Es berechnet auch die Fairness für die verzerrungsbereinigte Ausgabe und zeigt sie auf der Registerkarte **Verzerrungsbereinigtes Modell** an.

- *Aktive Verzerrungsbereinigung*: Bei der aktiven Verzerrungsbereinigung können Sie Gebrauch von einem REST-API-Endpunkt für Verzerrungsbereinigung Ihrer Anwendung machen. Dieser REST-API-Endpunkt ruft Ihr Modell intern auf und prüft dessen Verhalten.

  Wenn {{site.data.keyword.aios_short}} der Auffassung ist, dass das Modell verzerrt handelt, führt es die Perturbation (Störung) der Daten wie oben beschrieben durch und schickt diese dann an das ursprüngliche Modell zurück. Die Ausgabe des ursprünglichen Modells für die durch Perturbation gestörten Daten wird als die verzerrungsbereinigte Vorhersage zurückgegeben. Wenn {{site.data.keyword.aios_short}} feststellt, dass das ursprüngliche Modell nicht verzerrt handelt, gibt {{site.data.keyword.aios_short}} die Vorhersage des ursprünglichen Modells als verzerrungsbereinigte Vorhersage zurück. Durch die Verwendung dieses REST-API-Endpunkts können Sie also sicherstellen, dass Ihre Anwendung keine Entscheidungen trifft, die auf einer verzerrten Ausgabe Ihrer Modelle basieren.

Wählen Sie den Link **Verzerrungsbereinigten Scoring-Endpunkt anzeigen** aus, um Ihren verzerrungsbereinigten REST-API-Endpunkt zu ermitteln.

![Verzerrungsbereinigter API-Endpunkt](images/insight-debias-api.png)
