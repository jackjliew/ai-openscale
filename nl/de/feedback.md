---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: feedback data, data, feedback, models

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

# Rückmeldedaten formatieren und in {{site.data.keyword.aios_short}} hochladen
{: #fmt-upld-fdbk-data}

Rückmeldedaten sind von zentraler Bedeutung, wenn sichergestellt werden soll, dass ein Modell keine Verzerrung aufweist. Sie müssen regelmäßig Rückmeldedaten in den {{site.data.keyword.aios_full}}-Service hochladen, um sicherzustellen, dass das Modell aktuelle Daten berücksichtigt, die auf Änderungen im Kontext Ihrer Prognoseanwendung hinweisen können. Eine Rückmeldungsschleife ermöglicht einem System das kontinuierliche Lernen durch die Überwachung der Effektivität von Prognosen und gegebenenfalls erforderliches erneutes Training. Die Überwachung und Verwendung der daraus resultierenden Rückmeldedaten sind ein zentraler Bestandteil der Machine Learning-Prozesse. Die folgenden Informationen sollen Sie bei der Formatierung und dem Upload der Rückmeldedaten unterstützen.
{: shortdesc}

## Rückmeldedaten formatieren
{: #fmt-upld-fdbk-data-fmt}

Damit Rückmeldedaten korrekt gelesen werden können, müssen sie korrekt formatiert sein. Der {{site.data.keyword.aios_short}}-Service akzeptiert die folgenden Formate: 

- CSV-Dateiformate, die über die Benutzerschnittstelle oder die REST-API hochgeladen werden können. 
- JSON-Dateiformate, die ausschließlich über die REST-API hochgeladen werden können. 

Diese Dateiformat werden durch ein Schema, `training_data_schema`, definiert, das in den Abonnementdetails verfügbar ist. Führen Sie zum Anzeigen des Schemas `training_data_schema` den folgenden Befehl über die Python-API aus: 

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

Sie können auch das Rückmeldedatenschema anzeigen, um es mit dem Trainingsdatenschema zu vergleichen. Führen Sie zum Anzeigen des Rückmeldedatenschemas den folgenden Befehl über die Python-API aus: 

```
subscription.feedback_logging.print_table_schema()
```


### CSV-Format
{: #fmt-upld-fdbk-data-fmt-csv}

In einer CSV-Datei werden die Daten typischerweise in Spalten und Zeilen angegeben, wobei eine Zeile für Spaltennamen vorgesehen ist. 

Wenn die Spaltennamen ausschließlich aus Großbuchstaben bestehen und damit für Db2 von der Groß-/Kleinschreibung unabhängig sind, sind normalerweise keine Anführungszeichen erforderlich. Bei anderen Datenbanken und bei Spaltennamen in Groß-/Kleinschreibung muss die Schreibweise übereinstimmen. Falls die Datei Spaltennamen enthält, müssen die Spalten nicht unbedingt der Tabellenreihenfolge entsprechen. Bei Dateien ohne Spaltennamen muss die Tabellenreihenfolge eingehalten werden. Es ist möglich, Spalten zu verwenden, die nicht in den ursprünglichen Trainingsdaten enthalten sind. Diese Spalten werden während der Verarbeitung ignoriert. 


### JSON-Format
{: #fmt-upld-fdbk-data-fmt-json}

Das JSON-Format besteht aus einer Sammlung von Objekten mit Feldern, die Spaltennamen entsprechen. 

