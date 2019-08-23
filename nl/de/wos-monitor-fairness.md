---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Fairnessüberwachung konfigurieren
{: #mf-monitor}

In {{site.data.keyword.aios_full}} prüft die Fairnessüberwachung die Bereitstellung auf Verzerrungen, um faire Ergebnisse in unterschiedlichen Bevölkerungsgruppen sicherzustellen.
{: shortdesc}

## Schritte
{: #mf-config}

Klicken Sie auf der Registerkarte **Fairness** auf der Seite **Was ist Fairness?** auf **Beginnen**, um den Konfigurationsprozess zu starten.

![Seite 'Was ist Fairness?'](images/fair-what-is.png)

Bei diesem Prozess wird das Modell von {{site.data.keyword.aios_full}} analysiert und es werden an dem logischsten Ergebnis ausgerichtete Empfehlungen erstellt. Auf den nachfolgenden Seiten der Registerkarte **Fairness** müssen Sie die folgenden Aufgaben ausführen:

1. Wählen Sie die zu überwachenden Merkmale aus. Es werden nur Merkmale unterstützt, die 'kategorial', 'numerisch' (Ganzzahl), Gleitkomma oder Double als Datentyp aufweisen. Merkmale mit anderen Datentypen werden nicht unterstützt.

1. Geben Sie Referenzgruppen und überwachte Gruppen an.

   Für jedes Merkmal müssen bestimmte Anforderungen konfiguriert werden. Wenn Sie z. B. `Alter` als zu überwachendes Merkmal auswählen, müssen Sie die Altersbereiche für eine **Referenzgruppe** und eine **überwachte Gruppe** definieren, indem Sie in den einzelnen Gruppen Werte eingeben.

1.  Legen Sie den Alertschwellenwert für Fairness für das Merkmal fest.

    Eine Fairnessschwellenwert wird verwendet, um eine annehmbare Differenz zwischen dem Prozentsatz der günstigen Ergebnisse für die überwachte Gruppe im Vergleich zu dem Prozentsatz der günstigen Ergebnisse für die Referenzgruppe festzulegen.

    Betrachten Sie ein Modell, das vorhersagt, wer ein Darlehen erhalten soll (`Günstiges Ergebnis=Darlehen bewilligt`) und wer nicht (`Ungünstiges Ergebnis=Darlehen abgelehnt`). Außerdem ist für das Alter der Bereich `[18,25]` für die überwachte Gruppe und `[26,100]` für die Referenzgruppe festgelegt. Wenn der Erkennungsalgorithmus für Verzerrung bei der Ausführung feststellt, dass der Prozentsatz der günstigen Ergebnisse bei Menschen der Altersgruppe `[18,25]` in den letzten `N` Datensätzen zuzüglich der durch Perturbation gestörten Daten einen Wert von `50 %` aufweist, während der Prozentsatz der günstigen Ergebnisse bei Menschen der Altersgruppe `[26,100]` bei `70 %` liegt, wird für die Fairness der Wert 50*100/70 = 71,42 berechnet.

    Falls als Schwellenwert für Fairness der Wert 80 % festgelegt wurde, wird das Modell vom Algorithmus als verzerrt markiert, weil der berechnete Fairnesswert über dem Schwellenwert liegt. Wenn jedoch ein Wert von 70 % als Schwellenwert festgelegt ist, wird das Modell nicht als verzerrt gemeldet.

     Bei den Werten, die Sie in diesen Anzeigen eingeben, sollte es sich um die Werte handeln, die an den Scoring-Endpunkt des Modells gesendet werden (und die somit zu der Nutzdatentabelle hinzugefügt werden). Wenn die Daten vor dem Senden an den Scoring-Endpunkt bearbeitet werden, geben Sie die bearbeiteten Werte ein. Wenn die ursprünglichen Daten die Werte `Männlich` und `Weiblich` für das Merkmal *Geschlecht* enthielten und diese dann so bearbeitet wurden, dass `M` und `W` an den Scoring-Endpunkt gesendet wurde, geben Sie in dieser Anzeige die Werte `M` und `W` ein.

1.  Geben Sie Werte an, die ein günstiges Ergebnis für das Modell darstellen. Diese Werte werden aus der Spalte `Kennzeichnung` in den [Trainingsdaten](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) abgeleitet, sofern das Modellausgabeschema eine Zuordnungsspalte enthält. Bei {{site.data.keyword.pm_full}} weist die Spalte `prediction` stets einen Wert des Typs double auf. Anhand der Zuordnungsspalte wird angegeben, wie dieser Wert der `Vorhersage` der Klassenbezeichnung zugeordnet werden soll.

    Wenn `Vorhersage` den Wert `1.0` hat, könnte die Zuordnungsspalte den Wert `Darlehen abgelehnt` aufweisen. Dies bedeutet, dass die Vorhersage des Modells `Darlehen abgelehnt` lautet. Wenn das Modellausgabeschema eine Zuordnungsspalte enthält, geben Sie anhand der in der Zuordnungsspalte enthaltenen Elemente die günstigen bzw. ungünstigen Werte an.

    Wenn im Modellausgabeschema jedoch keine Zuordnungsspalte vorhanden ist, müssen die günstigen und die ungünstigen Werte anhand des Werts der Spalte `Vorhersage` angegeben werden (`0.0`, `1.0` usw.).

1.  Legen Sie zum Schluss einen Mindeststichprobenumfang fest, um zu verhindern, dass die Messung der Fairness bereits erfolgt, noch bevor eine Mindestanzahl von Datensätzen im Auswertungsdatensatz verfügbar ist. Dadurch wird sichergestellt, dass die Ergebnisse nicht etwa durch einen zu kleinen Stichprobenumfang verfälscht werden. Bei jeder Durchführung der Verzerrungsprüfung wird dabei jeweils die Mindeststichprobengröße verwendet, um die Anzahl von Datensätzen zu bestimmen, für die sie die Verzerrungsberechnung durchführt.

    Zur Überprüfung wird eine Zusammenfassung der von Ihnen getroffenen Auswahl angezeigt. Falls Sie Änderungen vornehmen möchten, klicken Sie für den betreffenden Abschnitt auf den Link **Bearbeiten**. Klicken Sie andernfalls auf **Speichern**.

    Sie können auch auf **Weiteres Merkmal hinzufügen** klicken, um zu der Anzeige für die Merkmalauswahl zurückzukehren und weitere Merkmale zur Fairnessüberwachung hinzuzufügen, z. B. `Stadt`, `Postleitzahl` oder `Kontostand`.

### Informationen zur Funktionsweise der Verzerrungsbereinigung
{: #mf-debias}

Klicken Sie auf die Schaltfläche **Endpunkt für Verzerrungsbereinigung**, um den Endpunkt für Verzerrungsbereinigung zu überprüfen. Sie können dann den Endpunkt in verschiedenen Formaten wie cURL, Java oder Python anzeigen und kopieren. 

Der verzerrungsbereinigte Scoring-Endpunkt kann genau so wie der normale Scoring-Endpunkt Ihres bereitgestellten Modells verwendet werden. Neben der Antwort Ihres bereitgestellten Modells werden auch zwei zusätzliche Spalten namens `debiased_prediction` und `debiased_probability` zurückgegeben.

- Die Spalte `debiased_prediction` enthält den verzerrungsbereinigten Vorhersagewert. Bei Verwendung von {{site.data.keyword.pm_full}} ist dies eine codierte Darstellung der Vorhersage. Beispiel: Wenn die Modellvorhersage entweder 'Darlehen bewilligt' oder 'Darlehen abgelehnt' lautet, können diese beiden Werte von {{site.data.keyword.pm_full}} als '0.0' bzw. '1.0' codiert sein. Die Spalte `debiased_prediction` enthält eine derartig codierte Darstellung der verzerrungsbereinigten Vorhersage.

- Die Spalte `debiased_probability` hingegen stellt die Wahrscheinlichkeit der verzerrungsbereinigten Vorhersage dar. Hierbei handelt es sich um einen Bereich aus Werten des Typs double, bei dem jeder Wert die Wahrscheinlichkeit der verzerrungsbereinigten Vorhersage darstellt, die zu einer der Vorhersageklassen gehört.

Eine weitere Spalte namens `debiased_decoded_target` wird ebenfalls zurückgegeben, und zwar für den Fall, dass sich eine Spalte in Ihrem Ausgabeschema befindet, die eine Spalte mit `modeling-role` als `decoded-target` enthält.

- Die Spalte `debiased_decoded_target` enthält die Zeichenfolgedarstellung der verzerrungsbereinigten Vorhersage. Während der Vorhersagewert im vorherigen Beispiel entweder '0.0' oder '1.0' lautete, enthält `debiased_decoded_target` entweder 'Darlehen bewilligt' oder 'Darlehen abgelehnt'.

Im Idealfall rufen Sie diesen Endpunkt direkt aus der Produktionsanwendung auf, anstatt den Scoring-Endpunkt direkt im Modell aufzurufen, das in der Modell-Server-Engine bereitgestellt wird ({{site.data.keyword.pm_full}}, Amazon SageMaker, Microsoft Azure ML Studio usw.). Auf diese Weise speichert {{site.data.keyword.aios_short}} auch die `verzerrungsbereinigten` Werte in der Nutzdatenprotokollierungstabelle Ihrer Modellbereitstellung. Dann wäre die gesamte Bewertung, die über diesen Endpunkt erfolgt, automatisch verzerrungsbereinigt.

Da dieser Endpunkt die Verzerrung zur Laufzeit bearbeitet, wird er weiterhin Hintergrundprüfungen für die neuesten Bewertungsdaten aus der Nutzdatenprotokollierungstabelle durchführen und das Modell für Verzerrungsminimierung, mit dem Verzerrungsbereinigung der gesendeten Scoring-Anforderungen durchgeführt wird, weiterhin aktualisieren. Auf diese Weise ist {{site.data.keyword.aios_short}} mit den zuletzt ankommenden Daten und mit seinem Verhalten zur Erkennung und Bereinigung der Verzerrung stets auf dem neuesten Stand.

{{site.data.keyword.aios_short}} verwendet zum Schluss einen Schwellenwert, um zu entscheiden, ob bzw. dass Daten nun annehmbar sind und als unverzerrt gelten. Für diesen Schwellenwert wird der niedrigste Wert der Schwellenwerte verwendet, die in der Fairnessüberwachung für alle konfigurierten Fairnessattribute festgelegt sind.

## Weitere Schritte
{: #mf-next}

Klicken Sie auf die Registerkarte **Drift** und dann auf **Beginnen**, um mit der Konfiguration der Überwachung fortzufahren. Weitere Informationen hierzu enthält der Abschnitt [Drifterkennungsüberwachung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
