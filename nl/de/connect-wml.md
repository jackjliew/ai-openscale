---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Watson Machine Learning-Serviceinstanz angeben
{: #wml-connect}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Watson Machine Learning-Instanz (WML-Instanz) an. In Ihrer WML-Instanz speichern Sie Ihre AI-Modelle und -Bereitstellungen.
{: shortdesc}

## Voraussetzungen
{: #wml-prereq}

Sie sollten in demselben {{site.data.keyword.Bluemix_notm}}-Konto, in dem die {{site.data.keyword.aios_short}}-Serviceinstanz vorhanden ist, eine WML-Instanz eingerichtet haben. Sollten Sie eine WML-Instanz in einem anderen Konto eingerichtet haben, so werden Sie diese Instanz nicht mit {{site.data.keyword.aios_short}} konfigurieren können.

## Watson Machine Learning-Serviceinstanz verbinden
{: #wml-config}

{{site.data.keyword.aios_short}} stellt die Verbindung zu AI-Modellen und Bereitstellungen in einer WML-Serviceinstanz her.

1.  Klicken Sie auf der Startseite des {{site.data.keyword.aios_short}}-Tools auf **Beginnen**.

    ![Startseite](images/gs-config-start.png)

2.  Wählen Sie die Kachel **Watson Machine Learning** aus.

    ![Auswahl der Kachel](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} überprüft Ihr {{site.data.keyword.Bluemix_notm}}-Konto, um vorhandene WML-Instanzen zu finden. Sie können dann eine Instanz aus dem Dropdown-Menü für den **Watson Machine Learning-Service** auswählen.

    ![WML-Service auswählen](images/gs-set-wml.png)

4.  (Optional) Sie haben auch die Möglichkeit, mit der Option **Anderen Standort auswählen** einen anderen ML-Standort außerhalb Ihres {{site.data.keyword.Bluemix_notm}}-Kontos anzugeben. Geben Sie die Berechtigungsnachweise für Ihren Standort in gültigem JSON-Format an:

    ![WML-Instanz einrichten](images/gs-get-wml.png)

    Klicken Sie auf **Weiter**.

5.  {{site.data.keyword.aios_short}} überprüft die ausgewählte Machine Learning-Instanz, um eine Liste der in dieser Instanz gespeicherten Bereitstellungen zu finden. Wählen Sie in der Liste der Bereitstellungen diejenigen aus, die Sie künftig überwachen werden.

    ![Bereitstellungen auswählen](images/gs-config-deploy.png)

6.  Klicken Sie auf **Weiter**.
7.  Klicken Sie auf **Speichern**.

### Weitere Schritte
{: #wml-next}

{{site.data.keyword.aios_short}} ist jetzt so eingerichtet, dass Sie eine [Datenbank angeben](/docs/services/ai-openscale?topic=ai-openscale-connect-db) können.
