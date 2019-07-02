---

title: Vertrauen und Transparenz für Ihre Machine Learning-Modelle mit {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

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

# Lernprogramm (Erweitert)
{: #tadv-tutorial-advanced}

## Szenario
{: #tadv-scenario}

Ein Autovermieter hat Rückmeldedaten zur Kundenzufriedenheit gesammelt. Das dargestellte Modell verwendet diese Daten, um die Vorgehensweise für das Nachfassen beim Kunden der Weiterverfolgung eines Kunden vorherzusagen, z. B. durch Vergabe eines Gutscheins für das nächste Mietfahrzeug.

Das Modell verwendet die Kundendatenfelder ID (eine ID-Nummer), GENDER, STATUS ('single' oder 'married'), CHILDREN (Zahl) AGE, CUSTOMER STATUS ('active' oder 'inactive'), CAR OWNER ('yes' oder 'no'), CUSTOMER SERVICE (kundenseitiger Kommentar), SATISFACTION ('satisfied' oder 'unsatisfied' und BUSINESS AREA (bezogen auf 'product' oder 'service'), um für das Datenfeld AKTION einen der folgenden vier Werte vorherzusagen: 'NA', 'Voucher', 'Free upgrade' oder 'On-demand pickup' (Nicht zutreffend, Gutschein, gebührenfreies Upgrade und bedarfsgesteuerte Abholung).

## Voraussetzungen
{: #tadv-prereqs}

Zur vollständigen Durchführung dieses Lernprogramms müssen Sie über Folgendes verfügen:

- Ein Konto bei [Watson Studio ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://dataplatform.ibm.com/){: new_window}
- Ein Konto bei [{{site.data.keyword.cloud_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}){: new_window}

Im Rahmen dieses Lernprogramms werden Sie die folgenden kostenfreien {{site.data.keyword.cloud_notm}}-Services in der Lite-Version einrichten:

- Machine Learning
- Apache Spark
- Object Storage

Außerdem richten Sie die folgenden **gebührenpflichtigen** {{site.data.keyword.cloud_notm}}-Service ein:

- PostgreSQL

  Es kann ein {{site.data.keyword.cloud_notm}}-Guthaben in Höhe von 200 US-Dollar durch Umwandlung in ein gebührenpflichtiges Konto mit einer Kreditkarte erworben werden. Falls Sie bereits über ein gebührenpflichtiges Konto verfügen, erhalten Sie eine einmalige Rückerstattung der Kosten für Ihr erstes GB an Speicherplatz für einen Monat in Höhe von 16 US-Dollar.
  {: tip}

Die PostgreSQL-Datenbank und die {{site.data.keyword.pm_full}}-Instanz müssen in demselben {{site.data.keyword.cloud_notm}}-Konto bereitgestellt werden.
{: important}

Falls Sie die erforderlichen Services bereits eingerichtet haben, zum Beispiel weil Sie das andere Lernprogramm bereits abgearbeitet haben, fahren Sie mit [Watson Studio-Projekt einrichten](#tadv-setup-ws) unten fort.

## Einführung
{: #tadv-intro}

In diesem Lernprogramm lernen Sie Folgendes:

- Einrichten von {{site.data.keyword.cloud_notm}} Machine Learning-Services und -Speicherservices
- Konfigurieren eines Watson Studio-Projekts und Ausführen eines Python-Notizbuchs zum Erstellen, Trainieren und Bereitstellen eines Machine Learning-Modells
- Ausführen eines Python-Notizbuchs zum Erstellen eines Datamarts, Konfigurieren der Leistungs-, Genauigkeits- und Fairnessüberwachungen und Erstellen von Daten, die überwacht werden sollen
- Anzeigen der Ergebnisse auf der {{site.data.keyword.aios_short}}-Registerkarte 'Einsichten'

## {{site.data.keyword.cloud_notm}}-Services einrichten
{: #tadv-svcs}

Melden Sie sich mit Ihrer IBM ID bei Ihrem [{{site.data.keyword.cloud_notm}}-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}){: new_window} an. Bei der Einrichtung von Services, insbesondere bei Apache Spark, Object Storage und Db2 Warehouse, müssen Sie unbedingt sicherstellen, dass für alle Services dieselbe Organisation und der derselbe Bereich (Space) ausgewählt ist.

### Watson Studio-Konto erstellen
{: #tadv-stac}

- Zunächst müssen Sie eine [Watson Studio-Instanz erstellen![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/watson-studio){: new_window}, sofern Ihrem Konto noch keine solche Instanz zugeordnet ist:

  ![Watson Studio](images/watson_studio.png)

- Benennen Sie Ihren Service, wählen Sie den kostenlosen Plan 'Lite' aus und klicken Sie auf die Schaltfläche **Erstellen**.

### Machine Learning-Service bereitstellen
{: #tadv-pml}

- Zunächst müssen Sie eine [Watson Machine Learning-Instanz bereitstellen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/machine-learning){: new_window}, sofern Ihrem Konto noch keine solche Instanz zugeordnet ist:

  ![Machine Learning](images/machine_learning.png)

- Benennen Sie Ihren Service, wählen Sie den kostenlosen Plan 'Lite' aus und klicken Sie auf die Schaltfläche **Erstellen**.

- Notieren Sie die Berechtigungsnachweise für den Machine Learning-Service. Klicken Sie in Ihrer Machine Learning-Instanz links auf der Seite auf den Link **Serviceberechtigungsnachweise**. Nennen Sie den Berechtigungsnachweis und klicken Sie auf **Weiter**. Klicken Sie anschließend in der Liste der Berechtigungsnachweise auf **Berechtigungsnachweis anzeigen** und kopieren Sie die Berechtigungsnachweise zur späteren Verwendung.

### Spark-Service bereitstellen
{: #tadv-ps}

- Zunächst müssen Sie einen [Spark-Service einrichten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/apache-spark){: new_window}, sofern Ihrem Konto noch keine solche Instanz zugeordnet ist:

  ![Apache Spark](images/spark.png)

- Weisen Sie Ihrem Service einen Namen zu, wählen Sie den kostenlosen Plan 'Lite' aus und klicken Sie auf die Schaltfläche **Erstellen**.

- Notieren Sie die Serviceberechtigungsnachweise für Ihre Spark-Instanz. Öffnen Sie Ihre Spark-Instanz und klicken Sie im Menü links auf **Serviceberechtigungsnachweise**. Klicken Sie auf die Schaltfläche **Neuer Berechtigungsnachweis**, benennen Sie Ihre Berechtigungsnachweise und klicken Sie auf **Hinzufügen**. Klicken Sie dann neben dem soeben erstellten Paar auf **Berechtigungsnachweise anzeigen** und kopieren Sie sie zur Verwendung zu einem späteren Zeitpunkt.

### Object Storage-Service einrichten
{: #tadv-pos}

- Zunächst müssen Sie einen [Object Storage-Service einrichten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window}, sofern Ihrem Konto noch keine solche Instanz zugeordnet ist:

  ![Object Storage](images/object_storage.png)

- Benennen Sie Ihren Service, wählen Sie den kostenlosen Plan 'Lite' aus und klicken Sie auf die Schaltfläche **Erstellen**.

### Gebührenpflichtigen PostgreSQL-Service einrichten
{: #tadv-ppgs}

- Zunächst müssen Sie einen [gebührenpflichtigen PostgreSQL-Service einrichten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window}, sofern Ihrem Konto noch kein solcher zugeordnet ist.

  ![Compose for PostgreSQL](images/postgres.png)

- Benennen Sie Ihren Service, wählen Sie den Plan 'Standard' aus und klicken Sie auf die Schaltfläche **Erstellen**.

  Es kann ein {{site.data.keyword.cloud_notm}}-Guthaben in Höhe von 200 US-Dollar durch Umwandlung in ein gebührenpflichtiges Konto mit einer Kreditkarte erworben werden. Falls Sie bereits über ein gebührenpflichtiges Konto verfügen, erhalten Sie eine einmalige Rückerstattung der Kosten für Ihr erstes GB an Speicherplatz für einen Monat in Höhe von 16 US-Dollar.
  {: tip}

- Notieren Sie die Serviceberechtigungsnachweise für Ihre PostgreSQL-Instanz. Öffnen Sie Ihre PostgreSQL-Instanz und klicken Sie im Menü links auf **Serviceberechtigungsnachweise**. Klicken Sie auf die Schaltfläche **Neuer Berechtigungsnachweis**, benennen Sie Ihre Berechtigungsnachweise und klicken Sie auf **Hinzufügen**. Klicken Sie dann neben dem soeben erstellten Paar auf **Berechtigungsnachweise anzeigen** und kopieren Sie sie zur Verwendung zu einem späteren Zeitpunkt.

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![Datentyp manuell festlegen](images/data-type-manual.png)

- Die Trainingsdaten müssten nun ordnungsgemäß in Spalten angezeigt werden. Klicken Sie zum Fortfahren auf **Weiter** und klicken Sie dann auf **Mit dem Laden beginnen**, um die Daten zu laden.

--->

## Watson Studio-Projekt einrichten
{: #tadv-setup-ws}

- Melden Sie sich bei Ihrem [Watson Studio-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://dataplatform.ibm.com/){: new_window} an. Klicken Sie in der rechten oberen Ecke auf das Avatar-Symbol für das Konto stellen Sie sicher, dass es sich bei dem von Ihnen verwendeten Konto um dasselbe Konto handelt, mit dem Sie Ihre {{site.data.keyword.cloud_notm}}-Services erstellt haben:

  ![Dasselbe Konto](images/same_account.png)

- Beginnen Sie in Watson Studio mit der Erstellung eines neuen Projekts. Wählen Sie 'Projekt erstellen' aus:

  ![Watson Studio -Projekt erstellen](images/studio_create_proj.png)

- Wählen Sie zum Erstellen des Projekts die Kachel **Standard** aus:

  ![Projekt 'Standard' in Watson Studio auswählen](images/studio_create_standard.png)

- Geben Sie Ihrem Projekt einen Namen und eine Beschreibung, stellen Sie sicher, dass Sie den im vorherigen Schritt erstellten Object Storage-Service im Menü **Speicher** auswählen, und klicken Sie auf **Erstellen**.

### {{site.data.keyword.cloud_notm}}-Services dem Watson-Projekt zuordnen
{: #tadv-acsw}

- Öffnen Sie Ihr Watson Studio-Projekt und wählen Sie die Registerkarte **Einstellungen** aus. Klicken Sie im Abschnitt **Zugehörige Services** auf die Dropdown-Liste **Service hinzufügen** und wählen Sie **Watson** aus:

  ![Watson-Service hinzufügen](images/add_watson_service.png)

- Klicken Sie auf der Kachel **Machine Learning** auf **Hinzufügen** und wählen Sie die Registerkarte **Vorhanden** aus. Wählen Sie in der Dropdown-Liste **Vorhandene Service-Instanz** den Service aus, den Sie im vorherigen Abschnitt erstellt haben, und klicken Sie auf **Auswählen**.

- Wählen Sie auf der Registerkarte für Projekteinstellungen erneut die Option **Service hinzufügen** aus und wählen Sie in der Dropdown-Liste **Spark** aus. Wählen Sie auf der Registerkarte **Vorhanden** den von Ihnen erstellten Spark-Service aus und klicken Sie auf **Auswählen**.

## Machine Learning-Modell erstellen und bereitstellen
{: #tadv-deploy-ml}

### Notizbuch `CARS4U Action Recommendation - model` zum Watson Studio-Projekt hinzufügen

- Laden Sie die folgende Datei herunter:

    - [CARS4U Action Recommendation - model ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- Klicken Sie auf der Registerkarte **Assets** in Ihrem Watson Studio-Projekt auf die Schaltfläche **Zu Projekt hinzufügen** und wählen Sie in der Dropdown-Liste den Eintrag **Notizbuch** aus:

  ![Verbindung hinzufügen](images/add_notebook.png)

- Wählen Sie **Aus Datei** aus:

  ![Formular für neues Notizbuch](images/new_notebook_name.png)

- Klicken Sie dann auf die Schaltfläche **Datei auswählen** und wählen Sie die heruntergeladene Notizbuchdatei 'CARS4U Action Recommendation - model' aus:

  ![Formular für neues Notizbuch](images/new_notebook_name2.png)

- Wählen Sie im Abschnitt **Laufzeit auswählen** die Spark-Instanz aus der Dropdown-Liste aus, die Sie zuvor erstellt haben:

  ![Spark-Laufzeit](images/spark_runtime.png)

- Klicken Sie auf **Notizbuch erstellen**.

### Notizbuch `CARS4U Action Recommendation - model` bearbeiten und ausführen
{: #tadv-ern}

Das Notizbuch `CARS4U Action Recommendation - model` enthält detaillierte Anweisungen für jeden Schritt im Python-Code, den Sie ausführen werden. Lassen Sie sich beim Durcharbeiten des Notizbuchs etwas Zeit, um zu verstehen, welche Funktionen die einzelnen Befehle haben.
{: tip}

- Klicken Sie auf der Registerkarte **Assets** in Ihrem Watson Studio-Projekt neben dem Notizbuch `CARS4U Action Recommendation - model` auf das Symbol **Bearbeiten**, um das Notizbuch zu bearbeiten.

- Ersetzen Sie in Abschnitt 2.2 - 'Daten in PostgreSQL-Datenbank hochladen' - die Serviceberechtigungsnachweis für Postgres durch die Berechtigungsnachweise, die Sie im vorherigen Abschnitt erstellt haben.

- Ersetzen Sie in Abschnitt 4 bei 'Modell im Repository speichern' unter **TIPP** die Berechtigungsnachweise für Watson Machine Learning durch diejenigen, die Sie im vorherigen Abschnitt erstellt haben.

- Nachdem Sie Ihre Berechtigungsnachweise eingegeben haben, kann Ihr Notizbuch ausgeführt werden. Klicken Sie auf das Menüelement **Kernel** und wählen Sie im Menü **Alles neu starten und ausführen** aus:

  ![Neu starten und ausführen](images/restart_and_run.png)

  Dadurch wird das Modell **CARS4U - Action Recommendation Model** in Ihrem Projekt erstellt, trainiert und bereitgestellt. Sie können sich dann vergewissern, ob das Modell bereitgestellt wurde, indem Sie in Ihrem Watson Studio-Projekt die Registerkarte **Bereitstellungen** auswählen und auf den Link **CARS4U - Area and Action Model Deployment** klicken.

## {{site.data.keyword.aios_short}} konfigurieren
{: #tadv-config-aios}

### {{site.data.keyword.aios_short}} einrichten
{: #tadv-paios}

- Wenn Sie noch keine Instanz von {{site.data.keyword.aios_short}} eingerichtet haben, klicken Sie in Ihrem {{site.data.keyword.cloud_notm}}-Konto auf den Link **Katalog** und filtern Sie nach 'OpenScale'. Wählen Sie die Kachel für {{site.data.keyword.aios_short}} aus.

<!---
  ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)
--->

- Benennen Sie Ihren Service, wählen Sie den Plan 'Lite' aus und klicken Sie auf **Erstellen**.

### Verbindung von {{site.data.keyword.aios_short}} zu Ihrem Machine Learning-Modell herstellen
{: #tadv-cmlm}

Da das Machine Learning-Modell bereitgestellt worden ist, können Sie {{site.data.keyword.aios_short}} konfigurieren, um Vertrauen und Transparenz im Zusammenhang mit Ihren Modellen sicherzustellen. Wählen Sie für Ihre {{site.data.keyword.aios_short}}-Instanz die Registerkarte **Verwalten** aus und klicken Sie auf die Schaltfläche **Anwendung starten**. Die {{site.data.keyword.aios_full}}-Seite für 'Erste Schritte' wird geöffnet. Klicken Sie auf **Beginnen**.

- Wählen Sie die Kachel 'Watson Machine Learning' aus und klicken Sie auf **Weiter**.

  ![WML-Instanz festlegen](images/gs-wml-default.png)

- Wählen Sie Ihre Watson Machine Learning-Instanz in der Dropdown-Liste aus und klicken Sie auf **Weiter**.

  ![WML-Instanz festlegen](images/gs-set-wml.png)

- Sie haben nun die Möglichkeit auszuwählen, welche bereitgestellten Modelle von {{site.data.keyword.aios_short}} überwacht werden. Prüfen Sie das Modell, das Sie erstellt und bereitgestellt haben. Klicken Sie auf **Weiter**, um die Auswahl zu bestätigen:

  ![Bereitgestellte Modelle auswählen](images/gs-set-deploy.png)

- Als Nächstes müssen Sie eine PostgreSQL-Datenbank auswählen. Dabei stehen die folgenden beiden Optionen zur Auswahl: die Datenbank für den kostenlosen Lite-Plan oder eine vorhandene oder neue Datenbank. Wählen Sie für dieses Lernprogramm die Kachel **Vorhandene Datenbank verwenden oder neue Datenbank kaufen** aus.

    ![Datenbank auswählen](images/gs-set-lite-db1.png)

  Ausführlichere und detaillierte Informationen zu jeder dieser Optionen enthält der Abschnitt [Datenbank angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
  {: note}

- Nachdem Sie die Option 'Vorhandene Datenbank verwenden oder neue Datenbank kaufen' ausgewählt haben, überprüft {{site.data.keyword.aios_short}} Ihr {{site.data.keyword.cloud_notm}}-Konto, um Ihre vorhandene Compose for PostgreSQL-Datenbank ausfindig zu machen.

  Wählen Sie im Dropdown-Menü **Schema** den Eintrag "data_mart" aus..

  ![Datenbank auswählen](images/gs-set-schema1.png)

- Nachdem Sie die Datenbank und das Schema ausgewählt haben, klicken Sie auf **Weiter**, um die Zusammenfassung der Daten zu überprüfen, und klicken Sie dann auf **Speichern**.

  ![Datenbank auswählen](images/gs-setup-summary3.png)

  Klicken Sie bei einer entsprechenden Aufforderung auf **Beenden und Dashboard aufrufen**.

## Datamart erstellen und Leistungs-, Genauigkeit- und Fairnessüberwachungen konfigurieren
{: #tadv-config-monitors}

### Notizbuch `{{site.data.keyword.aios_short}} and Watson ML engine` zu Ihrem Watson Studio-Projekt hinzufügen
{: #tadv-aomn}

Das Notizbuch `{{site.data.keyword.aios_short}} and Watson ML engine` enthält detaillierte Anweisungen für jeden Schritt im Python-Code, den Sie ausführen werden. Lassen Sie sich beim Durcharbeiten des Notizbuchs etwas Zeit, um zu verstehen, welche Funktionen die einzelnen Befehle haben.
{: tip}

- Laden Sie die folgende Datei herunter:

    - [{{site.data.keyword.aios_short}} and Watson ML engine ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Klicken Sie auf der Registerkarte **Assets** in Ihrem Watson Studio-Projekt auf die Schaltfläche **Zu Projekt hinzufügen** und wählen Sie in der Dropdown-Liste den Eintrag **Notizbuch** aus:

  ![Verbindung hinzufügen](images/add_notebook.png)

- Wählen Sie **Aus Datei** aus:

  ![Formular für neues Notizbuch](images/new_notebook_name.png)

- Klicken Sie dann auf die Schaltfläche **Datei auswählen** und wählen Sie die heruntergeladene Notizbuchdatei '{{site.data.keyword.aios_short}} and Watson ML engine' aus:

  ![Formular für neues Notizbuch](images/new_notebook_name3.png)

- Wählen Sie im Abschnitt **Laufzeit auswählen** die Spark-Instanz aus der Dropdown-Liste aus, die Sie zuvor erstellt haben:

  ![Spark-Laufzeit](images/spark_runtime.png)

- Klicken Sie auf **Notizbuch erstellen**.

### Notizbuch `{{site.data.keyword.aios_short}} and Watson ML engine` bearbeiten und ausführen
{: #tadv-eromn}

- Klicken Sie auf der Registerkarte **Assets** in Ihrem Watson Studio-Projekt neben dem Notizbuch `{{site.data.keyword.aios_short}} and Watson ML engine` auf das Symbol **Bearbeiten**, um das Notizbuch zu bearbeiten.

- Abschnitt 1.1 - "Installation und Authentifizierung":

    - Folgen Sie unter **AKTION: instance_id (GUID) und apikey abrufen** den Anweisungen zum Abrufen Ihrer Berechtigungsnachweise. Ersetzen Sie `aios_credentials` durch Ihre eigenen Berechtigungsnachweise.

    - Ersetzen Sie als Nächstes in **AKTION: Watson Machine Learning-Berechtigungsnachweise hier hinzufügen** die Berechtigungsnachweise für Watson Machine Learning durch diejenigen, die Sie zur erstellt haben.

    - Ersetzen Sie schließlich unter **AKTION: PostgreSQL-Berechtigungsnachweise hier hinzufügen** die Berechtigungsnachweise für Postgres durch diejenigen, die Sie zur erstellt haben.

- Nachdem Sie Ihre Berechtigungsnachweise eingegeben haben, kann Ihr Notizbuch ausgeführt werden. Klicken Sie auf das Menüelement **Kernel** und wählen Sie im Menü **Alles neu starten und ausführen** aus:

  ![Neu starten und ausführen](images/restart_and_run.png)

  Dies richtet Ihr Datamart ein, aktiviert die Nutzdatenprotokollierung, konfiguriert und bewertet Leistungs-, Genauigkeits- und Fairnessüberwachungen und stellt diese Metriken Ihrer {{site.data.keyword.aios_short}}-Instanz zur Verfügung.

## Ergebnisse anzeigen
{: #tadv-results}

### Einsichten für Ihre Bereitstellung anzeigen
{: #tadv-vide}

Klicken Sie im [{{site.data.keyword.aios_short}}-Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} auf die Registerkarte **Einsichten**:

  ![Einsichten](images/insight-dash-tab.png)

Auf der Seite 'Einsichten' können Sie sich einen Überblick über die Metriken für Ihre bereitgestellten Modelle verschaffen. Sie können ohne großen Aufwand Alerts für Fairness- oder Genauigkeitsmetriken anzeigen, die unter den festgelegten Schwellenwert gefallen sind, wenn Sie das Notebook ausführen (70 %). Die in diesem Lernprogramm verwendeten Daten und Einstellungen dürften Genauigkeits- und Fairnessmetriken ähnlich den hier gezeigten erstellt haben.

  ![Überblick über 'Einsichten'](images/insight-overview-adv-tutorial.png)

### Überwachungsdaten für Ihre Bereitstellung anzeigen
{: #tadv-vmdd}

Wählen Sie eine Bereitstellung aus, indem Sie auf der Seite 'Einsichten' auf die entsprechende Kachel klicken. Die Überwachungsdaten für diese Bereitstellung werden angezeigt. Verschieben Sie die Markierung auf dem Diagramm, um Daten für den Zeitrahmen auszuwählen, für den Sie das Notizbuch ausgeführt haben. Wählen Sie dann den Link **Details anzeigen** aus.

  ![Daten überwachen](images/insight-monitor-data1.png)

Nun können Sie die Diagramme auf die von Ihnen überwachten Daten überprüfen. Bei diesem Beispiel können Sie mithilfe der Dropdown-Liste **Merkmal** entweder 'Kinder' oder aber 'Geschlecht' auswählen, damit Details zu den überwachten Daten angezeigt werden.

  ![Überblick über 'Einsichten'](images/insight-review-charts1.png)

<!---

### Erklärbarkeit für eine Modelltransaktion anzeigen
{: #tadv-vemt}

Wählen Sie in den Diagrammen für die von Ihnen überwachten Daten die Schaltfläche **Transaktionen anzeigen** aus.

  ![Transaktionen anzeigen](images/view_transactions.png)

  Es wird eine Liste der Transaktionen für die vergangene Stunde angezeigt. Kopieren Sie eine der Transaktions-IDs.

  ![Liste der Transaktionen](images/transaction_list.png)

Klicken Sie mithilfe des Dashboards für [{{site.data.keyword.aios_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} auf die Registerkarte **Erklärbarkeit**:

  ![Erklärbarkeit](images/explainability.png)

Fügen Sie den kopierten Transaktions-ID-Wert in das Suchfeld ein und drücken Sie auf Ihrer Tastatur die **Eingabetaste**. Es wird eine Erklärung dahingehend angezeigt, wie das Modell zu seiner Schlussfolgerung gekommen ist. Diese Erklärung beinhaltet, wie zuversichtlich das Modell war (Konfidenzniveau), welche Faktoren zum Konfidenzniveau beigetragen haben welche Spalten dem Modell zugeführt wurden.

  ![Transaktion anzeigen ](images/view_transaction1.png)

--->

## Weitere Schritte
{: #tadv-next}

- Informieren Sie sich weiter über die [Anzeige und Interpretation der Daten](/docs/services/ai-openscale?topic=ai-openscale-it-ov) und über die [Überwachung der Erklärbarkeit](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
