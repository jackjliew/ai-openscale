---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: deployment, monitors, data

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

# Überwachungen für eine Bereitstellung vorbereiten
{: #mo-config}

Richten Sie für jede Bereitstellung, die Sie mit {{site.data.keyword.aios_short}} verfolgen, Überwachungen ein und aktivieren Sie diese.
{: shortdesc}

Wenn Sie beispielsweise das **deutsche Kreditrisikomodell** für das interaktive Lernprogramm verwenden, wählen Sie die Modellbereitstellung aus, legen den Datentyp für die Nutzdatenprotokollierung fest und bestätigen die Einstellungen, die als Teil des Abschnitts für Modelldetails angezeigt werden.

## Bereitstellung auswählen
{: #mo-select-deploy}

1. Klicken Sie in der Registerkarte **Insights** auf die Schaltfläche **Zum Dashboard hinzufügen**. 

   Eine Liste der verfügbaren Modellbereitstellungen wird angezeigt. Wenn keine Modellbereitstellungen angezeigt werden, müssen Sie ein Modell mit Ihrem Machine Learning-Provider bereitstellen. Für das Lernprogramm wählen Sie das **deutsche Kreditrisikomodell** aus.

   ![Darstellung der Anzeige 'Modellbereitstellung auswählen', mit Auswahlmöglichkeiten für einen Machine Learning-Provider und eine Bereitstellung.](images/wos-select-model-deployment.png)

2. Klicken Sie auf eine Modellbereitstellung und anschließend auf **Konfigurieren**.

   Wenn es für ein bestimmtes Modell mehrere Bereitstellungen gibt, werden bei der Konfiguration einer Bereitstellung auch gleich alle anderen Bereitstellungen für genau dieses Modell konfiguriert.

   Nach dem Speichern Ihrer Auswahl können Sie Überwachungen konfigurieren, die die Protokollierung von Nutzdaten, Genauigkeit und Fairness einschließen. 

2. Klicken Sie auf **Überwachungen konfigurieren**, um damit zu beginnen.

## Details zur Nutzdatenprotokollierung angeben
{: #mo-work-data}

Sie müssen Informationen zu Ihrem Modell und zu Ihren Trainingsdaten angeben. Weitere Informationen zu Trainingsdaten finden Sie in [Warum benötigt {{site.data.keyword.aios_short}} Zugriff auf meine Trainingsdaten?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) Wählen Sie für das Lernprogramm im Feld **Datentyp** die Option **Numerisch/kategorial** und für **Algorithmustyp** die Option **Binäre Klassifizierung** aus.

![Darstellung der Anzeige 'Eingabetyp angeben' mit Auswahlmöglichkeiten für Datentyp und Algorithmustyp](images/config-what-monitor.png)

- Wenn Sie eine {{site.data.keyword.pm_full}}-Instanz verwenden, die sich in derselben Region wie die {{site.data.keyword.aios_short}}-Instanz befindet, müssen Sie zwar den Datentyp und den Algorithmustyp auswählen, es werden jedoch einige Angaben für die Nutzdatenprotokollierung automatisch für Sie konfiguriert. 
- Andernfalls müssen Sie auf der Registerkarte **Nutzdatenprotokollierung** und in den zugehörigen Fenstern Informationen zu Ihren Daten- und Algorithmustypen und zur Nutzdatenprotokollierung eingeben. 

   Je nach Auswahl gibt es bestimmte Anforderungen. Weitere Informationen hierzu finden Sie im Abschnitt [Numerische/kategoriale Daten](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan).

   Vor dem Konfigurieren der Überwachung müssen Sie ein auszuführendes Codefragment kopieren. Führen Sie den cURL-Befehl in Ihrer Clientanwendung oder den Python-Befehl in Ihrem Data-Science-Notebook aus. Auf diese Weise können Sie Modellbereitstellungsanforderungen und Antwortdaten in der Nutzdatendatenbank protokollieren.
   
Nach dem Senden der Details der Nutzdatenprotokollierung mithilfe der lokalen {{site.data.keyword.pm_full}}-Methode oder mithilfe der API müssen Sie zur Anzeige **Nutzdaten-Protokollierung** zurückkehren und auf **Fertig** klicken.

![Darstellung der Anzeige für Nutzdatenprotokollierung](images/payload-logging-gosales001.png)

Wenn das Scoring ordnungsgemäß an {{site.data.keyword.aios_short}} gesendet wurde, erscheint nach dem Klick auf die Schaltfläche **Fertig** die im Folgenden abgebildete Anzeige. Die Schaltfläche ist ausgeblendet und es wird eine Nachricht mit dem folgenden Inhalt angezeigt: **Protokollierung erfolgreich aktiviert**.

![Darstellung der Anzeige für die Nutzdatenprotokollierung nach dem erfolgreichen Hochladen von Daten](images/payload-logging-gosales002.png)


### Modelldetails angeben
{: #mo-work-model-dets}

Geben Sie Informationen zu Ihrem Modell an, damit {{site.data.keyword.aios_short}} auf die Datenbank zugreifen kann und über Angaben zur Konfiguration des Modells verfügt. Wenn Sie beispielsweise das **deutsche Kreditrisikomodell** für das interaktive Lernprogramm verwenden, werden viele der folgenden Felder automatisch für Sie ausgefüllt.

Sie müssen die folgenden Aufgaben ausführen, die insbesondere für die Überwachungskonfiguration von Bedeutung sind:

1. Geben Sie die Position der Trainingsdaten an. Geben Sie dazu die Position, den Hostnamen oder die IP-Adresse, den Datenbanknamen und die Authentifizierungsdaten ein.
2. Wählen Sie in der Datenbank die Trainingstabelle aus, indem Sie das Schema und die Tabelle auswählen.
3. Wählen Sie die Kennzeichnungsspalte in der Trainingstabelle aus, z. B. für das Lernprogramm, und klicken Sie auf die Kachel **Risiko**.
4. Wählen Sie die Merkmale aus, die zum Training der AI-Bereitstellung verwendet wurden.
5. Wählen Sie die Textmerkmale und die kategorialen Merkmale aus.
6. Wählen Sie die Spalte für Bereitstellungsvorhersage aus, z. B. für das Lernprogramm, und klicken Sie auf die Kachel **predictedLabel**.
7. Überprüfen Sie die Modelldetails gegebenenfalls, bevor Sie sie speichern.

In den folgenden Abschnitten werden bestimmte Informationen angezeigt, die Ihnen je nach Modelltyp ([numerische/kategoriale Daten](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan) oder [Bilder und unstrukturierter Text](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datai)) begegnen werden.


### Numerische/kategoriale Daten
{: #mo-nuca}

Bei numerischen oder kategorialen Daten müssen Sie Informationen zu den Trainingsdaten für Ihr Modell angeben, um die Überwachungen konfigurieren zu können.

- **Überwachungen manuell konfigurieren** - Erfordert die Angabe von Informationen für die Verbindungsherstellung zu Ihren Trainingsdaten.

    - Wählen Sie den [Algorithmustyp](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) aus und klicken Sie auf **Weiter**:

      Das Format der Trainingsdaten muss dem Modell entsprechen. Wenn das Modell z. B. `M` und `W` für das Merkmal `Geschlecht` erwartet, müssen die Trainingsdaten `M` und `W` enthalten und nicht `Männlich` und `Weiblich`.  Das aktuelle Release von {{site.data.keyword.aios_short}} unterstützt nur Db2-Datenbank und Cloud Object Storage als Speicherposition.
        {: important}

    - Geben Sie die Speicherposition an (entweder `Db2` oder `Cloud Object Storage`) und fahren Sie wie folgt fort:

        - Geben Sie für eine Db2-Datenbank die folgenden Angaben ein:

            - Hostname oder IP-Adresse
            - Port
            - Datenbank (Name)
            - Benutzername
            - Kennwort

        - Geben Sie für Cloud Object Storage die folgenden Angaben ein:

            - Anmelde-URL: Die Anmelde-URL muss der Regionseinstellung des Buckets entsprechen, in dem sich Ihre Trainingsdaten befinden. Die Angabe des Buckets mit den Trainingsdaten erfolgt im nächsten Schritt.
            - Ressourceninstanz (ID)
            - API-Schlüssel

    - Stellen Sie sicher, dass eine gültige Verbindung besteht, indem Sie auf die Schaltfläche **Testen** klicken, um eine Verbindung zu den Trainingsdaten herzustellen.
    - Geben Sie die genaue Position in der Db2-Datenbank oder in Cloud Object Storage an, an der sich die Trainingsdaten befinden.

        - Wählen Sie für eine Db2-Datenbank sowohl ein Schema als auch eine Trainingstabelle aus, die die von Ihrem Modell erwarteten Spalten enthält.
        - Wählen Sie für Cloud Object Storage ein Bucket und einen Datenbestand aus.

- **Konfigurationsdatei hochladen** - Wählen Sie diese Option aus, wenn Sie es vorziehen, dass Ihre Trainingsdaten privat bleiben. Sie können ein angepasstes Python-Notebook verwenden, um {{site.data.keyword.aios_short}} Informationen zur Analyse der Trainingsdaten bereitzustellen, jedoch ohne Zugriff auf die Daten selbst zu gewähren.

  Das Ausführen des Python-Notebooks ermöglicht Ihnen, verschiedene Werte in den Spalten des Schemas sowie die Namen der Spalten zu erfassen. Darüber hinaus können Sie mit dem Notebook die Überwachung der Fairness vorkonfigurieren.

   - Laden Sie das [angepasste Notebook](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external} herunter und ersetzen Sie alle Berechtigungsnachweise durch Ihre eigenen Berechtigungsnachweise.
   - Überprüfen Sie das Notebook sorgfältig und geben Sie gegebenenfalls Daten für Ihr Modell an. Speichern Sie das Notebook.
   - Führen Sie das Notebook aus, um eine mit JSON formatierte Konfigurationsdatei zu generieren.
   - Laden Sie die JSON-Konfigurationsdatei hoch.

     ![JSON-Konfigurationsdatei hochladen](images/config-json-monitor.png)

- Von {{site.data.keyword.aios_short}} werden die Trainingsdaten anhand der Metadaten gesucht, die mit dem Modell in {{site.data.keyword.pm_full}} gespeichert sind. Wählen Sie die Kennzeichnungsspalte in den Trainingsdaten aus, die Ihre Vorhersagewerte enthält.
- Wählen Sie die Spalten aus, die zum Trainieren des Modells verwendet werden. Dies sind die Merkmale, die Ihre Modellbereitstellung in einer Anforderung erwartet.
- Wählen Sie zum Schluss die Spalten aus, die Text enthalten und in Ganzzahlen umgewandelt wurden. Wenn die ursprünglichen Trainingsdaten `Male` und `Female` für `Gender` enthielten und diese Angaben nun den Werten `0` bzw. `1` zugeordnet wurden, enthalten die Trainingsdaten jetzt die Werte `0` und `1` für die Spalte `Gender`. Geben Sie solche Spalten an, die jetzt zwar Ganzzahlen enthalten, ursprünglich aber Textwerte enthielten.

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

Klicken Sie auf die Registerkarte **Qualität** und auf **Beginnen**, um mit der Konfiguration der Überwachungen fortzufahren. Weitere Informationen hierzu enthält der Abschnitt [Qualitätsüberwachung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
