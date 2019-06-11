---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: deployment, monitors, data

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

# Überwachungen für eine Bereitstellung vorbereiten
{: #mo-config}

Richten Sie für jede Bereitstellung, die Sie mit {{site.data.keyword.aios_short}} verfolgen, Überwachungen ein und aktivieren Sie diese.
{: shortdesc}

## Bereitstellung auswählen
{: #mo-select-deploy}

1.  Zuerst müssen Sie eine Bereitstellung auswählen.

    Wenn es für ein bestimmtes Modell mehrere Bereitstellungen gibt, werden bei der Konfiguration einer Bereitstellung auch gleich alle anderen Bereitstellungen für genau dieses Modell konfiguriert.
    {: note}

    ![Seite 'Bereitstellung auswählen'](images/config-select-deploy.png)

1.  Wählen Sie die Kachel *Für Überwachung vorbereiten* aus.

    ![Für Überwachung vorbereiten](images/config-prep-monitor.png)

## Mit Daten arbeiten
{: #mo-work-data}

1.  Sie geben jetzt Informationen zu Ihrem Modell und zu Ihren Trainingsdaten an. Klicken Sie auf **Weiter**. Weitere Informationen zu den Trainingsdaten finden Sie unter [Warum muss {{site.data.keyword.aios_short}} auf meine Trainingsdaten zugreifen?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

    ![Erklärung vorbereiten](images/config-what-monitor.png)

1.  Wählen Sie im Dropdown-Menü den Typ von Daten aus, den Ihre Bereitstellung analysiert, und klicken Sie auf **Weiter**.

    ![Eingabetyp auswählen](images/config-input-monitor.png)

### Numerische/kategoriale Daten
{: #mo-nuca}

Bei numerischen oder kategorialen Daten müssen Sie Informationen zu den Trainingsdaten für Ihr Modell angeben, um die Überwachungen konfigurieren zu können.

  ![Konfigurationstyp auswählen](images/config-manual-monitor.png)

- **Überwachungen manuell konfigurieren** - Erfordert die Angabe von Informationen für die Verbindungsherstellung zu Ihren Trainingsdaten.

    - Wählen Sie den [Algorithmustyp](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) aus und klicken Sie auf **Weiter**:

      ![Mehrklassige Klassifikation](images/multiclass.png)

      Stellen Sie unbedingt sicher, dass das Format der Trainingsdaten genau dem Format entspricht, das Ihr Modell erwartet. Wenn das Modell zum Beispiel `M` und `F` für das Merkmal *Gender* erwartet, müssen die Trainingsdaten `M` und `F` enthalten und nicht `Male` und `Female`. Derzeit unterstützt {{site.data.keyword.aios_short}} nur Speicherpositionen von Db2-Datenbanken oder Cloud Object Storage.
        {: important}

    - Geben Sie die Speicherposition an (entweder `Db2` oder `Cloud Object Storage`) und fahren Sie wie folgt fort:

        - Wenn Sie eine Db2-Datenbank verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Hostname oder IP-Adresse
            - Port
            - Datenbank (Name)
            - Benutzername
            - Kennwort

            ![Seite für Angabe der Speicherposition der Trainingsdaten für Db2](images/config-train-db2-monitor.png)

        - Wenn Sie Cloud Object Storage verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Anmelde-URL

              Die Anmelde-URL der Bereichseinstellung des Buckets entsprechen, in dem sich Ihre Trainingsdaten befinden. Die Angabe des Datenbuckets erfolt im nächsten Schritt.
              {: important}

            - Ressourceninstanz (ID)
            - API-Schlüssel

            ![Seite für Angabe der Speicherposition der Trainingsdaten für Cloud Object Storage](images/config-train-cos-monitor.png)

    - Stellen Sie sicher, dass eine gültige Verbindung besteht, indem Sie auf die Schaltfläche **Testen** klicken, um eine Verbindung zu den Trainingsdaten herzustellen. Klicken Sie auf **Weiter**.

    - Geben Sie die genaue Position in der Db2-Datenbank oder in Cloud Object Storage an, an der sich die Trainingsdaten befinden.

        - Wählen Sie für eine Db2-Datenbank sowohl ein Schema als auch eine Trainingstabelle aus, die die von Ihrem Modell erwarteten Spalten enthält:

          ![Angabe der Speicherposition von Schema und Trainingstabelle bei Db2](images/fair-config-table-db2.png)

        - Wählen Sie für Cloud Object Storage ein Bucket und ein Dataset aus:

          ![Angabe der Speicherposition von Bucket und Dataset bei Cloud Object Storage](images/fair-config-dset-cos.png)

          Klicken Sie auf **Weiter**, um mit Schritt 5 unten fortzufahren.

- **Konfigurationsdatei hochladen** - Wählen Sie diese Option aus, wenn Sie es vorziehen, dass Ihre Trainingsdaten privat bleiben. Sie können ein angepasstes Python-Notizbuch verwenden, um {{site.data.keyword.aios_short}} Informationen zur Analyse der Trainingsdaten bereitzustellen, jedoch ohne Zugriff auf die Daten selbst zu gewähren.

  Das Ausführen des Python-Notizbuchs ermöglicht Ihnen, verschiedene Werte in den Spalten des Schemas sowie die Namen der Spalten zu erfassen. Darüber hinaus können Sie mit dem Notizbuch die Überwachung der Fairness vorkonfigurieren.

    - Laden Sie das [angepasste Notizbuch ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: new_window} herunter und ersetzen Sie alle Berechtigungsnachweise durch Ihre eigenen Berechtigungsnachweise.

    - Überprüfen Sie das Notizbuch sorgfältig und geben Sie gegebenenfalls Daten für Ihr Modell an. Speichern Sie das Notizbuch.

    - Führen Sie das Notizbuch aus, um eine mit JSON formatierte Konfigurationsdatei zu generieren.

    - Laden Sie die JSON-Konfigurationsdatei hoch.

        ![JSON-Konfigurationsdatei hochladen](images/config-json-monitor.png)

    - Klicken Sie auf **Weiter**.

- {{site.data.keyword.aios_short}} sucht Ihre Trainingsdaten in den Metadaten, die mit dem Modell in WML gespeichert wurden. Wählen Sie die Kennzeichnungsspalte in den Trainingsdaten aus, die Ihre Vorhersagewerte enthält, und klicken Sie auf **Weiter**.

  ![Bezeichnung der Spalte auswählen](images/fair-config-column.png)

- Wählen Sie die Spalten aus, die zum Trainieren des Modells verwendet werden. Dies sind die Merkmale, die Ihre Modellbereitstellung in einer Anforderung erwartet. Klicken Sie auf **Weiter**.

    ![Bezeichnung der Spalte auswählen](images/explain-select-column.png)

- Wählen Sie zum Schluss die Spalten aus, die Text enthalten und in Ganzzahlen umgewandelt wurden. Wenn die ursprünglichen Trainingsdaten `Male` und `Female` für *Gender* enthielten und diese Angaben nun den Werten `0` bzw. `1` zugeordnet wurden, enthalten die Trainingsdaten jetzt die Werte `0` und `1` für die Spalte *Gender*. Geben Sie solche Spalten an, die jetzt zwar Ganzzahlen enthalten, ursprünglich aber Textwerte enthielten. Klicken Sie auf **Weiter**.

    ![Datentabelle auswählen](images/explain-text-column.png)

### Images und unstrukturierter Text
{: #mo-imun}

- **Images**

  Bei Modellen, die Images als Eingabe akzeptieren, muss das Image im Format (Höhe) x (Breite) x (# Kanäle) dargestellt werden, wobei jeder Punkt entweder monochrome oder RGB-Werte für jedes Pixel darstellt.

- **Unstrukturierter Text**

   Bei Modellen, die Text als Eingabe akzeptieren, wird erwartet, dass das Modell den gesamten Text akzeptiert und nicht etwa eine vektorisierte Darstellung des Textes.

## Konfiguration überprüfen und speichern
{: #mo-save}

Überprüfen Sie die Zusammenfassung der von Ihnen getroffenen Auswahl und klicken Sie zum Fortfahren auf **Speichern**.

  ![Datentabelle auswählen](images/config-summary-monitor.png)

### Weitere Schritte
{: #mo-next}

Um mit der Konfiguration der Überwachungen zu beginnen, wählen Sie eine Kategorie aus und klicken Sie auf **Beginnen**.
