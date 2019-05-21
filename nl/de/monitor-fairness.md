---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: fairness, fairness monitor

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

# Fairness
{: #mf-monitor}

Fairness überwacht Ihre Bereitstellung auf Verzerrungen, um faire Ergebnisse in unterschiedlichen Bevölkerungsgruppen sicherzustellen.
{: shortdesc}

## Fairness verstehen
{: #mf-understand}

{{site.data.keyword.aios_short}} überprüft Ihr bereitgestelltes Modell während der Laufzeit auf Verzerrungen. Damit Verzerrungen für ein bereitgestelltes Modell erkannt werden können, müssen Sie Fairnessattribute wie etwa Alter oder Geschlecht definieren, wie weiter unten in [Fairnessüberwachung konfigurieren](#mf-config) detailliert beschrieben.

Damit das Ausgabeschema für ein Modell oder eine Funktion in Watson {{site.data.keyword.pm_short}} angegeben werden kann, ist es zwingend erforderlich, dass die Verzerrungsprüfung in {{site.data.keyword.aios_short}} aktiviert ist. Das Ausgabeschema kann anhand der Eigenschaft `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` im Metadatenbereich er API `store_model` angegeben werden. Weitere Informationen hierzu enthält die [Dokumentation für den WML-Client ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://wml-api-pyclient-dev.mybluemix.net/#repository){: new_window}.

### Funktionsweise
{: #mf-works}

Bevor Sie die Fairnessüberwachung konfigurieren, sollten Sie sich mit einigen zentralen Konzepten vertraut machen, die Sie unbedingt verstehen sollten: 

- *Fairnessattribute*: Das sind diejenigen Modellattribute, bei denen das Modell wahrscheinlich eine Verzerrung aufweist. Für das Fairnessattribut **`Geschlecht`** könnte das Modell zum Beispiel eine Verzerrung gegenüber bestimmten Werten für das Geschlecht (`Weiblich`, `Transsexuell` usw.) aufweisen. Ein weiteres Beispiel für ein Fairnessattribut ist das **`Alter`**, bei dem das Modell gegenüber Menschen in einer bestimmten eine Verzerrung aufweisen kann, zum Beispiel in der Altersgruppe von `18 bis 25` Jahren.

- *Referenzwert/Überwachter Wert*: Die Werte von Fairnessattributen sind in zwei unterschiedliche Kategorien unterteilt, nämlich die der Referenzwerte und die der überwachten Werte. Die überwachten Werte sind diejenigen, bei denen wahrscheinlich eine Diskrimination auftritt. Im Fall eines Fairnessattributs wie **`Geschlecht`** könnten als überwachte Werte `Weiblich` und `Transsexuell` verwendet werden. Bei einem numerischen Fairnessattribut wie **`Alter`** könnte der Altersbereich `[18-25]` als überwachte Werte dienen. Alle anderen Werte für ein bestimmtes Fairnessattribut werden dann als Referenzwerte betrachtet, wie zum Beispiel `Geschlecht=Männlich` oder `Alter=[26,100]`.

- *Günstiges/Ungünstige Ergebnis*: Die Ausgabe des Modells wird entweder als günstig oder als ungünstig kategorisiert. Wenn das Modell zum Beispiel vorhersagt, ob eine Person ein Darlehen erhalten sollte oder nicht, könnten `Darlehen bewilligt` oder `Darlehen teilbewilligt` als günstiges Ergebnis und im Gegensatz dazu `Darlehen abgelehnt` als ungünstiges Ergebnis dienen. Das günstige Ergebnis ist also ein Ergebnis, das als positives Ergebnis angesehen wird, während das ungünstige Ergebnis als negativ gilt.

Der {{site.data.keyword.aios_short}}-Algorithmus berechnet Verzerrungen auf Stundenbasis und verwendet dabei die letzten `N` Datensätzen, die in der Nutzdatenprotokollierungstabelle vorhanden sind, wobei der Wert für `N` bei der Konfiguration der Fairness angegeben wird. Der Algorithmus stört diese letzten `N` Datensätze durch Perturbation, um zusätzliche Daten zu generieren.

Die Perturbation (Störung) erfolgt durch Ändern des Werts des Fairnessattributs von 'Referenz' zu 'Überwacht' oder umgekehrt. Die durch Perturbation gestörten Daten werden dann an das Modell gesendet, um sein Verhalten zu auszuwerten. Der Algorithmus analysiert die letzten `N` Datensätze in der Nutzdatentabelle und das Verhalten des Modells für die durch Perturbation gestörten Daten, um zu bestimmen, ob das Modell verzerrt handelt.

Ein Modell gilt als verzerrt, wenn in diesem kombinierten Dataset der Prozentsatz der günstigen Ergebnisse für die überwachte Klasse um einen bestimmten Schwellenwert niedriger ist als der Prozentsatz der günstigen Ergebnisse für die Referenzklasse. Die Angabe dieses Schwellenwerts muss bei der Konfiguration der Fairness erfolgen.

Fairnesswerte können über 100 % liegen. Dies bedeutet, dass die überwachte Gruppe mehr günstige Ergebnisse als die Referenzgruppe erhalten hat. Darüber hinaus bleibt der Fairnesswert konstant, wenn keine neuen Scoring-Anforderungen gesendet werden.
{: note}

### Beispiel
{: #mf-ex1}

Nehmen Sie einen Datenpunkt, bei dem das Modell für `Geschlecht=Männlich` (Referenzwert) ein günstiges Ergebnis vorhersagt. Wird der Datensatz jedoch durch Perturbationen gestört, indem `Geschlecht` zu `Weiblich` (überwachter Wert) geändert wird, während die Werte für alle übrigen Merkmale gleicht bleiben, sagt das Modell ein ungünstiges Ergebnis vorher. Ein Modell gilt allgemein als kognitiv verzerrt, wenn es genügend Datenpunkte (in den letzten `N` Datensätzen in der Nutzdatentabelle zuzüglich den durch Perturbation gestörten Daten) enthält, bei denen das Modell in verzerrter Weise agiert hat.

### Unterstützte Modelle
{: #mf-supmo}

 {{site.data.keyword.aios_short}} unterstützt die Erkennung von Verzerrungen nur für diejenigen Modelle und Python-Funktionen, die eine Art strukturierter Daten in ihrem Merkmalsvektor erwarten.

## Fairnessüberwachung konfigurieren
{: #mf-config}

1.  Klicken Sie auf der Seite *Was ist Genauigkeit?* auf **Weiter**, um den Konfigurationsprozess zu starten.

    ![Seite 'Was ist Fairness?'](images/fair-what-is.png)

1.  Suchen Sie auf der Seite *Zu überwachende Merkmale auswählen* die Fairnessattribute, die Sie verwenden möchte , wählen Sie sie aus. Klicken Sie danach auf **Weiter**.

    Es werden nur Merkmale unterstützt, die 'kategorial', 'numerisch' (Ganzzahl), Gleitkomma oder Double als Datentyp unterstützen. Merkmale mit anderen Datentypen werden nicht unterstützt.
    {: note}

    In diesem Beispiel wurden die Merkmale `Alter`, `Geschlecht` und `Ethnie` ausgewählt.

    ![Seite 'Zu überwachende Merkmale auswählen' mit ausgewählten Merkmalen](images/fair-select-feature.png)

    Klicken Sie zum Fortfahren auf **Weiter**.

1.  Für jedes Merkmal müssen bestimmte Anforderungen konfiguriert werden. Im vorliegenden Beispiel definieren Sie die Zahlengruppen für das **`Alter`** für eine Referenzgruppe und eine überwachte Gruppe, indem Sie in jede Gruppe die Werte jeweils direkt eingeben.

    Wenn Sie bei diesem Beispiel für das Fairnessattribut **`Alter`** der Auffassung sind, dass Ihr Modell bei Menschen im Alter von 18 und 25 Jahren mit gewisser Wahrscheinlichkeit eine Verzerrung aufweist, so muss der Zahlenbereich für die überwachte Gruppe `[18-25]` lauten, während Sie für die Referenzgruppe den Bereich `[26-100]` festlegen. Beim Fairnessattribut **`Geschlecht`** könnte die Referenzgruppe den Wert `Männlich` haben, während für die Überwachungsgruppe die Werte `Weiblich` und `Transsexuell` verwendet angegeben werden könnten.

    ![Einstellungen für das Alter konfigurieren](images/fair-config-age.png)

    Klicken Sie zum Fortfahren auf **Weiter**.

1.  Legen Sie für **`Alter`** den Schwellenwert für die Fairness fest.

    Eine Fairnessschwellenwert wird verwendet, um eine annehmbare Differenz zwischen dem Prozentsatz der günstigen Ergebnisse für die überwachte Gruppe im Vergleich zu dem Prozentsatz der günstigen Ergebnisse für die Referenzgruppe festzulegen.

    Betrachten Sie ein Modell, das vorhersagt, wer ein Darlehen erhalten soll (`Günstiges Ergebnis=Darlehen bewilligt`) und wer nicht (`Ungünstiges Ergebnis=Darlehen abgelehnt`). Außerdem ist für das Alter der Bereich `[18,25]` für die überwachte Gruppe und `[26,100]` für die Referenzgruppe festgelegt. Wenn der Erkennungsalgorithmus für Verzerrung bei der Ausführung feststellt, dass der Prozentsatz der günstigen Ergebnisse bei Menschen der Altersgruppe `[18,25]` in den letzten `N` Datensätzen zuzüglich der durch Perturbation gestörten Daten einen Wert von `50 %` aufweist, während der Prozentsatz der günstigen Ergebnisse bei Menschen der Altersgruppe `[26,100]` bei `70 %` liegt, wird für die Fairness der Wert 50*100/70 = 71,42 berechnet.

    Wenn als Schwellenwert für Fairness ein Wert von 80 % festgelegt ist, kennzeichnet der Algorithmus das Modell als verzerrt, da die berechnete Fairness unter dem festgelegten Schwellenwert liegt. Wenn jedoch ein Wert von 70 % als Schwellenwert festgelegt ist, wird das Modell nicht als verzerrt gemeldet.

    ![Einstellungen für das Alter konfigurieren](images/fair-config-age-limit.png)

    Wählen Sie einen Schwellenwert für die Fairness aus und klicken Sie auf **Weiter**.

1.  Konfigurieren Sie die Merkmale `Geschlecht` und `Ethnie` auf dieselbe Weise:

     ![Einstellungen für das Geschlecht konfigurieren](images/fair-config-gender.png)

     ![Einstellungen für die Ethnie konfigurieren](images/fair-config-ethnic.png)

     **Hinweis**: Die Werte, die Sie in diesen Anzeigen eingeben, sollten diejenigen sein, die an den Modellscoring-Endpunkt gesendet werden (und somit zu der Nutzdatentabelle hinzugefügt werden). Wenn die Daten vor dem Senden an den Scoring-Endpunkt bearbeitet werden, geben Sie die bearbeiteten Werte ein. Wenn die ursprünglichen Daten die Werte `Männlich` und `Weiblich` für das Merkmal *Geschlecht* enthielten und diese dann so bearbeitet wurden, dass `M` und `W` an den Scoring-Endpunkt gesendet wurde, geben Sie in dieser Anzeige die Werte `M` und `W` ein.

     Klicken Sie, wenn Sie die Bearbeitung für die einzelnen Merkmale abgeschlossen haben, auf **Weiter**.

1.  Geben Sie nun Werte an, die ein günstiges Ergebnis für das Modell darstellen. Diese Werte werden aus der Spalte `Kennzeichnung` in den Trainingsdaten abgeleitet, sofern das Modellausgabeschema eine Zuordnungsspalte enthält. Bei WML enthält die Spalte für `Vorhersage` stets einen Wert des Typs 'double'. Anhand der Zuordnungsspalte wird angegeben, wie dieser Wert der `Vorhersage` der Klassenbezeichnung zugeordnet werden soll.

    Wenn `Vorhersage` den Wert `1.0` hat, könnte die Zuordnungsspalte den Wert `Darlehen abgelehnt` aufweisen. Dies bedeutet, dass die Vorhersage des Modells `Darlehen abgelehnt` lautet. Wenn das Modellausgabeschema eine Zuordnungsspalte enthält, geben Sie anhand der in der Zuordnungsspalte enthaltenen Elemente die günstigen bzw. ungünstigen Werte an.

    Wenn im Modellausgabeschema jedoch keine Zuordnungsspalte vorhanden ist, müssen die günstigen und die ungünstigen Werte anhand des Werts der Spalte `Vorhersage` angegeben werden (`0.0`, `1.0` usw.).

     ![Ergebnis konfigurieren](images/fair-config-outcome.png)

     Klicken Sie auf **Weiter**.

1.  Legen Sie zum Schluss einen Mindeststichprobenumfang fest, um zu verhindern, dass die Messung der Fairness bereits erfolgt, noch bevor eine Mindestanzahl von Datensätzen im Auswertungsdatensatz verfügbar ist. Dadurch wird sichergestellt, dass die Ergebnisse nicht etwa durch einen zu kleinen Stichprobenumfang verfälscht werden. Bei jeder Durchführung der Verzerrungsprüfung wird dabei jeweils die Mindeststichprobengröße verwendet, um die Anzahl von Datensätzen zu bestimmen, für die sie die Verzerrungsberechnung durchführt.

     ![Stichprobenumfang konfigurieren](images/fair-config-sample.png)

1.  Klicken Sie auf die Schaltfläche **Weiter**.

    Zur Überprüfung wird eine Zusammenfassung der von Ihnen getroffenen Auswahl angezeigt. Falls Sie Änderungen vornehmen möchten, klicken Sie für den betreffenden Abschnitt auf den Link **Bearbeiten**.

    Sie können auch den Link **Weiteres Merkmal hinzufügen** auswählen, um zu der Anzeige für die Merkmalauswahl zurückzukehren und weitere Merkmale zur Fairnessüberwachung hinzuzufügen, wie zum Beispiel `Stadt`, `Postleitzahl` oder `Account Kontostand`.

1.  Klicken Sie zum Abschließen Ihrer Konfiguration auf **Speichern**.

### Funktionsweise der Verzerrungsbereinigung verstehen
{: #mf-debias}

Ihnen wird jetzt eine Anzeige mit einem verzerrungsbereinigten Scoring-Endpunkt angezeigt.

  ![API für Verzerrungsbereinigung](images/fair-debias-api.png)

Der verzerrungsbereinigte Scoring-Endpunkt kann genau so wie der normale Scoring-Endpunkt Ihres bereitgestellten Modells verwendet werden. Es gibt nicht nur die Antwort Ihres bereitgestellten Modells zurück, sondern zwei zusätzliche Spalten namens `debiased_prediction` und `debiased_probability`.

- Die Spalte `debiased_prediction` enthält den verzerrungsbereinigten Vorhersagewert. Im Falle von Watson Machine Learning (WML) handelt es sich dabei um eine codierte Darstellung der Vorhersage. Wenn die Modellvorhersage zum Beispiel entweder 'Darlehen bewilligt' oder 'Darlehen abgelehnt' lautet, kann WML diese beiden Werte mit '0.0' bzw. mit '1.0' kodieren. Die Spalte `debiased_prediction` enthält eine derartig codierte Darstellung der verzerrungsbereinigten Vorhersage.

- Die Spalte `debiased_probability` hingegen stellt die Wahrscheinlichkeit der verzerrungsbereinigten Vorhersage dar. Hierbei handelt es sich um einen Bereich aus Werten des Typs double, bei dem jeder Wert die Wahrscheinlichkeit der verzerrungsbereinigten Vorhersage darstellt, die zu einer der Vorhersageklassen gehört.

Eine weitere Spalte namens `debiased_decoded_target` wird ebenfalls zurückgegeben, und zwar für den Fall, dass sich eine Spalte in Ihrem Ausgabeschema befindet, die eine Spalte mit `modeling-role` als `decoded-target` enthält.

- Die Spalte `debiased_decoded_target` enthält die Zeichenfolgedarstellung der verzerrungsbereinigten Vorhersage. Beim obigen Beispiel, bei dem der Vorhersagewert entweder '0.0' oder '1.0' lautete, wird die Spalte `debiased_decoded_target` entweder 'Darlehen bewilligt' oder 'Darlehen abgelehnt' enthalten.

Im Idealfall würden Sie diesen Endpunkt direkt aus Ihrer Produktionsanwendung aufrufen, anstatt den Scoring-Endpunkt Ihres Modells direkt aufzurufen, das in Ihrer Modellservice-Engine bereitgestellt wird (Watson Machine Learning, Amazon Sagemaker, Microsoft Azure ML Studio usw.). Auf diese Weise speichert {{site.data.keyword.aios_short}} auch die `verzerrungsbereinigten` Werte in der Nutzdatenprotokollierungstabelle Ihrer Modellbereitstellung. Dann wäre die gesamte Bewertung, die über diesen Endpunkt erfolgt, automatisch verzerrungsbereinigt.

Da dieser Endpunkt die Verzerrung zur Laufzeit bearbeitet, wird er weiterhin Hintergrundprüfungen für die neuesten Bewertungsdaten aus der Nutzdatenprotokollierungstabelle durchführen und das Modell für Verzerrungsminimierung, mit dem Verzerrungsbereinigung der gesendeten Scoring-Anforderungen durchgeführt wird, weiterhin aktualisieren. Auf diese Weise ist {{site.data.keyword.aios_short}} mit den zuletzt ankommenden Daten und mit seinem Verhalten zur Erkennung und Bereinigung der Verzerrung stets auf dem neuesten Stand.

{{site.data.keyword.aios_short}} verwendet zum Schluss einen Schwellenwert, um zu entscheiden, ob bzw. dass Daten nun annehmbar sind und als unverzerrt gelten. Für diesen Schwellenwert wird der niedrigste Wert der Schwellenwerte verwendet, die in der Fairnessüberwachung für alle konfigurierten Fairnessattribute festgelegt sind.

### Weitere Schritte
{: #mf-next}

Auf der Seite *Überwachungen konfigurieren* können Sie eine weitere Überwachungskategorie auswählen.
