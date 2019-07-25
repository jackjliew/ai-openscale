---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Nutzdatenprotokollierung automatisieren
{: #fmrk-workaround-pyld-lg}

Die automatische Nutzdatenprotokollierung beim Datenverkehr zwischen {{site.data.keyword.aios_full}} und {{site.data.keyword.pm_full}} erfolgt, wenn beide Produkte in demselben {{site.data.keyword.Bluemix_notm}}-Konto bereitgestellt werden. Sie können die Nutzdatenprotokollierung auch für andere Machine Learning-Anbieter und für eine {{site.data.keyword.pm_full}}-Instanz automatisieren, die nicht zu demselben Konto gehört. Orientieren Sie sich dazu an einem der folgenden Fälle und verwenden Sie die entsprechenden Optionen:
{: shortdesc}

### Fall 1: Das ursprüngliche Format der Scoring-Eingabe und -Ausgabe bleibt erhalten (anders als {{site.data.keyword.aios_short}} erfordert)
{: #fmrk-workaround-case1}

Wenn Ihre Anwendungen eine ursprünglich Nutzdatenformat verwenden, das nicht geändert werden kann, wählen Sie eine der folgenden Optionen aus:

- Option 1: Der Scoring-Endpunkt der angepassten Machine Learning-Engine sollte beide Nutzdatenformate akzeptieren. 

   Je nach Nutzdatenformat: Bei Nutzdaten in {{site.data.keyword.aios_short}}-Format (ähnlich wie {{site.data.keyword.pm_full}}) oder in Benutzerformat wird die Ausgabe im entsprechenden Format zurückgegeben. Bei Verwendung des Benutzerformats als Format müssen Sie eine Konvertierung in das {{site.data.keyword.aios_short}}-Format vornehmen und die Daten anschließend als in der Nutzdatenprotokollierungstabelle als Datensätze für Nutzdaten speichern. Speichern Sie bei Verwendung des {{site.data.keyword.aios_short}}-Formats als Format für die Scoring-Eingabe die Nutzdaten nicht, denn diese Nutzdaten stammen von {{site.data.keyword.aios_short}} und nicht vom Benutzer.

   Weitere Informationen enthält der Abschnitt [Zwei Nutzdatenformate verwenden](/docs/services/ai-openscale?topic=ai-openscale-integrating-3rd-party-ml-engines-with-watson-openscale#fmrk-workaround-notsuppt).

- Option 2: Sollte die Einbettung einer solchen Logik in einen einzigen REST-API-Endpunkt aus einem beliebigen Grund nicht möglich sein, können Sie zwei Endpunkte definieren. 

   Einer der beiden Endpunkte wird von Ihrer Anwendung verwendet. Sie müssen jedoch die Protokollierung der Nutzdaten hinzufügen und die Konvertierung in das erwartete Format vornehmen. Der zweite Endpunkt wird von {{site.data.keyword.aios_short}} verwendet, um erforderliche Berechnungen wie etwa die Verzerrung oder die Erklärbarkeit durchzuführen. Für diesen Endpunkt ist keine Nutzdatenprotokollierung erforderlich. Während der Konfiguration von {{site.data.keyword.aios_short}} sollte der zweite Endpunkt auf denjenigen mit kompatiblen Formaten verweisen.

   Weitere Informationen hierzu enthält [Zwei Endpunkte verwenden](/docs/services/ai-openscale?topic=ai-openscale-integrating-3rd-party-ml-engines-with-watson-openscale#fmrk-workaround-opt2-cs1).

- Option 3: Sie verschieben das Modul für die Nutzdatenprotokollierung zum ursprünglichen Endpunkt oder zur nachgeordneten Anwendung. 

   Sofern Ihre Anwendung diese Option unterstützt, muss lediglich ein Endpunkt auf der angepassten Machine Learning-Engine entwickelt werden, nämlich der Endpunkt für {{site.data.keyword.aios_short}}.

### Fall 2: Sie arbeiten mit dem Nutzdatenformat, das {{site.data.keyword.aios_short}} erfordert.
{: #fmrk-workaround-case2}

In diesem Fall ist es nicht erforderlich, eine Konvertierung vom Benutzerformat (Scoring-Ein-/Ausgabe) in das für {{site.data.keyword.aios_short}} erforderliche Format vorzunehmen.

Da es nicht wünschenswert ist, dass die internen Scoring-Anfragen als Benutzernutzdaten protokolliert werden (Berechnungen von {{site.data.keyword.aios_short}}), müssen Sie entweder zwei Endpunkte entwickeln oder zusätzliche Logik für einen einzelnen Endpunkt codieren.

- Option 1: Zwei Endpunkte. Diese Option hat sehr starke Ähnlichkeit mit Option 2 in Fall 1. Der einzige Unterschied besteht darin, dass keine Notwendigkeit für Formatkonvertierungen besteht, da deren Ausrichtung bereits erfolgt ist.

- Option 2: Einzelner Endpunkt. Es muss festgestellt werden, ob die Scoring-Anforderung von der Benutzeranwendung kommt. Dies kann erzielt werden, indem einige zusätzliche Informationen in den Scoring-Nutzdaten (bzw. Metadaten) gesendet werden. Werden solche Metadaten erkannt, sollten die Nutzdaten protokolliert werden.

## Zwei Nutzdatenformate verwenden
{: #fmrk-workaround-notsuppt}

Nehmen Sie an, dass Sie das Angebot von XYZ verwenden, um die Modelle zu bedienen. XYZ wird von diesem Zeitpunkt von {{site.data.keyword.aios_short}} nicht unterstützt.

Sie verwenden zahlreiche nachgeordnete Anwendungen, die die Bereitstellungen auf XYZ verbrauchen, und Sie können das Format der Scoring-Nutzdaten nicht ändern. Es ist jedoch möglich, Änderungen an der Logik des Scoring-Endpunkts vorzunehmen.

### Schritte

1. Entwickeln Sie eine angepasste Machine Learning-Engine, die die XYZ-Bereitstellung einschließt.
2. Implementieren Sie den Scoring-Endpunkt auf der angepassten Machine Learning-Engine, sodass die Nutzdatenformate sowohl für XYZ als auch für {{site.data.keyword.aios_short}} unterstützt werden.
3. Fügen Sie die Logik zur Erkennung des Formats der Nutzdaten im Scoring-Endpunkt auf Ihrer angepassten Machine Learning-Engine hinzu.
4. Wenn die Nutzdaten von nachgeordneten Apps stammen, konvertieren Sie sie in das {{site.data.keyword.aios_short}}-Format und protokollieren Sie sie in {{site.data.keyword.aios_short}} als Datensätze für Nutzdaten.
5. Wechseln Sie von den Scoring-Endpunkten der nachgeordneten Apps zu dem neu von Ihnen erstellten Scoring-Endpunkt.

Wenn die URL des Scoring-Endpunkts erhalten bleiben soll, verwenden Sie die URL-Weiterleitung, die auch als Proxy bezeichnet wird.

## Zwei Endpunkte verwenden
{: #fmrk-workaround-opt2-cs1}

Wenn das Format Ihrer Nutzdaten nicht geändert werden kann, weil dadurch zum Beispiel die Funktion nachgeordneter Anwendungen unterbrochen würden, müssen Sie getrennte Endpunkte verwenden. Dieser Ansatz bezieht die folgenden Komponenten ein:

- Scoring-Endpunkt (im Format des Benutzers) mit dem ursprünglichen Scoring-Endpunkt unter Verwendung des benutzerdefinierten Formats für Eingabe und Ausgabe
- Angepasste Machine Learning-Engine mit Perturbationsendpunkt ({{site.data.keyword.aios_short}}-Format) und mit Erkennungsendpunkt. Der Perturbationsendpunkt schließt den ursprünglichen Scoring-Endpunkt ein und nimmt Konvertierungen aus dem {{site.data.keyword.aios_short}}-Format in das Benutzerformat und aus dem Benutzerformat in das {{site.data.keyword.aios_short}}-Format vor. Dies ist erforderlich, damit {{site.data.keyword.aios_short}} korrekte Scoring-Anforderungen stellen und die Ausgabe verstehen kann.
- Scoring-Endpunkt-Wrapper mit Nutzdatenprotokollierungsfunktion. Dieser Wrapper wird anstatt vom ursprünglichen Scoring-Endpunkt von einer nachgeordneten Anwendung verarbeitet wird. Ihre Logik wurde um die Funktion der Nutzdatenprotokollierung erweitert. Jedes Mal, wenn eine Scoring-Anforderung ausgeführt wird, werden die Ein- und die Ausgabe in das {{site.data.keyword.aios_short}}-Format konvertiert und protokolliert.

Das folgende Flussdiagramm zeigt eine Lösung mit einer angepassten Machine Learning-Engine, bei der die angepasste Machine Learning-Engine die Endpunkte für Perturbation (Störung durch Verfremdung) und Erkennung abwickelt und die Umsetzung in Ihr Format übernimmt:

![Spezifikation der REST-API-Endpunkte](images/woscustommlworkflow.png)

### Schritte
{: #fmrk-workaround-smple-cd}

1. Verwenden Sie ein Notebook, um einen Scoring-Endpunkt für die Bereitstellung des Modells 'Kreditrisiko'(scikit-learn) auf dem Microsoft Azure Machine Learning-Service zu erstellen. Weitere Informationen hierzu finden Sie in [diesem Beispielnotebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb).
2. Erstellen Sie eine angepasste Machine Learning-Engine und stellen Sie sie unter Microsoft Azure Cloud als Flask-Anwendung zur Verfügung. Erstellen Sie den Perturbations- und den Erkennungsendpunkt. Weitere Informationen hierzu finden Sie in [diesen Bereitstellungsanweisungen](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure).
3. Konfigurieren Sie {{site.data.keyword.aios_short}} für die Zusammenarbeit mit der angepassten Machine Learning-Engine. Weitere Informationen hierzu finden Sie in [diesem Beispielnotebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb).
4. Erstellen Sie einen Scoring-Endpunkt-Wrapper, der die Protokollierung der Nutzdaten auf dem Microsoft Azure Machine Learning-Service automatisiert. Weitere Informationen hierzu finden Sie in [diesem Beispielnotebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb).

Achten Sie besonders auf die folgenden Punkte:

- Berechtigungsnachweise: Damit das Lernprogramm einfach nachvollzogen werden kann, sind die Berechtigungsnachweise für {{site.data.keyword.aios_short}} im Code (Scoring-Endpunkt-Wrapper) fest codiert. Diese Werte müssen Sie durch Ihre tatsächlichen Berechtigungsnachweise ersetzen.
- Python SDK gegenüber REST API: Das Lernprogramm verwendet das Python-SDK zum Protokollieren der Nutzdaten. Dazu könnten Sie auch die REST-API verwenden, jedoch müssen Sie das Token eigenständig generieren oder aktualisieren. 
- {{site.data.keyword.cloud_notm}} im Gegensatz zu Cloud Pak for Data: Wenn Sie {{site.data.keyword.wos4d_notm}} verwenden, befinden sich die Berechtigungsnachweise [hier im Beispielnotebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb) in einem anderen Format. Die {{site.data.keyword.aios_short}}-Clientklasse ist ebenfalls eine andere. Es wird die Clientklasse `APIClient4ICP` verwendet.
- Protokollierung von Nutzdaten als getrennter Endpunkt/getrenntes Paket - Extraktion der Protokollierungs- TWBAMP; Konvertierungsverfahren in eigenes Paket oder eigenen Endpunkt. Auf diese Weise ist eine Wiederverwendung möglich, wenn Sie ein Batch von Nutzdaten außerhalb des Scoring-Endpunkt-Wrappers einfügen möchten.

