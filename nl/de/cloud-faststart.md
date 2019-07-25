---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, fast start

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

# Lernprogramm für die interaktive Konfiguration
{: #gs-obj}

In diesem Lernprogramm führen Sie die folgenden Schritte durch:

- [{{site.data.keyword.Bluemix_notm}} Machine Learning-Services und -Speicherservices bereitstellen](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps)
- [Watson Studio-Projekt konfigurieren und Machine Learning-Modell erstellen, trainieren und bereitstellen](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup).
- [Vertrauen, Transparenz und Erklärbarkeit für Ihr Modell konfigurieren und erkunden](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios)

## Vorausgesetzte {{site.data.keyword.Bluemix_notm}}-Services bereitstellen
{: #gs-prps}

Zusätzlich zu {{site.data.keyword.aios_short}} benötigen Sie zum vollständigen Ausführen dieses Lernprogramms die folgenden Konten und Services.

**Wichtig**: Zur Sicherstellung der bestmöglichen Leistung wird empfohlen, die erforderlichen Services in der gleichen Region wie {{site.data.keyword.aios_short}} zu erstellen. Welche Standorte für {{site.data.keyword.aios_short}} zur Verfügung stehen, können Sie in [Serviceverfügbarkeit](/docs/resources?topic=resources-services_region) nachprüfen.

1.  Melden Sie sich an Ihrem [{{site.data.keyword.Bluemix_notm}}-Konto ](https://{DomainName}){: external} mit Ihrer {{site.data.keyword.ibmid}} an.
1.  Erstellen Sie für jeden der folgenden Services, der noch nicht mit Ihrem Konto verknüpft ist, eine Instanz. Klicken Sie dazu auf den Link, geben Sie dem Service einen Namen, wählen Sie den (kostenlosen) **Lite**-Plan aus und klicken Sie auf die Schaltfläche **Erstellen**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Watson Studio-Projekt einrichten
{: #gs-setup}

1.  Melden Sie sich bei Ihrem [Watson Studio-Konto](https://dataplatform.ibm.com/){: external} an und beginnen Sie mit der Erstellung eines neuen Projekts. Klicken Sie auf **Projekt erstellen**.

    ![Watson Studio - Projekt erstellen](images/studio_create_proj.png)

1.  Klicken Sie auf die Kachel **Standard**.

    ![Projekt 'Standard' in Watson Studio auswählen](images/studio_create_standard.png)

1.  Geben Sie Ihrem Projekt einen Namen und eine Beschreibung, stellen Sie sicher, dass Sie den im vorherigen Schritt erstellten Object Storage-Service im Menü **Speicher** auswählen, und klicken Sie auf **Erstellen**.

### {{site.data.keyword.Bluemix_notm}}-Services dem Watson-Projekt zuordnen
{: #gs-assoc}

1.  Öffnen Sie Ihr Watson Studio-Projekt und wählen Sie die Registerkarte **Einstellungen** aus. Klicken Sie im Abschnitt **Zugehörige Services** auf **Service hinzufügen** und klicken Sie dann auf **Watson**.

    ![Watson-Service hinzufügen](images/add_watson_service.png)

1.  Klicken Sie auf der Kachel **Machine Learning** auf **Hinzufügen**.
2.  Klicken Sie auf der Registerkarte **Vorhanden** in der Dropdown-Liste **Vorhandene Service-Instanz** auf den Service, den Sie zuvor erstellt haben.
3. Klicken Sie auf **Auswählen**.

### Modell `Kreditrisiko` hinzufügen
{: #gs-addmod}

1.  Wählen Sie in {{site.data.keyword.DSX}} für Ihr Projekt die Registerkarte **Assets** aus, blättern Sie bis zum Abschnitt **Watson Machine Learning-Modelle** vor und klicken Sie auf die Schaltfläche **Neues Watson Machine Learning-Modell**.

1.  Wählen Sie im Abschnitt **Modelltyp auswählen** die Option **Aus Beispiel** und das Modell `Kreditrisiko` aus und klicken Sie anschließend auf **Erstellen**.

    ![Anzeige der Kachel für das Kreditrisiko](images/credit-sample-model.png)

### Modell `Kreditrisiko` bereitstellen
{: #gs-depmod}

1.  Klicken Sie auf der Seite mit dem Modell für `Kreditrisiko` auf die Registerkarte **Bereitstellungen** und klicken Sie dann auf **Bereitstellung hinzufügen**.
1.  Geben Sie als Namen für Ihre Bereitstellung die Zeichenfolge `credit-risk-deploy` an und wählen Sie als Bereitstellungstyp die Option **Web-Service** aus.
1.  Klicken Sie auf **Speichern**.

## {{site.data.keyword.aios_short}} konfigurieren
{: #gs-confaios}

Nachdem das Machine Learning-Modell bereitgestellt worden ist, können Sie {{site.data.keyword.aios_short}} konfigurieren, um Vertrauen und Transparenz im Zusammenhang mit Ihren Modellen sicherzustellen.

### {{site.data.keyword.aios_short}} einrichten
{: #gs-provaios}

1.  [Richten Sie eine neue {{site.data.keyword.aios_short}}-Serviceinstanz ein](https://{DomainName}/catalog/services/watson-openscale){: external}.

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  Benennen Sie Ihren Service, wählen Sie den **Plan 'Lite'** aus und klicken Sie auf **Erstellen**.

1.  Wählen Sie für Ihre {{site.data.keyword.aios_short}}-Instanz die Registerkarte **Verwalten** aus und klicken Sie auf die Schaltfläche **Anwendung starten**. Die Seite mit der Demo für **Willkommen bei {{site.data.keyword.aios_short}}** wird geöffnet.
2. Klicken Sie für dieses Lernprogramm auf **Nein danke**.

### Datenbank auswählen
{: #gs-db-choice}

Als Nächstes müssen Sie eine Datenbank auswählen. Dabei stehen die folgenden beiden Optionen zur Auswahl: die kostenlose Datenbank oder eine vorhandene oder neue Datenbank.

2. Wählen Sie für dieses Lernprogramm die Kachel **Datenbank des kostenfreien Lite-Plans verwenden** aus.

   Für die kostenlose Datenbank gelten einige wichtige Einschränkungen. Es handelt sich um eine per Hosting bereitgestellte Datenbank, auf die Ihnen kein separater Zugriff ermöglicht wird. {{site.data.keyword.aios_short}} erhält Zugriff auf Ihre Datenbank und Ihre Daten. Die Datenbank entspricht nicht den Vorgaben der DSGVO. Ausführlichere und detaillierte Informationen zu jeder dieser Optionen enthält der Abschnitt [Datenbank angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-db). Bei der vorhandenen Datenbank kann es sich um eine PostgreSQL-Datenbank oder eine Db2-Datenbank handeln.
    {: tip}

   ![Datenbank auswählen](images/gs-set-lite-db2.png)

1.  Überprüfen Sie die Zusammenfassung der Angaben und klicken Sie auf **Speichern**. Bestätigen Sie den Vorgang und klicken Sie bei entsprechender Aufforderung auf die Schaltfläche **Mit Konfiguration fortfahren**.

    Es wird auch eine Datamart-ID aufgeführt, was dasselbe ist wie eine {{site.data.keyword.aios_short}}-Instanz-ID.
    {: tip}

    ![Überprüfung der Zusammenfassung](images/gs-setup-summary4.png)

1.  Ihre Anzeige kann Ähnlichkeit mit dem folgenden Screenshot haben. Das Sie für das Scoring Ihrer Daten eine GUI-Methode verwenden werden, klicken Sie einfach auf die Schaltfläche **Überwachungen konfigurieren**, um diese Konfiguration zu beenden.

    ![Code für Scoring-Anforderung](images/gs-config-send-scoring.png)

### Verbindung von {{site.data.keyword.aios_short}} zu Ihrem Machine Learning-Modell herstellen
{: #gs-ctmod}


1.  Klicken Sie auf die Kachel **Watson Machine Learning** und anschließend auf **Speichern**.

1.  Wählen Sie für dieses Lernprogramm im Menü Ihre {{site.data.keyword.pm_full}}-Instanz aus und klicken Sie auf **Weiter**.

    Sie haben auch die Möglichkeit, einen anderen {{site.data.keyword.pm_short}}-Standort auszuwählen. Weitere Informationen enthält der Abschnitt [{{site.data.keyword.pm_full}}-Serviceinstanz angeben](/docs/services/ai-openscale?topic=ai-openscale-wml-connect).
    {: note}

    ![ {{site.data.keyword.pm_short}}-Instanz festlegen](images/gs-set-wml.png)

1.  Sie können nun die bereitgestellten Modelle auswählen, die künftig von {{site.data.keyword.aios_short}} überwacht werden. Wählen Sie das Modell aus, das Sie erstellt und bereitgestellt haben, und klicken Sie auf **Weiter**.

    ![Bereitgestellte Modelle auswählen](images/wos-select-model-deployment.png)



### Stichprobendaten für das Modell bereitstellen
{: #gs-samp}

Bevor Sie Ihre Überwachungen konfigurieren können, müssen Sie mindestens eine Scoring-Anforderung für Ihr Modell generieren, um eine Protokollierung von Nutzdaten zu generieren, die von den Überwachungen verarbeitet werden kann. In diesem Abschnitt stellen Sie Stichprobendaten in Form einer JSON-Datei zur Verfügung, um eine Scoring-Anforderung zu generieren.

1.  Laden Sie die Datei [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) herunter.

1.  Klicken Sie auf der Registerkarte **Bereitstellungen** Ihres Watson Studio-Projekts auf den Link **credit-risk-deploy** und dann auf die Registerkarte **Testen** und wählen Sie das Symbol für JSON-Eingaben aus.

    ![JSON-Test](images/json_test02.png)

1.  Öffnen Sie jetzt die heruntergeladene Datei `credit_payload_data.json` und kopieren Sie den Inhalt dieser Datei in das JSON-Feld auf der Registerkarte **Testen**. Klicken Sie auf die Schaltfläche **Vorhersagen**, um Trainingsnutzdaten an Ihr Modell zu senden und sie zu bewerten.

    ![JSON-Vorhersage](images/json_test03.png)

### Für die Überwachung vorbereiten
{: #gs-prepmon}

1.  Wählen Sie nun in der {{site.data.keyword.aios_short}}-Instanz Ihre Bereitstellung aus und klicken Sie auf **Beginnen**.

    ![Bereitstellung auswählen](images/wos-select-model-deployment.png)

1.  Geben Sie das Merkmal an, das die Antwort enthält, die das Modell vorhersagen wird. (Diejenige Tabellenspalte in Ihrer Datenbank, die die Vorhersagewerte oder Kennzeichnungen enthält.) Im vorliegenden Fall sagt das Modell das Kreditrisiko vorher. Wählen Sie daher die Spalte **Risiko** aus und klicken Sie auf **Weiter**.

    ![Für Überwachung vorbereiten](images/wos-select-model-deployment.png)

1.  Als Nächstes geben Sie Informationen zu Ihrem Modell und zu Ihren Trainingsdaten an. Klicken Sie auf **Weiter**.

    ![Erklärung vorbereiten](images/config-what-monitor.png)

1.  Wählen Sie im Menü **Datentyp** den Eintrag **Numerisch/kategorial** als Typ von Daten aus, den Ihre Bereitstellung analysiert, und klicken Sie auf **Weiter**.

    ![Eingabetyp auswählen](images/config-input-monitor.png)

1.  Bei numerischen oder kategorialen Daten müssen Sie Informationen zu den Trainingsdaten für Ihr Modell angeben, um die Überwachungen konfigurieren zu können. Wählen Sie **Überwachungen manuell konfigurieren** aus, um Informationen für die Verbindungsherstellung zu Ihren Trainingsdaten bereitzustellen.

    ![Konfigurationstyp auswählen](images/config-manual-monitor.png)

1.  Der Algorithmustyp ist wichtig für die Überwachung Ihrer Modellmetriken, wie z.B. Genauigkeit. Da die Vorhersage, die das Modell treffen kann, 'Risiko' oder 'Kein Risiko' lautet, wählen Sie **Binäre Klassifizierung** als [Algorithmustyp](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) aus und klicken Sie auf **Weiter**.

    ![Binär](images/binary.png)

1.  Die Standortinformationen für die Stichprobendaten sind in der folgenden Anzeige bereits enthalten. Klicken Sie zum Fortfahren auf **Weiter**.

    ![Seite für Angabe der Speicherposition der Trainingsdaten für Db2](images/gs-config-train-db2-monitor.png)

1.  Das Schema und die Tabelle sind ebenfalls bereits mit Daten gefüllt. Fahren Sie durch Klicken auf **Weiter** fort.

    ![Schema und Trainingstabelle aus einem Db2-Datenbankstandort angeben](images/gs-fair-config-table-db2.png)

1.  Jetzt müssen Sie das Merkmal angeben, das die Antwort(en) enthält, die das Modell vorhersagen wird, in anderen Worten also diejenige Spalte in Ihrer Datenbank, die die Vorhersagewerte (Kennzeichnungen) enthält. Im vorliegenden Fall sagt das Modell das Kreditrisiko vorher. Wählen Sie daher die Spalte **Risiko** aus und klicken Sie auf **Weiter**.

    Ihre Trainingsdatenbank enthält die Werte, die Sie zum Trainieren Ihres Modells bereitgestellt haben.
    {: note}

    ![Eingabe für Kennzeichnungen für die Vorhersage](images/gs-config-label.png)

1.  Wählen Sie die Spalten aus, die zum Trainieren des Modells verwendet werden sollen. Dies sind die Daten, die Ihre Modellbereitstellung in einer Anfrage erwartet. Mit Ausnahme von `_training` handelt es sich bei allen Datenspalten um Eingaben für das Modell. Wählen Sie alle anderen Eingaben aus und klicken Sie auf **Weiter**.

    ![Eingaben für Erklärbarkeit](images/explain_inputs1.png)

1.  Bei kategorialen Daten müssen Sie Spalten angeben, die jetzt zwar Ganzzahlen enthalten, ursprünglich aber Textwerte enthielten. Wählen Sie die Werte wie hier gezeigt aus.

    ![Eingaben für Erklärbarkeit](images/config_categories.png)

1.  Überprüfen Sie die Zusammenfassung der von Ihnen getroffenen Auswahl, klicken Sie auf **Speichern** und anschließend auf **OK**.

### Fairnessüberwachung konfigurieren
{: #gs-cfgfair}

1.  Klicken Sie auf **Fairness**.

1.  Lesen Sie die Angaben zur Fairness und klicken Sie auf **Weiter**. Weitere Informationen hierzu enthält der Abschnitt [Fairness](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

1.  Sie können nun auswählen, welche Merkmale auf Fairness überwacht werden sollen. Für jedes von Ihnen ausgewählte Merkmal überwacht {{site.data.keyword.aios_short}}, welche Neigung zu einem günstigen Ergebnis das bereitgestellte Modell bei einer Gruppe gegenüber einer anderen Gruppe aufweist. In diesem Beispiel werden die Merkmale **Geschlecht** und **Alter** überwacht.

    Merkmale werden einzeln überwacht, aber jedes Debiasing (Verzerrungsbereinigung) korrigiert Probleme gemeinsam für alle Merkmale. Klicken Sie auf die Kacheln für **Geschlecht** und **Alter** und klicken Sie dann auf **Weiter**.

1.  {{site.data.keyword.aios_short}} erkennt Verzerrungen bei einer überwachten Gruppe im Vergleich zu einer Referenzgruppe. Fügen Sie für das Merkmal **Geschlecht** den Wert `Männlich` (male) zu **Referenzgruppe** und den Wert `Weiblich` (female) zu **Überwachte Gruppe** hinzu und klicken Sie auf **Weiter**.

    Das Modell wird für **Geschlecht** als verzerrt markiert, wenn die Proportionen der Risikovorhersage für die überwachte Gruppe von denen für die Referenzgruppe abweichen. Wenn das Modell also für männliche Kunden in 60 % der Fälle das Ergebnis 'Risiko' vorhersagt und für weibliche Kunden in 20 % der Fälle, ist es verzerrt.

    ![Geschlechtergruppen](images/gender_groups1.png)

1.  Weisen Sie **Geschlecht** (Sex) einen Fairnessschwellenwert zu. In Ihrem Dashboard für Unternehmensaktivitäten wird ein Alert angezeigt, wenn der Fairnesswert den von Ihnen festgelegten Schwellenwert übersteigt. Legen Sie einen Prozentsatz von 90 % als Schwellenwert fest und klicken Sie auf **Weiter**.

1.  Fügen Sie für das Merkmal **Alter** (Age) die Werte `26 bis 74` zu **Referenzgruppe** und die Werte `19 bis 25` zur **Überwachte Gruppe** hinzu und klicken Sie auf **Weiter**.

    Wie beim Merkmal **Geschlecht** wird das Modell für **Alter** als verzerrt markiert, wenn die Proportionen der Risikovorhersage für die überwachte Gruppe von denen für die Referenzgruppe abweichen. Wenn also Kunden zwischen 26 und 74 Jahren in einer anderen Proportion die Vorhersage 'Risiko' erhalten als Kunden im Alter von 19 und 25 Jahren, so ist das Modell verzerrt.

    ![Altersgruppen](images/age_groups.png)

1.  Legen Sie für **Alter** (Age) einen Prozentsatz von 90 % fest und klicken Sie auf **Weiter**.

1.  Ziehen Sie Werte aus dem Feld **Werte aus den Trainingsdaten** und legen Sie diese in den Feldern **Günstige Werte** bzw. **Ungünstige Werte** ab. Bei diesem Lernprogramm ist **Kein Risiko** der günstige Wert, während **Risiko** als ungünstiger Wert gilt. Klicken Sie auf **Weiter**.

    {{site.data.keyword.aios_short}} erkennt automatisch, welche Spalte in der Datenbank für die Nutzdatenprotokollierung die Vorhersagewerte enthält und stellt diese im Feld **Werte aus den Trainingsdaten** dar. Beachten Sie, dass Ihre Trainingsdatenbank zwar Werte enthält, die Sie zum Trainieren Ihres Modells angegeben haben, die Datenbank für die Nutzdatenprotokollierung jedoch Rückmeldedaten enthält, die während der Laufzeit des Modells erfasst wurden und mit denen Sie Ihr Modell anschließend optional umtrainieren und neu bereitstellen können.
    {: note}

    ![Positive und negative Werte](images/pos_and_neg2.png)

1.  Legen Sie den Mindeststichprobenumfang fest, indem Sie den Schieberegler auf den Wert 100 verschieben, und klicken Sie dann auf **Weiter**.

    ![Mindeststichprobenumfang](images/gs-fair-config-sample.png)

    In diesem Lernprogramm wird als Mindeststichprobenumfang ein Wert von 100 verwendet. Normalerweise wird eine größerer Stichprobenumfang empfohlen, um sicherzustellen, dass die Ergebnisse nicht etwa durch einen zu kleinen Stichprobenumfang verfälscht werden.
    {: note}

1.  Überprüfen Sie die von Ihnen getroffene Auswahl, klicken Sie auf **Speichern** und anschließend auf **OK**.

    ![Zusammenfassung der Konfiguration](images/fair-summary.png)

    Das folgende Fenster wird mit einem verzerrungsbereinigten Scoring-Endpunkt angezeigt. Da in diesem Lernprogramm zum Durchführen des Scoring für Daten die GUI-Methode und nicht die CLI (Befehlszeilenschnittstelle) verwendet wird, müssen Sie zum Fortfahren auf **OK** klicken.

    ![API für Verzerrungsbereinigung](images/gs-insight-debias-api.png)

### Genauigkeitsüberwachung konfigurieren
{: #gs-cfgac}

1.  Klicken Sie auf **Genauigkeit**.

1.  Lesen Sie die Angabe zur Genauigkeit und klicken Sie auf **Weiter**. Weitere Informationen hierzu enthält der Abschnitt [Genauigkeit](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

1.  Legen einen Prozentsatz von 90 % als Alertschwellenwert für die Genauigkeit fest und klicken Sie auf **Weiter**.

1.  Legen Sie auf der nächsten Anzeige den Mindeststichprobenumfang fest, indem Sie den Schieberegler auf den Wert 10 verschieben, und klicken Sie dann auf **Weiter**.

    In diesem Lernprogramm wurde als Mindeststichprobenumfang ein Wert von 10 festgelegt. Normalerweise wird eine größerer Stichprobenumfang empfohlen, um sicherzustellen, dass die Ergebnisse nicht etwa durch einen zu kleinen Stichprobenumfang verfälscht werden.
    {: note}

1.  Legen Sie als Maximalstichprobenumfang den Wert 10.000 fest. Klicken Sie auf **Weiter**.

1.  Überprüfen Sie die von Ihnen getroffene Auswahl, klicken Sie auf **Speichern** und anschließend auf **OK**.

1.  Zum Schluss erhalten Sie die Möglichkeit, auf Wunsch Rückmeldedaten hinzuzufügen. Dieses Thema wird im nächsten Abschnitt behandelt. Schließen Sie zunächst das Fenster, indem Sie auf **OK** klicken, ohne jedoch auf die Schaltfläche **Rückmeldedaten hinzufügen** zu klicken.

    Weitere Details hierzu enthält der Abschnitt [Genauigkeitsüberwachung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config).

## Stichprobenrückmeldedaten für das Modell bereitstellen
{: #gs-smpfeed}

Um die Genauigkeitsüberwachung zu ermöglichen, müssen Sie Ihrem Modell Rückmeldedaten zur Verfügung stellen. Genauigkeitsdaten werden erst dann im Dashboard angezeigt, wenn dies geschehen ist. Sie können die Anforderungen auf einmal generieren, indem Sie zum Durchführen des Scoring Stichprobenrückmeldedaten zum Modell hinzufügen. Für diese Task laden Sie eine CSV-Datei herunter, die Stichprobenrückmeldedaten enthält.

1.  Laden Sie die Datei [credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv) herunter.

1.  Klicken Sie in {{site.data.keyword.aios_short}} auf die Registerkarte **Insights**.

    ![Insights](images/insight-dash-tab.png)

1.  Klicken Sie auf die Kachel für Ihr bereitgestelltes Modell.

    ![Registerkarte 'Insights' - keine Daten](images/gs-insight-overview.png)

1.  Klicken Sie dann auf **Überwachungen konfigurieren**.

    ![Anzeige des Symbols 'Bearbeiten'](images/gs-insight-edit-icon.png)

1.  Klicken Sie auf **Genauigkeit** und anschließend auf **Rückmeldung**.
1.  Klicken Sie auf die Schaltfläche **Rückmeldedaten hinzufügen** und wählen Sie die heruntergeladene Datei `credit_feedback_data.csv` aus und klicken Sie dann auf **Öffnen**. 
2. Wählen Sie als Trennzeichen das **Komma (,)** aus und klicken Sie dann auf **Auswählen**.

    Die Größe für Dateien ist gegenwärtig auf 8 MB begrenzt.
    {: note}

    ![Begrenzungszeichen bei Genauigkeit](images/accuracy-delimit.png)

Durch Hinzufügen der CSV-Datei werden Ihrem Modell Rückmeldedaten zur Verfügung gestellt.

## Driftüberwachung konfigurieren
{: gs-drift-config}

Weitere Informationen zum Konfigurieren der Driftüberwachung enthält der Abschnitt [Überwachung der Drifterkennung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

## Ergebnisse anzeigen
{: #gs-viewres}

Nachdem Sie die Genauigkeitsüberwachung konfiguriert haben, wird die Genauigkeitsprüfung nach Ablauf einer Stunde ausgeführt. In einem Produktionssystem ist dies sinnvoll, damit Ihr Dashboard Rückmeldedaten sammeln kann. Für die Zwecke dieses Lernprogramms ist es wahrscheinlich wünschenswert, die Genauigkeitsprüfung manuell auszulösen, nachdem Sie Ihre Rückmeldedaten hinzugefügt haben, sodass die Ergebnisse im Dashboard **Insights** angezeigt werden.

Wenn Sie das Ergebnis sofort überprüfen möchten, wählen Sie auf der Seite **Insights** eine Bereitstellung aus und klicken Sie dann auf **Fairness jetzt überprüfen** oder **Qualität jetzt überprüfen**.

Weitere Informationen zum Interpretieren der Ergebnisse finden Sie im Abschnitt [Insights abrufen](/docs/services/ai-openscale?topic=ai-openscale-io-ov).

## Zugehörige Informationen
{: #wos-info}

- Wenn Sie mehr über Verzerrungen erfahren möchten, können Sie in [Fairness](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor) nachlesen.
- Informationen dazu, wie gut Ihr Modell Ergebnisse vorhersagt, finden Sie in [Genauigkeit](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- Informationen zum Interpretieren von Diagrammen, Daten und Transaktionen finden Sie unter [Fairness, durchschnittliche Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).
