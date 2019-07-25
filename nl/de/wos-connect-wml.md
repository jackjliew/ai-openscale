---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}-Serviceinstanz angeben
{: #wml-connect}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Instanz von {{site.data.keyword.pm_full}} an. In Ihrer {{site.data.keyword.pm_short}}-Instanz speichern Sie Ihre AI-Modelle und -Bereitstellungen.
{: shortdesc}

## Voraussetzungen
{: #wml-prereq}

Sie sollten in demselben {{site.data.keyword.Bluemix_notm}}-Konto, in dem die {{site.data.keyword.aios_short}}-Serviceinstanz vorhanden ist, eine {{site.data.keyword.pm_full}}-Instanz eingerichtet haben. Wenn Sie eine {{site.data.keyword.pm_full}}-Instanz in einem anderen Konto eingerichtet haben, können Sie diese Instanz nicht mit der automatischen Nutzdatenprotokollierung mit {{site.data.keyword.aios_short}} konfigurieren.

## {{site.data.keyword.pm_short}}-Serviceinstanz verbinden
{: #wml-config}

{{site.data.keyword.aios_short}} stellt die Verbindung zu AI-Modellen und Bereitstellungen in einer {{site.data.keyword.pm_full}}-Instanz her.

1.  Klicken Sie auf der Registerkarte **Konfigurieren** auf **Machine Learning-Anbieter**.

    ![Die Anzeige für die Auswahl des Machine Learning-Anbieters mit Kacheln für die unterstützten Machine Learning-Engines wird angezeigt.](images/wos-machine-learning-providers-selection.png)

2.  Wählen Sie die Kachel für {{site.data.keyword.pm_full}} aus. {{site.data.keyword.aios_short}} überprüft Ihr {{site.data.keyword.Bluemix_notm}}-Konto, um vorhandene {{site.data.keyword.pm_full}}-Instanzen zu finden. 
3. Wählen Sie eine Instanz in dem Dropdown-Menü für den **Watson Machine Learning-Service** aus.

    ![ {{site.data.keyword.pm_short}}-Service auswählen](images/gs-set-wml.png)

4.  (Optional) Sie haben auch die Möglichkeit, mit der Option **Anderen Standort auswählen** einen anderen ML-Standort außerhalb Ihres {{site.data.keyword.Bluemix_notm}}-Kontos anzugeben. Geben Sie die Berechtigungsnachweise für Ihren Standort in gültigem JSON-Format an:

    ![{{site.data.keyword.pm_short}}-Instanz festlegen](images/gs-get-wml.png)

    Klicken Sie auf **Speichern**.

1.  In {{site.data.keyword.aios_short}} sind die bereitgestellten Modelle aufgelistet. Wählen Sie die Modelle aus, die Sie überwachen möchten, und klicken Sie auf **Konfigurieren**.

### Weitere Schritte
{: #wml-next}

Nun können Sie in {{site.data.keyword.aios_short}} die [Überwachungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
