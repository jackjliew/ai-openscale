---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen
{: #it-ov}

Die Überwachungsdaten für die einzelnen Bereitstellungen werden in einem Zeitreihendiagramm dargestellt. In diesem Diagramm werden Fairness, die durchschnittliche Zahl der Anforderungen pro Minute und die Genauigkeit über den Zeitraum der letzten sieben Tage überwacht.
{: shortdesc}

## Daten für eine Bereitstellung anzeigen
{: #it-vdep}

Wählen Sie im Dashboard eine Bereitstellung aus, damit Überwachungsdaten für diese Bereitstellung angezeigt werden. In der Überschrift werden Informationen zum bereitgestellten Modell angezeigt, z. B. die Felder für **Modell-ID** und **Erstellungsdatum**.

![Zeitreihendiagramm](images/insight-time-chart.png)

Da die Algorithmusprüfungen nur jede Stunde ausgeführt werden, sind außerdem Links vorhanden, mit denen Sie Fairness und Qualität bei Bedarf jederzeit prüfen können. In der Anzeige **Zeitplan** können Sie auf die folgenden Links klicken, um eine sofortige Überprüfung Ihrer Daten vorzunehmen:

![Schaltfläche für Fairnessprüfung](images/wos-fairness-button.png)


![Schaltfläche für Qualitätsprüfung](images/wos-quality-button.png)

Klicken Sie als Nächstes auf das Diagramm und verschieben Sie die Markierung auf dem Diagramm, um Statistiken für eine einzelne Stunde anzuzeigen:

![Detailansicht des Zeitreihendiagramms](images/wos-insight-time-detail.png)

- ***Fairness***: Zwei Fairnessmerkmale (Geschlecht und Alter) haben die für die Genehmigung festgelegten Schwellenwerte eingehalten.
- ***Qualität***: Die Metrik **Fläche unterhalb der ROC-Kurve** zeigt einen Alert an, da dieser Wert gegen den konfigurierten Schwellenwert verstößt.
- ***Durchschnittliche Anf./Min.***: Klicken Sie auf die Metrik **Durchsatz**, um die Anzahl der Datensätze anzuzeigen, die pro Minute verarbeitet wurden. Der Durchsatz wird minütlich berechnet und im Diagramm wird sein Durchschnittswert über den Verlauf der Stunde angezeigt.

## Visualisierung von Daten für eine bestimmte Uhrzeit anzeigen
{: #it-vdet}

Wenn Sie Details zu einer bestimmten Fairnessstatistik anzeigen möchten, klicken Sie auf das Diagramm für eine bestimmte Zeit.

Es wird eine Visualisierung der Datenpunkte für ein überwachtes Merkmal zum ausgewählten Zeitpunkt geöffnet. Im folgenden Beispiel wird das Merkmal für Alter angezeigt.

Beachten Sie die drei Filter im oberen Bereich der Seite (Merkmal, Datum und Uhrzeit), die Ihnen die Auswahl eines anderen Merkmals oder eines anderen Datums bzw. einer anderen Uhrzeit zwecks Überprüfung von Details ermöglichen.

![Zeitreihendiagramm](images/wos-insight-data-detail.png)

### Diagramm interpretieren
{: #it-intp}

Das Diagramm zeigt mehrere Dinge an:

- Es wird angezeigt, für welchen Anteil der Bevölkerung eine Verzerrung vorliegt (nämlich für Kunden im Alter von 18 bis 23 Jahren). Im Diagramm ist auch den Prozentsatz des erwarteten Ergebnisses für diesen Bevölkerungsanteil zu sehen.

- Das Diagramm zeigt den Prozentsatz des erwarteten Ergebnisses (70 %) für den als Referenzgruppe verwendeten Bevölkerungsanteil an. Dies ist der Durchschnitt der erwarteten Ergebnisse über alle Referenzbevölkerungsgruppen hinweg.

- Aus dem Diagramm geht auch hervor, dass eine Verzerrung vorliegt, da das Verhältnis des Prozentsatzes der erwarteten Ergebnisse für den Bevölkerungsanteil im Alter von 18 bis 23 Jahren zum Prozentsatz der erwarteten Ergebnisse für die Referenzbevölkerungsgruppe über dem Schwellenwert liegt. Anders ausgedrückt ergibt die Berechnung 0,52/0,7 = 0,74 einen Wert, der unter dem Schwellenwert von 0,8 liegt.

- Das Diagramm zeigt auch die Verteilung der Referenz- und der Überwachungswerte für jeden einzelnen Wert des Attributs in den Daten aus der Nutzdatentabelle, die analysiert wurde, um Verzerrungen festzustellen. Anders ausgedrückt trifft Folgendes zu: Wenn der Erkennungslogarithmus für Verzerrung die letzten 1.790 Datensätze aus der Nutzdatentabelle analysiert hat, galt für 120 dieser Datensätze ein Kundenalter von 18 bis 23 Jahren, und aus dieser Verteilung stellt das Balkendiagramm die Ergebnisse `Bewilligt` und `Abgelehnt` dar. Die Verteilung der Nutzdaten im Bestand wird für jeden einzelnen Wert des Fairnessattributs angezeigt und es werden sogar Referenzwerte angezeigt. Mit diesen Informationen kann eine Korrelation zwischen der Verzerrung und der vom Modell empfangenen Menge an Daten hergestellt werden.

- Das Diagramm zeigt außerdem, dass für den Bevölkerungsanteil im Alter zwischen 31 und 35 Jahren 91 % der erwarteten Ergebnisse eingetroffen sind. Dies bedeutet diese die Quelle für die Verzerrung ist, was heißt, dass Daten in dieser Gruppe die Ergebnisse verfälscht haben zu einem Anstieg des Prozentsatzes der erwarteten Ergebnisse bei der Referenzklasse geführt haben. Anhand dieser Informationen können die Teile der Daten aufgedeckt werden, die dann beim Retraining des Modells durch einen geringeren Stichprobenanteil repräsentiert werden können.

- Als weiteren wichtigen Aspekt zeigt das Diagramm den Namen der Tabelle mit den Daten an, die für die manuelle Kennzeichnung angegeben wurde. Wann immer der Algorithmus Verzerrungen in einem Modell erkennt, identifiziert und gibt er auch die Datenpunkte an, dann zur manuellen Kennzeichnung durch den Menschen gesendet werden können. Diese manuell beschrifteten Daten können dann zusammen mit den ursprünglichen Trainingsdaten zum erneuten Trainieren (Retraining) des Modells verwendet werden. Dieses erneut trainierte Modell weist die Verzerrung wahrscheinlich nicht auf. Die Tabelle für die manuelle Kennzeichnung ist in der Datenbank enthalten, die der {{site.data.keyword.aios_short}}-Instanz zugeordnet ist.

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

{{site.data.keyword.aios_short}} verwendet zwei Typen von Verzerrungsbereinigung: passive und aktive Bereinigung. Bei der passiven Verzerrungsbereinigung erfahren Sie, welche Verzerrung vorlag, während die aktive Verzerrungsbereinigung durch eine Echtzeitänderung des Modells für die aktuelle Anwendung verhindert, dass sich die Verzerrung fortsetzt.

- *Passive Verzerrungsbereinigung* - Passive Verzerrungsbereinigung wird von OpenScale automatisch jede Stunde ausgeführt. Diese Bereinigung wird als passiv bezeichnet, da sie ohne Benutzereingriff erfolgt. Im Rahmen der Verzerrungsprüfung führt {{site.data.keyword.aios_short}} auch eine Verzerrungsbereinigung der Daten durch, indem das Verhalten des Modells analysiert und die Daten ermittelt werden, bei denen das Modell eine Verzerrung aufweist.

  {{site.data.keyword.aios_short}} erstellt dann ein Machine Learning-Modell, um vorherzusagen, ob das Modell an einem bestimmten neuen Datenpunkt wahrscheinlich auf verzerrte Weise reagieren wird. {{site.data.keyword.aios_short}} analysiert dann die Daten, die vom Modell in Stundenintervallen empfangen werden, und sucht die Datenpunkte, an denen {{site.data.keyword.aios_short}} meint, ein verzerrtes Verhalten feststellen zu können. Für derartige Datenpunkte wird der Wert des Attributs 'Fairness' durch Perturbation (Störung) von 'Minderheit' in 'Mehrheit' geändert und die durch Perturbation gestörten Daten werden zur Vorhersage an das ursprüngliche Modell gesendet. Diese Vorhersage des Originalmodells wird als verzerrungsbereinigte Ausgabe verwendet.

  {{site.data.keyword.aios_short}} führt diese Verzerrungsbereinigung stündlich für alle Daten durch, die in der letzten Stunde vom Modell empfangen wurden. Es berechnet auch die Fairness für die verzerrungsbereinigte Ausgabe und zeigt sie auf der Registerkarte **Verzerrungsbereinigtes Modell** an.

- *Aktive Verzerrungsbereinigung* - Die aktive Verzerrungsbereinigung stellt eine Möglichkeit dar, verzerrungsbereinigte Ergebnisse über den REST-API-Endpunkt anzufordern und in Ihre Anwendung aufzunehmen. Sie weisen {{site.data.keyword.aios_short}} aktiv an, eine Verzerrungsbereinigung durchzuführen und das Modell zu ändern, damit Sie Ihre Anwendung ohne Verzerrung ausführen können. Bei der aktiven Verzerrungsbereinigung können Sie von Ihrer Anwendung aus einen REST-API-Endpunkt für Verzerrungsbereinigung einsetzen. Dieser REST-API-Endpunkt ruft Ihr Modell intern auf und prüft dessen Verhalten.

  Wenn {{site.data.keyword.aios_short}} erkennt, dass das Modell ein verzerrtes Verhalten aufweist, verändert es die Daten wie zuvor erwähnt durch Perturbation und sendet sie dann an das ursprüngliche Modell zurück. Die Ausgabe des ursprünglichen Modells für die durch Perturbation gestörten Daten wird als die verzerrungsbereinigte Vorhersage zurückgegeben. Wenn {{site.data.keyword.aios_short}} feststellt, dass das ursprüngliche Modell nicht verzerrt handelt, gibt {{site.data.keyword.aios_short}} die Vorhersage des ursprünglichen Modells als verzerrungsbereinigte Vorhersage zurück. Durch die Verwendung dieses REST-API-Endpunkts können Sie also sicherstellen, dass Ihre Anwendung keine Entscheidungen trifft, die auf einer verzerrten Ausgabe Ihrer Modelle basieren.

Wählen Sie den Link **Verzerrungsbereinigten Scoring-Endpunkt anzeigen** aus, um Ihren verzerrungsbereinigten REST-API-Endpunkt zu ermitteln.

![Verzerrungsbereinigter API-Endpunkt](images/insight-debias-api.png)
