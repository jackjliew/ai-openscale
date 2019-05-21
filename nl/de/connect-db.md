---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-09"

keywords: databases, connections, scoring, requests

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

# Datenbank angeben
{: #connect-db}

Geben Sie eine Datenbank an, die von Ihrer {{site.data.keyword.aios_short}}-Instanz verwendet werden soll.
{: shortdesc}

## Verbindung zu Ihrer Datenbank herstellen
{: #cdb-connect}

{{site.data.keyword.aios_short}} verwendet eine Datenbank zum Speichern von Nutzdateninformationen, Feedbackdaten und Messdaten. Sie können nicht nur eine Datenbank auswählen, sondern bei Bedarf auch ein Schema für die ausgewählte Datenbank. Ein Schema ist eine benannte Sammlung (Gruppe) von Tabellen in der Datenbank.

1.  Wählen Sie eine Datenbank aus. Dabei stehen die folgenden beiden Optionen zur Auswahl: die Datenbank für den kostenlosen Lite-Plan oder eine vorhandene oder neue Datenbank.

    ![Datenbank auswählen](images/gs-config-database.png)

    Wenn Sie über ein gebührenpflichtiges {{site.data.keyword.cloud_notm}}-Konto verfügen, können Sie einen Service vom Typ `Databases for PostgreSQL` oder einen `Db2 Warehouse`-Service einrichten, um die Vorteile der Integration mit Watson Studio und Services für kontinuierliches Lernen optimal zu nutzen. Wenn Sie sich gegen die Einrichtung eines gebührenpflichtigen Service entscheiden, können Sie zwar den kostenlosen internen PostgreSQL-Speicher mit {{site.data.keyword.aios_short}} verwenden, aber Sie können kein kontinuierliches Lernen für Ihr Modell konfigurieren.
    {: note}

### Datenbank des kostenlosen Lite-Plans
{: #cdb-lite}

**HINWEIS**: Für die kostenlose Datenbank des Lite-Plans gelten einige wichtige Einschränkungen:

- Die kostenlose Lite Plan-Datenbank wird per Hosting bereitgestellt und es kann nicht direkt auf sie zugegriffen werden.
- {{site.data.keyword.aios_full}} hat uneingeschränkten Zugriff auf Ihre Datenbank und damit auch uneingeschränkten Zugriff auf Ihre Daten.
- Die kostenlose Datenbank des Lite-Plans ist nicht GDPR-konform. Wenn in Ihrem Modell personenbezogene Daten verarbeitet werden, können Sie die kostenlose Datenbank des Lite-Plans nicht verwenden. In diesem Fall müssen Sie eine neue Datenbank erwerben oder eine bestehende Datenbank verwenden, die GDPR-konform ist. Näheres zu diesem Thema enthält der Abschnitt [Informationssicherheit](/docs/services/ai-openscale?topic=ai-openscale-is-ov).

Um mit der Verwendung der kostenlosen Datenbank des Lite-Plans fortzufahren, wählen Sie einfach diese Option aus, überprüfen Sie dann die Zusammenfassung der Angaben und klicken Sie auf **Speichern**.

  ![Datenbank auswählen](images/gs-config-database2.png)

### Vorhandene oder neue Datenbank
{: #cdb-exn}

1.  Nachdem Sie die Option 'Vorhandene Datenbank verwenden oder neue Datenbank kaufen' ausgewählt haben, überprüft {{site.data.keyword.aios_short}} Ihr {{site.data.keyword.Bluemix_notm}}-Konto auf bereits vorhandene Datenbanken.

1.  Wählen Sie zunächst den Typ Ihrer vorhandenen Datenbank (Compose for Postgres, Database for Postgres oder Db2) aus und wählen Sie dann im Dropdown-Menü **Datenbank** eine Datenbank und anschließend ein **Schema** aus:

    Zum Speichern von Modellbereitstellungsausgaben und Retrainingdaten verwendet {{site.data.keyword.aios_short}} eine PostgreSQL- oder Db2-Datenbank. Lite-Pläne mit Db2 werden gegenwärtig nicht unterstützt.
    {: note}

    ![Datenbank auswählen](images/gs-config-database3.png)

1.  Sie können auch auf **Anderen Standort auswählen** auswählen, um eine Speicherposition der Datenbank außerhalb Ihres {{site.data.keyword.Bluemix_notm}}-Kontos anzugeben.

    Zum Speichern von Modellbereitstellungsausgaben und Retrainingdaten verwendet {{site.data.keyword.aios_short}} eine PostgreSQL- oder Db2-Datenbank. Lite-Pläne mit Db2 werden gegenwärtig nicht unterstützt.
    {: note}

    - Wählen Sie den **Datenbanktyp** aus (`Compose for PostgreSQL`, `Database for PostgreSQL` oder `Db2`) und geben Sie dann die Verbindungsinformationen an:

        - Wenn Sie eine `Compose for PostgreSQL`-Datenbank verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Hostname oder IP-Adresse
            - Port
            - Datenbank (Name)
            - Benutzername
            - Kennwort

            ![Standort einer Compose for PostgreSQL-Datenbank angeben](images/db-config-cpostgres.png)

        - Wenn Sie eine `Database for PostgreSQL`-Datenbank verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Hostname oder IP-Adresse
            - SSL-Port
            - Zertifikat mit Base64-Codierung
            - Datenbank (Name)
            - Benutzername
            - Kennwort

            ![Standort einer Database for PostgreSQL-Datenbank angeben](images/db-config-dpostgres.png)

        - Wenn Sie eine `Db2`-Datenbank verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Hostname oder IP-Adresse
            - SSL-Port
            - Datenbank (Name)
            - Benutzername
            - Kennwort

            ![Standort einer Db2-Datenbank angeben](images/db-config-db2.png)

    - Nach erfolgreicher Verbindungsherstellung können Sie ein Schema auswählen.

      Der Schemaname muss explizit angegeben werden, wenn Sie eine Db2-Instanz mit eingeschränktem Zugriff bereitstellen, denn in diesem Fall ist die automatische Generierung des Schemanamens nicht möglich. Dies betrifft den Db2 Warehouse-Einstiegsplan.
      {: important}

      ![Schema auswählen](images/gs-config-database5.png)

1.  Klicken Sie auf **Weiter**, überprüfen Sie die Zusammenfassung der Angaben und klicken Sie dann auf **Speichern**.

## Scoring-Anforderung senden
{: #cdb-score}

Zum Konfigurieren von Überwachungsprogrammen erfordert {{site.data.keyword.aios_short}}, dass Sie eine Scoring-Anforderung senden, um mit der Protokollierung der Daten zu beginnen, die künftig überwacht werden.

Für Modelle, die in Watson Machine Learning bereitgestellt sind, führt {{site.data.keyword.aios_short}} automatisch ein Scoring durch. Wenn Sie nur über Modelle verfügen, die in Watson Machine Learning bereitgestellt sind, wird diese Anzeige nicht angezeigt.
{: note:}

Wählen Sie eine Bereitstellung aus, in diesem Fall 'Fraud Detector' (Betrugserkennung), und verwenden Sie dann die bereitgestellten `cURL`- oder `Python`-Code-Snippets zum Protokollieren von Daten zu den Modellbereitstellungsanforderungen und Antwortdaten. Weitere Informationen enthält der Abschnitt [Nutzdatenprotokollierung für andere Serviceinstanzen als die Watson Machine Learning-Serviceinstanz](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Die Felder und Werte in den Code-Snippets müssen durch die tatsächlichen Werte ersetzt werden, da es sich bei den angegebenen Werten lediglich um Beispiele handelt.
{: important}

![Datenbank auswählen](images/config-send-scoring.png)

Nachdem Sie Ihre Nutzdatenprotokollierung ausgeführt haben, wird für die ausgewählte Bereitstellung in der Spalte 'Bereit zur Überwachung' ein Häkchen angezeigt. Klicken Sie zum Fortfahren auf **Überwachungen konfigurieren**.

## Weitere Schritte
{: #cdb-next}

{{site.data.keyword.aios_short}} ist jetzt so eingerichtet, dass Sie [Überwachungen für die Bereitstellungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config) können.
