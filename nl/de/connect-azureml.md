---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Microsoft Azure, ml, machine learning, services

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

# Microsoft Azure ML Studio-Instanz angeben
{: #connect-azure}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Microsoft Azure ML Studio-Instanz an. In der Azure ML Studio-Instanz werden die AI-Modelle und -Bereitstellungen gespeichert.
{: shortdesc}

## Verbindung zu Azure ML Studio-Instanz herstellen
{: #ca-connect}

Von {{site.data.keyword.aios_short}} wird eine Verbindung zu AI-Modellen und -Bereitstellungen in einer Azure ML Studio-Instanz aufgebaut.

1.  Klicken Sie auf der Startseite des {{site.data.keyword.aios_short}}-Tools auf **Beginnen**.

    ![Startseite](images/gs-config-start.png)

1.  Wählen Sie die Kachel **Microsoft Azure ML Studio** aus und klicken Sie auf **Weiter**.

    ![Azure ML Studio auswählen](images/connect-azure.png)

1.  Geben Sie Ihre Berechtigungsnachweise ein:

    Anweisungen dazu, wie Sie Ihre Microsoft Azure-Berechtigungsnachweise abrufen, enthält die Anleitung [How to: Use the portal to create an Azure AD application and service principal that can access resources ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window}.
    {: note}

    ![Azure ML Studio-Berechtigungsnachweise eingeben](images/connect-azure-cred.png)

1.  Klicken Sie auf **Weiter**.

1.  {{site.data.keyword.aios_short}} zeigt eine Auflistung Ihrer bereitgestellten Modelle an. Wählen Sie diejenigen Modelle aus, die überwacht werden sollen.

    ![In MS Azure bereitgestellte Modelle auswählen](images/connect-azure-deploys.png)

1.  Klicken Sie auf **Weiter**.

### Weitere Schritte
{: #ca-next}

{{site.data.keyword.aios_short}} ist jetzt so eingerichtet, dass Sie Ihre [Datenbank angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db) können.
