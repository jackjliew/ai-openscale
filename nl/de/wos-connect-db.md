---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# Datenbank angeben
{: #connect-db}

Geben Sie eine Datenbank an, die von Ihrer {{site.data.keyword.aios_short}}-Instanz verwendet werden soll.
{: shortdesc}

## Verbindung zu Ihrer Datenbank herstellen
{: #cdb-connect}

{{site.data.keyword.aios_short}} verwendet eine Datenbank zum Speichern von Nutzdateninformationen, Rückmeldedaten und Messdaten. Sie können nicht nur eine Datenbank auswählen, sondern bei Bedarf auch ein Schema für die ausgewählte Datenbank. Ein Schema ist eine benannte Sammlung (Gruppe) von Tabellen in der Datenbank.

1.  Wählen Sie eine Datenbank aus. Dabei stehen die folgenden beiden Optionen zur Auswahl: die kostenlose Datenbank oder eine vorhandene oder neue Datenbank.

    ![Darstellung der Anzeige zur Datenbankauswahl mit den zwei Optionen zur Verwendung entweder des kostenlosen Lite-Plans oder einer vorhandenen Datenbank](images/gs-config-database.png)

    Wenn Sie über ein gebührenpflichtiges {{site.data.keyword.cloud_notm}}-Konto verfügen, können Sie einen Service vom Typ `Databases for PostgreSQL` oder einen `Db2 Warehouse`-Service einrichten, um die Vorteile der Integration mit Watson Studio und Services für kontinuierliches Lernen optimal zu nutzen. Wenn Sie sich gegen die Einrichtung eines gebührenpflichtigen Service entscheiden, können Sie zwar den kostenlosen internen PostgreSQL-Speicher mit {{site.data.keyword.aios_short}} verwenden, aber Sie können kein kontinuierliches Lernen für Ihr Modell konfigurieren.
    {: note}

### Datenbank des kostenlosen Lite-Plans
{: #cdb-lite}

**HINWEIS**: Für die kostenlose Datenbank gelten einige wichtige Einschränkungen:

- Die kostenlose Datenbank wird gehostet und ist für Sie nicht direkt zugänglich.
- {{site.data.keyword.aios_full}} hat uneingeschränkten Zugriff auf Ihre Datenbank und damit auch uneingeschränkten Zugriff auf Ihre Daten.
- Die kostenlose Datenbank ist nicht DSGVO-konform. Wenn von Ihrem Modell personenbezogene Angaben verarbeitet werden, dürfen Sie die kostenlose Datenbank nicht verwenden. In diesem Fall müssen Sie eine neue Datenbank erwerben oder eine bestehende Datenbank verwenden, den Regeln der DSGVO entspricht. Näheres zu diesem Thema enthält der Abschnitt [Informationssicherheit](/docs/services/ai-openscale?topic=ai-openscale-is-ov).

Wenn Sie mit der Verwendung der freien Datenbank fortfahren möchten, klicken Sie auf **Datenbank des kostenlosen Lite-Plans verwenden** und klicken Sie dann auf **Speichern**.

  ![Die Popup-Nachricht zur Datenbankspeicherung mit ausgewählter Schaltfläche zum Auswählen des Providers wird dargestellt](images/gs-config-database2.png)
  
Sie können für die kostenlose Datenbank ein Upgrade auf eine andere Datenbank durchführen. Es ist jedoch nicht möglich, eine Compose for Postgres-, Database for Postgres- oder Db2-Instanz für die kostenlose Datenbank zu konfigurieren. Es ist nicht möglich, nach dem Upgrade zur Verwendung der kostenlosen Datenbank zurückzukehren. Alle aktuellen Daten, wie z. B. die Konfiguration, die Scoring-Ergebnisse und die Erklärungen, können nicht wiederverwendet werden. Wenn Sie ein anderes Schema oder eine andere Datenbank auswählen, wird die {{site.data.keyword.aios_short}}-Umgebung vollständig zurückgesetzt.



### Vorhandene oder neue Datenbank
{: #cdb-exn}

1.  Nach Auswahl von **Vorhandene Datenbank verwenden oder neue Datenbank kaufen** überprüft {{site.data.keyword.aios_short}} Ihr {{site.data.keyword.Bluemix_notm}}-Konto auf bereits vorhandene Datenbanken.

1.  Wählen Sie zunächst den Typ Ihrer vorhandenen Datenbank (Compose for Postgres, Database for Postgres oder Db2) aus und wählen Sie dann im Dropdown-Menü **Datenbank** eine Datenbank und anschließend ein **Schema** aus:

    {{site.data.keyword.aios_short}} verwendet eine PostgreSQL- oder Db2-Datenbank zum Speichern modellbezogener Daten (Rückmeldedaten, Scoring-Nutzdaten) und berechneter Metriken. Lite-Pläne mit Db2 werden gegenwärtig nicht unterstützt. Weitere Informationen zu Trainingsdaten finden Sie in [Warum benötigt {{site.data.keyword.aios_short}} Zugriff auf meine Trainingsdaten?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
    {: note}

    ![Darstellung der Anzeige zur Datenbankauswahl, mit Feldern zur Eingabe von Datenbanktyp, Datenbanknamen und Schema.](images/gs-config-database3.png)

1.  Sie können auch auf **Anderen Standort auswählen** klicken, um eine Speicherposition der Datenbank außerhalb Ihres {{site.data.keyword.Bluemix_notm}}-Kontos anzugeben.

    {{site.data.keyword.aios_short}} verwendet eine PostgreSQL- oder Db2-Datenbank zum Speichern modellbezogener Daten (Rückmeldedaten, Scoring-Nutzdaten) und berechneter Metriken. Lite-Pläne mit Db2 werden gegenwärtig nicht unterstützt.
    {: note}

    - Wählen Sie den **Datenbanktyp** aus (`Compose for PostgreSQL`, `Database for PostgreSQL` oder `Db2`) und geben Sie dann die Verbindungsinformationen an:

        - Wenn Sie eine `Compose for PostgreSQL`-Datenbank verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Hostname oder IP-Adresse
            - Port
            - Datenbank (Name)
            - Benutzername
            - Kennwort

        - Wenn Sie eine `Database for PostgreSQL`-Datenbank verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Hostname oder IP-Adresse
            - SSL-Port
            - Zertifikat mit Base64-Codierung
            - Datenbank (Name)
            - Benutzername
            - Kennwort

        - Wenn Sie eine `Db2`-Datenbank verwenden, stellen Sie die entsprechenden Angaben für die folgenden Felder bereit:

            - Hostname oder IP-Adresse
            - SSL-Port
            - Datenbank (Name)
            - Benutzername
            - Kennwort

    - Nachdem Sie eine Verbindung hergestellt haben, können Sie ein Schema auswählen und Ihre Arbeit speichern.

      Der Schemaname muss explizit angegeben werden, wenn Sie eine Db2-Instanz mit eingeschränktem Zugriff bereitstellen, denn in diesem Fall ist die automatische Generierung des Schemanamens nicht möglich. Dies betrifft den Db2 Warehouse-Einstiegsplan.
      {: important}

## Weitere Schritte
{: #cdb-next}

{{site.data.keyword.aios_short}} ist jetzt so eingerichtet, dass Sie [Scoring-Nutzdaten senden](/docs/services/ai-openscale?topic=ai-openscale-cdb-score) und [Monitore für die Bereitstellungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config) können.
