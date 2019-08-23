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

In diesem Lernprogramm erfahren Sie, wie Sie die erforderlichen {{site.data.keyword.Bluemix_notm}}-Services bereitstellen, ein Projekt einrichten und ein Beispielmodell in Watson Studio bereitstellen sowie Überwachungen in {{site.data.keyword.aios_short}} konfigurieren.
{: shortdesc}

1. [Bereitstellen von {{site.data.keyword.Bluemix_notm}} Machine Learning-Services und -Speicherservices](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps)
2. [Watson Studio-Projekt konfigurieren und Machine Learning-Modell erstellen, trainieren und bereitstellen](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup).
3. [Vertrauen, Transparenz und Erklärbarkeit für Ihr Modell konfigurieren und erkunden](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios)

## Vorausgesetzte {{site.data.keyword.Bluemix_notm}}-Services bereitstellen
{: #gs-prps}

Zusätzlich zu {{site.data.keyword.aios_short}} benötigen Sie zum vollständigen Ausführen dieses Lernprogramms die folgenden Konten und Services.

**Wichtig**: Zur Sicherstellung der bestmöglichen Leistung wird empfohlen, die erforderlichen Services in der gleichen Region wie {{site.data.keyword.aios_short}} zu erstellen. Welche Standorte für {{site.data.keyword.aios_short}} zur Verfügung stehen, können Sie in [Serviceverfügbarkeit](/docs/resources?topic=resources-services_region){: external} nachprüfen.

1.  Melden Sie sich an Ihrem [{{site.data.keyword.Bluemix_notm}}-Konto ](https://{DomainName}){: external} mit Ihrer {{site.data.keyword.ibmid}} an.
1.  Erstellen Sie für jeden der folgenden Services, der noch nicht mit Ihrem Konto verknüpft ist, eine Instanz. Klicken Sie dazu auf den Link, geben Sie dem Service einen Namen, wählen Sie den (kostenlosen) **Lite**-Plan aus und klicken Sie auf die Schaltfläche **Erstellen**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Watson Studio-Projekt einrichten
{: #gs-setup}

1.  Melden Sie sich bei Ihrem [Watson Studio-Konto](https://dataplatform.ibm.com/){: external} an und beginnen Sie mit der Erstellung eines neuen Projekts. Klicken Sie auf **Projekt erstellen**.

    ![Watson Studio - Projekt erstellen](images/studio_create_proj.png)

1.  Klicken Sie auf die Kachel **Leeres Projekt erstellen**.
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

Sie können nun die bereitgestellten Modelle auswählen, die künftig von {{site.data.keyword.aios_short}} überwacht werden.


### Stichprobendaten für das Modell bereitstellen
{: #gs-samp}

Bevor Sie Ihre Überwachungen konfigurieren können, müssen Sie mindestens eine Scoring-Anforderung für Ihr Modell generieren, um eine Protokollierung von Nutzdaten zu generieren, die von den Überwachungen verarbeitet werden kann. In diesem Abschnitt stellen Sie Stichprobendaten für Watson Studio in Form einer JSON-Datei bereit, um eine Scoring-Anforderung zu generieren.

1.  Laden Sie die Datei [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) herunter.

1.  Klicken Sie auf der Registerkarte **Bereitstellungen** Ihres Watson Studio-Projekts auf den Link **credit-risk-deploy** und dann auf die Registerkarte **Testen** und wählen Sie das Symbol für JSON-Eingaben aus.

    ![JSON-Test](images/json_test02.png)

1.  Öffnen Sie jetzt die heruntergeladene Datei `credit_payload_data.json` und kopieren Sie den Inhalt dieser Datei in das JSON-Feld auf der Registerkarte **Testen**. Klicken Sie auf die Schaltfläche **Vorhersagen**, um Trainingsnutzdaten an Ihr Modell zu senden und sie zu bewerten.

    ![JSON-Vorhersage](images/json_test03.png)

## Weitere Schritte
{: #gs-next-steps-config}

Fahren Sie mit diesem Lernprogramm fort, indem Sie die folgenden Schritte ausführen:

1. [Überwachungen für die Bereitstellung vorbereiten](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy).

   Zur Vorbereitung von Überwachungen müssen Sie eines der bereitgestellten Modelle auswählen und dem Dashboard hinzufügen. Klicken Sie auf der Registerkarte **Insights** auf eine Bereitstellungskachel oder auf die Schaltfläche **Zum Dashboard hinzufügen**, um ein bereitgestelltes Modell auszuwählen, und dann auf **Konfigurieren**.

2. [Nutzdatenprotokollierung einrichten](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data).

   Im Abschnitt **Nutzdatenprotokollierung** müssen Sie den Typ der Eingabe angeben.

3. [Modelldetails einrichten](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets).

   Im Abschnitt **Modelldetails** müssen Sie die Modelldetails aufzeichnen. Wählen Sie für dieses Lernprogramm die Option **Überwachungen manuell konfigurieren** aus.

4. [Qualitätsüberwachung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

   Im Abschnitt **Qualität** legen Sie den Alertschwellenwert für die Qualität und die Stichprobenumfänge fest.

5. [Fairnessüberwachung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

   Wählen Sie im Abschnitt **Fairness** aus, welche Features auf Fairness überwacht werden sollen. Für jedes von Ihnen ausgewählte Merkmal überwacht {{site.data.keyword.aios_short}}, welche Neigung zu einem günstigen Ergebnis das bereitgestellte Modell bei einer Gruppe gegenüber einer anderen Gruppe aufweist. Wenngleich Features einzeln überwacht werden, korrigiert die Verzerrungsbereinigung Probleme für alle Features gemeinsam.

6. [Drifterkennungsüberwachung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

   Im Abschnitt **Drift** haben Sie ein Drifterkennungsmodell eingerichtet.
   
5. [Geben Sie eine Gruppe von Beispielrückmeldungsdaten für Ihr Modell an](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv).

   Um die Qualitätsüberwachung zu ermöglichen, müssen Sie Ihrem Modell Rückmeldedaten zur Verfügung stellen. Qualitätsdaten werden erst dann im Dashboard angezeigt, wenn dies geschehen ist. Sie können die Anforderungen auf einmal generieren, indem Sie zum Durchführen des Scoring Stichprobenrückmeldedaten zum Modell hinzufügen. Für diese Task laden Sie eine CSV-Datei herunter, die Stichprobenrückmeldedaten enthält.

6. [Insights abrufen](/docs/services/ai-openscale?topic=ai-openscale-io-ov).

   Nachdem Sie die Genauigkeitsüberwachung konfiguriert haben, wird die Genauigkeitsprüfung nach Ablauf einer Stunde ausgeführt. In einem Produktionssystem ist dies sinnvoll, damit Ihr Dashboard Rückmeldedaten sammeln kann. Für die Zwecke dieses Lernprogramms ist es wahrscheinlich wünschenswert, die Genauigkeitsprüfung manuell auszulösen, nachdem Sie Ihre Rückmeldedaten hinzugefügt haben, sodass die Ergebnisse im Dashboard **Insights** angezeigt werden.

   Wenn Sie das Ergebnis sofort überprüfen möchten, wählen Sie auf der Seite **Insights** eine Bereitstellung aus, klicken Sie auf eine der Metriken für **Qualität** und dann auf **Qualität jetzt überprüfen**.
