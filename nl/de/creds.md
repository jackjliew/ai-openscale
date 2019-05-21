---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Berechtigungsnachweise erstellen
{: #cred-create}

Um auf die {{site.data.keyword.aios_short}}-REST-APIs zugreifen zu können, sind ein Plattform-API-Schlüssel und eine Datamart-ID (Serviceinstanz-ID) erforderlich. Mit einem Plattform-API-Schlüssel wird ein einzelner Benutzer in die Lage versetzt, auf Ressourcen in der {{site.data.keyword.cloud_notm}} zuzugreifen.

Für Unternehmenskonten kann ein Administrator das Datamart erstellen und dann andere Benutzer in das Konto einladen und ihnen Zugriff auf ein bestimmtes {{site.data.keyword.aios_short}}-Datamart gewähren. Ein Benutzer kann dann seinen eigenen Plattform-API-Schlüssel erstellen und auf dasselbe {{site.data.keyword.aios_short}}-Datamart zugreifen. Dabei besteht kein Konflikt- oder Sicherheitsrisiko.

Führen Sie zum Erstellen eines Plattform-API-Schlüssels die folgenden Schritte aus:

- Melden Sie sich bei [{{site.data.keyword.cloud_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}){: new_window} an.

- Wählen Sie **Verwalten** --> **Sicherheit** --> **Plattform-API-Schlüssel** aus.

    ![Plattform-API-Schlüssel](images/cred-api-key.png)

- Erstellen und speichern Sie einen Plattform-API-Schlüssel.

Sie finden Sie Ihre Datamart-ID (oder Serviceinstanz-ID):

- Auf der Seite {{site.data.keyword.aios_short}} **Konfiguration --> Zusammenfassung** gibt der erste Eintrag Ihre Datamart-ID (bzw. Serviceinstanz-ID) an.

    ![Datamart-ID](images/data-mart-id.png)
