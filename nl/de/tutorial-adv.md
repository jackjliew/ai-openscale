---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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

# Lernprogramm für Python-SDK (Erweitert)
{: #crt-ov}

## Szenario
{: #crt-scenario}

Konventionelle Kreditgeber stehen unter dem Druck, ihr digitales Portfolio an Finanzdienstleistungen auf ein umfangreicheres und vielfältigeres Publikum auszuweiten, was einen neuen Ansatz bei der Kreditrisikomodellierung erfordert. Ihre Data-Science-Teams stützen sich derzeit auf Standardmodellierungstechniken wie Entscheidungsstrukturen und logistische Regression, die für moderate Datensätze gut funktionieren und Empfehlungen generieren, die leicht zu erklären sind. Damit wird den gesetzlichen Bestimmungen, dass Kreditentscheidungen transparent und nachvollziehbar sein müssen, Rechnung getragen.

Um einem breiteren Bevölkerungsanteil mit höherem Risiko Zugang zu Krediten zu ermöglichen, müssen die Bonitätsgeschichten (Kredithistorien) von Antragstellern über die herkömmlichen Kredite wie Hypotheken und KFZ-Darlehen hinausgehen und alternative Kreditquellen wie das Zahlungsverhalten gegenüber Versorgungsunternehmen und Preisplänen bei Mobilfunkanbietern sowie Bildungs- und Berufsbezeichnungen erschließen. Diese neuen Datenquellen bieten nicht nur vielversprechende Perspektiven, sondern bringen auch Risiken mit sich, indem sie die Wahrscheinlichkeit unerwarteter Korrelationen erhöhen, die aufgrund von Alter, Geschlecht oder anderen persönlichen Merkmalen eines Antragstellers Verzerrungen verursachen.

Die für diese verschiedenartigen Datasets am besten geeigneten Data-Science-Techniken, wie etwa gradientengetriebene Baumstrukturen und neuronale Netze, können zwar hochpräzise Risikomodelle generieren, allerdings zu einem entsprechenden Preis. Derartige 'Blackbox'-Modelle generieren undurchsichtige Vorhersagen, die irgendwie transparent gemacht werden müssen, um die behördliche Genehmigung sicherzustellen, wie beispielsweise durch Artikel 22 der Datenschutz-Grundverordnung (DSGVO) oder den Fair Credit Reporting Act (FCRA), das vom Bureau of Consumer Financial Protection (BCFP) verwaltet wird.

Das in diesem Lernprogramm bereitgestellte Kreditrisikomodell verwendet ein Trainingsdataset, das 20 Attribute zu jedem Kreditantragsteller enthält. Zwei dieser Attribute - Alter und Geschlecht - können auf Verzerrungen getestet werden. In diesem Lernprogramm steht die Verzerrung bei Geschlecht und Alter im Fokus. Weitere Informationen zu den Trainingsdaten finden Sie unter [Warum muss {{site.data.keyword.aios_short}} auf meine Trainingsdaten zugreifen?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

{{site.data.keyword.aios_short}} überwacht, welche Neigung zu einem günstigen Ergebnis ('Kein Risiko') das bereitgestellte Modell bei einer Gruppe (der Referenzgruppe) gegenüber einer anderen Gruppe (d. h. der überwachten Gruppe) aufweist. In diesem Lernprogramm ist die auf Geschlecht überwachte Gruppe `Weiblich` und die auf Alter überwachte Gruppe besteht aus Antragstellern im Alter von `18 bis 25` Jahren.

## Voraussetzungen
{: #crt-prereqs}

In diesem Lernprogramm wird ein Jupyter-Notizbuch verwendet, das in einem Watson Studio-Projekt ausgeführt unter Verwendung einer Laufzeitumgebung vom Typ 'Python 3.5 mit Spark' ausgeführt werden sollte. Hierzu sind Serviceberechtigungsnachweise für die folgenden {{site.data.keyword.cloud_notm}}-Services erforderlich:

- Cloud Object Storage (zum Speichern Ihres Watson Studio-Projekts)
- {{site.data.keyword.aios_short}}
- Watson Machine Learning
- (Optional) Database for PostgreSQL oder Db2 Warehouse

Das Jupyter-Notizbuch dient dazu, ein deutsches Kreditrisikomodell zu erstellen, zu trainieren und bereitzustellen, {{site.data.keyword.aios_short}} für die Überwachung dieser Bereitstellung zu konfigurieren und Protokollaufzeichnungen sowie Messungen im Umfang von sieben Tagen zur Anzeige im {{site.data.keyword.aios_short}}-Dashboard 'Einsichten' bereitzustellen. Optional können Sie das Modell auch für kontinuierliches Lernen mit Watson Studio und Spark konfigurieren.

## Einführung
{: #crt-intro}

In diesem Lernprogramm lernen Sie Folgendes:

- Einrichten von {{site.data.keyword.cloud_notm}} Machine Learning-Services und -Speicherservices
- Konfigurieren eines Watson Studio-Projekts und Ausführen eines Python-Notizbuchs zum Erstellen, Trainieren und Bereitstellen eines Machine Learning-Modells
- Ausführen eines Python-Notizbuchs zum Erstellen eines Datamarts, Konfigurieren der Leistungs-, Genauigkeits- und Fairnessüberwachungen und Erstellen von Daten, die überwacht werden sollen
- Anzeigen der Ergebnisse auf der {{site.data.keyword.aios_short}}-Registerkarte 'Einsichten'

## {{site.data.keyword.cloud_notm}}-Services einrichten
{: #crt-services}

Melden Sie sich mit Ihrer {{site.data.keyword.ibmid}} bei Ihrem [{{site.data.keyword.cloud_notm}}-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}){: new_window} an. Bei der Einrichtung von Services, insbesondere bei der Nutzung von Db2 Warehouse, müssen Sie unbedingt sicherstellen, dass für alle Services dieselbe Organisation und der derselbe Bereich ausgewählt ist.

### {{site.data.keyword.DSX}}-Konto erstellen
{: #crt-wstudio}

- Zunächst müssen Sie eine [{{site.data.keyword.DSX}}-Instanz erstellen![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/watson-studio){: new_window}, sofern Ihrem Konto noch keine solche Instanz zugeordnet ist:

  ![Watson Studio](images/watson_studio.png)

- Benennen Sie Ihren Service, wählen Sie den kostenlosen Plan 'Lite' aus und klicken Sie auf die Schaltfläche **Erstellen**.

### {{site.data.keyword.cos_full_notm}}-Service einrichten
{: #crt-cos}

- Zunächst müssen Sie einen [{{site.data.keyword.cos_short}}-Service einrichten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window}, sofern Ihrem Konto noch keine solche Instanz zugeordnet ist:

  ![Object Storage](images/object_storage.png)

- Benennen Sie Ihren Service, wählen Sie den kostenlosen Plan 'Lite' aus und klicken Sie auf die Schaltfläche **Erstellen**.

### {{site.data.keyword.pm_full}}-Service einrichten
{: #crt-wml}

- Zunächst müssen Sie eine [{{site.data.keyword.pm_short}}-Instanz bereitstellen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/machine-learning){: new_window}, sofern Ihrem Konto noch keine solche zugeordnet ist:

  ![Machine Learning](images/machine_learning.png)

- Benennen Sie Ihren Service, wählen Sie den kostenlosen Plan 'Lite' aus und klicken Sie auf die Schaltfläche **Erstellen**.

### (Optional) Databases for PostgreSQL- oder DB2 Warehouse-Service einrichten
{: #crt-db2}

Wenn Sie über ein gebührenpflichtiges {{site.data.keyword.cloud_notm}}-Konto verfügen, können Sie einen Service vom Typ `Databases for PostgreSQL` oder einen `Db2 Warehouse`-Service einrichten, um die Vorteile der Integration mit {{site.data.keyword.DSX}} und Services für kontinuierliches Lernen optimal zu nutzen. Wenn Sie sich gegen die Einrichtung eines gebührenpflichtigen Service entscheiden, können Sie zwar den kostenlosen internen PostgreSQL-Speicher mit {{site.data.keyword.aios_short}} verwenden, aber Sie können kein kontinuierliches Lernen für Ihr Modell konfigurieren.

- Zunächst müssen Sie einen [Databases for PostgreSQL-Service einrichten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/databases-for-postgresql) oder einen [Db2 Warehouse-Service einrichten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/db2-warehouse), sofern Ihrem Konto noch kein solcher zugeordnet ist:

  ![DB for Postgres](images/dbpostgres.png)

  ![Db2 Warehouse](images/db2_warehouse.png)

- Benennen Sie Ihren Service, wählen Sie den Plan 'Standard' (Databases for PostgreSQL) oder den Einstiegsplan (Db2 Warehouse) aus und klicken Sie auf die Schaltfläche **Erstellen**.

## {{site.data.keyword.DSX}}-Projekt einrichten
{: #crt-set-wstudio}

- Melden Sie sich bei Ihrem [{{site.data.keyword.DSX}}-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://dataplatform.ibm.com/){: new_window} an. Klicken Sie auf das {{site.data.keyword.avatar}} und stellen Sie sicher, dass es sich bei dem von Ihnen verwendeten Konto um dasselbe Konto handelt, mit dem Sie Ihre {{site.data.keyword.cloud_notm}}-Services erstellt haben:

  ![Dasselbe Konto](images/same_account.png)

- Beginnen Sie in {{site.data.keyword.DSX}} mit der Erstellung eines neuen Projekts. Wählen Sie 'Projekt erstellen' aus:

  ![Watson Studio - Projekt erstellen](images/studio_create_proj.png)

- Wählen Sie zum Erstellen des Projekts die Kachel **Standard** aus:

  ![Projekt 'Standard' in Watson Studio auswählen](images/studio_create_standard.png)

- Geben Sie Ihrem Projekt einen Namen und eine Beschreibung, stellen Sie sicher, dass im Dropdown-Fenster für **Speicher** der von Ihnen erstellte Object Storage-Service ausgewählt ist, und klicken Sie auf **Erstellen**.

## {{site.data.keyword.pm_short}}-Modell erstellen und bereitstellen
{: #crt-make-model}

### Notizbuch `Mit Watson Machine Learning arbeiten` zu Ihrem {{site.data.keyword.DSX}}-Projekt hinzufügen
{: #crt-add-notebook}

- Laden Sie die folgende Datei herunter:

    - [Mit Watson Machine Learning arbeiten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Klicken Sie auf der Registerkarte **Assets** in Ihrem {{site.data.keyword.DSX}}-Projekt auf die Schaltfläche **Zu Projekt hinzufügen** und wählen Sie im Dropdown-Fenster den Eintrag **Notizbuch** aus:

  ![Verbindung hinzufügen](images/add_notebook.png)

- Wählen Sie **Aus Datei** aus:

  ![Formular für neues Notizbuch](images/new_notebook_name.png)

- Klicken Sie dann auf die Schaltfläche **Datei auswählen** und wählen Sie die Notizbuchdatei 'german_credit_lab.ipynb' aus, die Sie soeben heruntergeladen haben:

  ![Formular für neues Notizbuch](images/new_notebook_name2a.png)

- Wählen Sie im Abschnitt **Laufzeit auswählen** eine Option von Python 3.5 mit Spark aus:

- Klicken Sie auf **Notizbuch erstellen**.

### Notizbuch `Mit Watson Machine Learning arbeiten` bearbeiten und ausführen
{: #crt-edit-notebook}

Das Notizbuch `Mit Watson Machine Learning arbeiten` enthält detaillierte Anweisungen für jeden Schritt im Python-Code, den Sie ausführen werden. Nehmen Sie sich beim Durcharbeiten des Notizbuchs etwas Zeit, um zu verstehen, welche Funktionen die einzelnen Befehle haben.
{: tip}

- Klicken Sie auf der Registerkarte **Assets** in Ihrem Watson Studio-Projekt neben dem Notizbuch `Mit Watson Machine Learning arbeiten` auf das Symbol **Bearbeiten**, um das Notizbuch zu bearbeiten.

- Nehmen Sie im Abschnitt 'Services einrichten und Berechtigungsnachweise konfigurieren' die folgenden Änderungen vor:

    - Folgen Sie den Anweisungen zum Erstellen, Kopieren und Einfügen eines {{site.data.keyword.cloud_notm}}-API-Schlüssels.

    - Ersetzen Sie die Berechtigungsnachweise für Watson Machine Learning (WML) durch die, die Sie zuvor erstellt haben.

    - Ersetzen Sie die Berechtigungsnachweise für die Datenbank durch diejenigen, die Sie für Databases for PostgreSQL erstellt haben.

    - Falls Sie {{site.data.keyword.aios_short}} zuvor für die Verwendung einer kostenlosen internen PostgreSQL-Datenbank als Datamart konfiguriert haben, können Sie zu einem neuen Datamart wechseln, das Ihren Databases for PostgreSQL-Service verwendet. Um Ihre alte PostgreSQL-Konfiguration zu löschen und eine neue zu erstellen, geben Sie für die Variable KEEP_MY_INTERNAL_POSTGRES den Wert `False` an.

        Das Notizbuch entfernt Ihren bestehenden internen PostgreSQL-Datamart und erstellt mit den angegebenen DB-Berechtigungsnachweisen einen neuen Datamart. **Es findet keine Datenmigration statt**.
        {: important}

- Nachdem Sie Ihre Services bereitgestellt und Ihre Berechtigungsnachweise eingegeben haben, kann Ihr Notizbuch ausgeführt werden. Klicken Sie auf den Menüpunkt **Kernel** und wählen Sie im Menü die Option **Erneut starten & Ausgabe löschen** aus:

  ![Erneut starten und Ausgabe löschen](images/restart_and_clear.png)

- Führen Sie nun die einzelnen Schritte des Notizbuchs der Reihenfolge nach aus. Beachten Sie, was bei jedem Schritt geschieht, wie beschrieben. Führen Sie alle Schritte bis einschließlich den Schritten im Abschnitt 'Additional data to help debugging' aus.

Als Endergebnis haben Sie das Modell **Spark German Risk Deployment** auf Ihrer {{site.data.keyword.aios_short}}-Serviceinstanz erstellt, trainiert und bereitgestellt. {{site.data.keyword.aios_short}} wird konfiguriert, um das Modell auf Verzerrungen hinsichtlich Geschlecht (in diesem Fall 'Weiblich') oder Alter (in diesem Fall '18-25 Jahre') zu prüfen.

## Ergebnisse anzeigen
{: #crt-view-results}

### Einsichten für Ihre Bereitstellung anzeigen
{: #crt-view-insights}

Klicken Sie im [{{site.data.keyword.aios_short}}-Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} auf die Registerkarte **Einsichten**:

  ![Einsichten](images/insight-dash-tab.png)

Auf der Seite 'Einsichten' können Sie sich einen Überblick über die Metriken für Ihre bereitgestellten Modelle verschaffen. Sie können ohne großen Aufwand Alerts für Fairness- oder Genauigkeitsmetriken anzeigen, die unter den festgelegten Schwellenwert gefallen sind, wenn Sie das Notebook ausführen. Die in diesem Lernprogramm verwendeten Daten und Einstellungen dürften Genauigkeits- und Fairnessmetriken ähnlich den hier gezeigten erstellt haben.

  ![Überblick über 'Einsichten'](images/insight-overview-adv-tutorial-2.png)

### Überwachungsdaten für Ihre Bereitstellung anzeigen
{: #crt-view-mon-data}

1. Wenn Überwachungsdetails angezeigt werden sollen, klicken Sie auf der Seite **Einsichten** auf die Kachel, die der jeweiligen Bereitstellung entspricht. Die Überwachungsdaten für diese Bereitstellung werden angezeigt. 
2. Verschieben Sie die Markierung auf dem Diagramm, um Daten für ein bestimmtes einstündiges Zeitfenster auszuwählen. 
3. Klicken Sie auf den Link **Details anzeigen**.

  ![Daten überwachen](images/insight-monitor-data2.png)

Nun können Sie die Diagramme auf die von Ihnen überwachten Daten überprüfen. Bei diesem Beispiel ist erkennbar, dass die Gruppe `Weiblich` für das Merkmal 'Geschlecht' das günstige Ergebnis 'Kein Risiko' seltener (68 %) erhielt als die Gruppe `Männlich` (78 %).

  ![Überblick über 'Einsichten'](images/insight-review-charts2.png)

### Erklärbarkeit für eine Modelltransaktion anzeigen
{: #crt-view-explain}

Für jede Bereitstellung können Sie Erklärungsdaten für bestimmte Transaktionen anzeigen.

Wenn Sie bereits wissen, welche Transaktion Sie anzeigen möchten, gibt es die Möglichkeit, diese Transaktion schnell mit der Transaktions-ID aufzurufen. Klicken Sie dazu auf der Bereitstellungskachel im Navigator auf das Symbol **Transaktion erklären** ![Registerkarte 'Transaktion erklären'](images/insight-transact-tab.png), geben Sie die Transaktions-ID ein und drücken Sie die **Eingabetaste**.
{: tip}

Wenn Sie die interne Lite-Version von PostgreSQL verwenden, können Sie Ihre Datenbankberechtigungsnachweise möglicherweise nicht abrufen. Dadurch wird unter Umständen die Anzeige von Transaktionen verhindert.
{: note}

1. Klicken Sie in den Diagrammen für die neuesten verzerrten Daten auf die Schaltfläche **Transaktionen anzeigen**.

  ![Transaktionen anzeigen](images/view_transactions.png)

  Es wird eine Liste der Transaktionen angezeigt, bei denen die Bereitstellung verzerrt agiert hat. 
  
2. Wählen Sie eine der Transaktionen aus und klicken Sie in der Spalte **AKTION** auf den Link **Erklären**.

  ![Liste der Transaktionen](images/transaction_list_cr.png)

Es wird eine Erklärung dahingehend angezeigt, wie das Modell zu seiner Schlussfolgerung gekommen ist. Diese Erklärung beinhaltet, wie zuversichtlich das Modell war (Konfidenzniveau), welche Faktoren zum Konfidenzniveau beigetragen haben welche Spalten dem Modell zugeführt wurden.

  ![Transaktion anzeigen](images/view_transaction_cr.png)
  
## Weitere Schritte
{: #crt-next-steps}

- Informieren Sie sich weiter über die [Anzeige und Interpretation der Daten](/docs/services/ai-openscale?topic=ai-openscale-it-ov) und über die [Überwachung der Erklärbarkeit](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
