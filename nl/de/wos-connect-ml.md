---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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

# Nutzdatenprotokollierung für andere Serviceinstanzen als die {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}-Serviceinstanz
{: #cml-connect}

Wenn ein AI-Modell in einer anderen Machine Learning-Engine als {{site.data.keyword.pm_full}} bereitgestellt wird, müssen Sie die Nutzdatenprotokollierung für die externe Machine Learning-Engine mit einem Python-Client aktivieren.
{: shortdesc}

Ausführlichere Informationen finden Sie in der [Dokumentation zum Python-Client für {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} und in den Beispielnotebooks für den Python-Client für {{site.data.keyword.aios_short}}, die Bestandteil der [{{site.data.keyword.aios_short}}-Lernprogramme](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external} sind.

## Vorbereitende Schritte
{: #cml-prereq}

Die Trainingsdaten des Modells müssen in Db2 oder {{site.data.keyword.cos_full}} zur Überwachung der Verzerrung für das Modell verfügbar sein. Erklärbarkeit und Genauigkeit werden für Python-Funktionen nicht unterstützt. Weitere Informationen zu den Trainingsdaten finden Sie unter [Warum muss {{site.data.keyword.aios_short}} auf meine Trainingsdaten zugreifen?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- {{site.data.keyword.aios_short}} importieren und initialisieren

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  Berechtigungsnachweise können durch Ausführen der Schritte im Abschnitt "[Berechtigungsnachweise erstellen](/docs/services/ai-openscale?topic=ai-openscale-cred-create)" erstellt bzw. ermittelt werden.

- Schemanamen in Ihrer PostgreSQL-Datenbank erstellen

- Datamart einrichten

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## Weitere Schritte
{: #cml-next}

- Informationen zum Fortfahren mit dem {{site.data.keyword.aios_short}}-Client finden Sie unter [Genauigkeits- oder Qualitätsüberwachung konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Informationen zum Fortfahren mit der Python-Befehlsbibliothek enthält die [Dokumentation zum Python-Client](http://ai-openscale-python-client.mybluemix.net/){: external}.
