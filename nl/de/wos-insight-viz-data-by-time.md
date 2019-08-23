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

# Visualisierung von Daten für eine bestimmte Stunde anzeigen
{: #it-vdet}

Wenn Sie Details zu einer bestimmten Fairnessstatistik anzeigen möchten, klicken Sie auf das Diagramm für eine bestimmte Zeit. Es wird eine Visualisierung der Datenpunkte für ein überwachtes Merkmal zum ausgewählten Zeitpunkt geöffnet. Im folgenden Beispiel wird das Merkmal für Alter angezeigt.
{: shortdesc}

Beachten Sie die drei Filter im oberen Bereich der Seite (Merkmal, Datum und Uhrzeit), die Ihnen die Auswahl eines anderen Merkmals oder eines anderen Datums bzw. einer anderen Uhrzeit zwecks Überprüfung von Details ermöglichen.

![Anzeige eines Zeitreihendiagramms mit Spalten für Nutzdaten und durch Perturbation gestörte Daten zu Alter und Anzahl der günstigen Ergebnisse](images/wos-insight-data-detail.png)

## Diagramm interpretieren
{: #it-intp}

Das Diagramm zeigt mehrere Dinge an:

- Es wird angezeigt, für welchen Anteil der Bevölkerung eine Verzerrung vorliegt (nämlich für Kunden im Alter von 18 bis 23 Jahren). Im Diagramm ist auch den Prozentsatz des erwarteten Ergebnisses für diesen Bevölkerungsanteil zu sehen.

- Das Diagramm zeigt den Prozentsatz des erwarteten Ergebnisses (70 %) für den als Referenzgruppe verwendeten Bevölkerungsanteil an. Dies ist der Durchschnitt der erwarteten Ergebnisse über alle Referenzbevölkerungsgruppen hinweg.

- Aus dem Diagramm geht auch hervor, dass eine Verzerrung vorliegt, da das Verhältnis des Prozentsatzes der erwarteten Ergebnisse für den Bevölkerungsanteil im Alter von 18 bis 23 Jahren zum Prozentsatz der erwarteten Ergebnisse für die Referenzbevölkerungsgruppe über dem Schwellenwert liegt. Anders ausgedrückt ergibt die Berechnung 0,52/0,7 = 0,74 einen Wert, der unter dem Schwellenwert von 0,8 liegt.

- Das Diagramm zeigt auch die Verteilung der Referenz- und der Überwachungswerte für jeden einzelnen Wert des Attributs in den Daten aus der Nutzdatentabelle, die analysiert wurde, um Verzerrungen festzustellen. Anders ausgedrückt trifft Folgendes zu: Wenn der Erkennungslogarithmus für Verzerrung die letzten 1.790 Datensätze aus der Nutzdatentabelle analysiert hat, galt für 120 dieser Datensätze ein Kundenalter von 18 bis 23 Jahren, und aus dieser Verteilung stellt das Balkendiagramm die Ergebnisse `Bewilligt` und `Abgelehnt` dar. Die Verteilung der Nutzdaten im Bestand wird für jeden einzelnen Wert des Fairnessattributs angezeigt und es werden sogar Referenzwerte angezeigt. Mit diesen Informationen kann eine Korrelation zwischen der Verzerrung und der vom Modell empfangenen Menge an Daten hergestellt werden.

- Das Diagramm zeigt außerdem, dass für den Bevölkerungsanteil im Alter zwischen 31 und 35 Jahren 91 % der erwarteten Ergebnisse eingetroffen sind. Dies bedeutet diese die Quelle für die Verzerrung ist, was heißt, dass Daten in dieser Gruppe die Ergebnisse verfälscht haben zu einem Anstieg des Prozentsatzes der erwarteten Ergebnisse bei der Referenzklasse geführt haben. Anhand dieser Informationen können die Teile der Daten aufgedeckt werden, die dann beim Retraining des Modells durch einen geringeren Stichprobenanteil repräsentiert werden können.

- Als weiteren wichtigen Aspekt zeigt das Diagramm den Namen der Tabelle mit den Daten an, die für die manuelle Kennzeichnung angegeben wurde. Wann immer der Algorithmus Verzerrungen in einem Modell erkennt, identifiziert und gibt er auch die Datenpunkte an, dann zur manuellen Kennzeichnung durch den Menschen gesendet werden können. Diese manuell beschrifteten Daten können dann zusammen mit den ursprünglichen Trainingsdaten zum erneuten Trainieren (Retraining) des Modells verwendet werden. Dieses erneut trainierte Modell weist die Verzerrung wahrscheinlich nicht auf. Die Tabelle für die manuelle Kennzeichnung ist in der Datenbank enthalten, die der {{site.data.keyword.aios_short}}-Instanz zugeordnet ist.
