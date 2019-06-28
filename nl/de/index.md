---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Produktinformation
{: #in-ov}

{{site.data.keyword.aios_full}} ist eine auf Unternehmen abgestimmte Umgebung für von AI durchdrungene Anwendungen, die Unternehmen dahingehend Transparenz bietet, wie in der Größenordnung ihres Unternehmens AI konzipiert und genutzt wird und welchen Return-on-Investment sie liefern kann.
{: shortdesc}

<p>&nbsp;</p>

## Implementierung
{: #in-imp}

So implementieren Sie {{site.data.keyword.aios_short}}:

- **{{site.data.keyword.aios_short}} konfigurieren**: Mit der benutzerfreundlichen grafischen Umgebung werden Sie eine [Datenbank für die Nutzdatenprotokollierung einrichten](/docs/services/ai-openscale?topic=ai-openscale-connect-db) und die [Watson Machine Learning-Instanz angeben](/docs/services/ai-openscale?topic=ai-openscale-wml-connect), in der Ihre AI-Modelle und Bereitstellungen gespeichert sind.

- **Mit Überwachungen arbeiten**: Für jede Bereitstellung konfigurieren Sie, wie {{site.data.keyword.aios_short}} diese Bereitstellung überwachen wird. Sie können auf Folgendes überwachen:

    - [Fairness](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [Genauigkeit](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)
    - [Leistung](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics#anlz_metrics_performance)

- **Überwachte Daten anzeigen und bearbeiten**: Mit dem {{site.data.keyword.aios_short}} [-Dashboard](/docs/services/ai-openscale?topic=ai-openscale-io-ov) können Sie ohne großen Aufwand wichtige Einsichten visualisieren und Probleme bei Ihren Bereitstellungen aufdecken. Durch die Darstellung einzelner Datenpunkte für jedes überwachte Merkmal werden zusätzliche Details geliefert.

<p>&nbsp;</p>

## Einschränkungen
{: #in-lim}

- Das aktuelle Release unterstützt nur eine Datenbank, eine {{site.data.keyword.pm_full}}-Instanz und eine Instanz von {{site.data.keyword.aios_short}}.

- Die Datenbank und die {{site.data.keyword.pm_full}}-Instanz müssen in demselben {{site.data.keyword.cloud_notm}}-Konto bereitgestellt werden.

- Für den kostenlosen Lite-Plan gelten die folgenden monatlichen Grenzwerte:

    - Überwachung von zwei bereitgestellten Modellen
    - Erklärung von 20 Transaktionen
    - 50.000 Datensätze für Nutzdaten (kumulativ)
    - 50.000 Rückmeldedatensätze (kumulativ)

- {{site.data.keyword.aios_short}} verwendet eine PostgreSQL- oder Db2-Datenbank zum Speichern modellbezogener Daten (Rückmeldedaten, Scoring-Nutzdaten) und berechneter Metriken. Lite-Pläne mit Db2 werden gegenwärtig nicht unterstützt.

- Für Lizenzen gilt ein Grenzwert von 20 bereitgestellten Modellen pro Instanz von {{site.data.keyword.aios_short}}.

- Für {{site.data.keyword.pm_full}} können die Nutzdaten mit den durch Perturbation veränderten Images, die über das Machine Learning-Gateway gesendet werden, ein Volumen von 1 MB nicht überschreiten. Um Probleme aufgrund von Zeitlimitüberschreitungen zu vermeiden, dürfen Images nicht mehr als 125 x 125 Pixel aufweisen und sie müssen nacheinander gesendet werden, damit die Erklärung für das zweite Image angefordert wird, nachdem die erste abgeschlossen ist.


<p>&nbsp;</p>

## Bekannte Probleme
{: #rn-12ki}

- **Microsoft Azure**

    - Von den beiden Arten von Azure Machine Learning-Web-Services wird nur der Typ `Neu` von {{site.data.keyword.aios_short}} unterstützt. Der Typ `Klassisch` wird nicht unterstützt.

    - __*Standardeingabename muss verwendet werden*__: Im Azure-Web-Service lautet der Standardeingabename `"input1"`. Dieses Feld ist gegenwärtig für {{site.data.keyword.aios_short}} bevollmächtigt und wenn es fehlt, funktioniert {{site.data.keyword.aios_short}} nicht.

      Wenn Ihr Azure-Web-Service nicht den Standardnamen verwendet, ändern Sie den Namen für das Eingabefeld in `"input1"`, dann funktioniert der Code.

- **AWS SageMaker**

    - __*BlazingText-Algorithmus wird nicht unterstützt*__: Das Format der Eingabenutzdaten für den AWS SageMaker BlazingText-Algorithmus wird in der aktuellen Version von {{site.data.keyword.aios_short}} nicht unterstützt.

- **Angepasste ML-Serviceinstanz**

    - Beim [Python-Modul](/docs/services/ai-openscale?topic=ai-openscale-as-module) funktioniert derzeit die Erklärbarkeit für die angepasste Serviceinstanz nicht. Das liegt daran, dass die angepasste Serviceinstanz eine numerische Vorhersage in den Antwortdaten erfordert, die nicht im Modulscript enthalten ist.

<p>&nbsp;</p>

## Unterstützte Machine Learning-Engines und Frameworks
{: #in-fram}

Der {{site.data.keyword.aios_short}}-Service unterstützt die folgenden Machine Learning-Engines. Jede Laufzeit unterstützt Modelle, die in den folgenden Frameworks erstellt werden:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Angepasst](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS (nur ICP)](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

Die vollständige Unterstützung umfasst die folgenden Funktionen für das jeweilige Framework, das jeweilige Problem und den jeweiligen Datentyp:

- Protokollierung von Nutzdaten	
- Protokollierung von Rückmeldedaten	
- Genauigkeit der Leistung	
- Verzerrungserkennung zur Laufzeit	
- Erklärbarkeit	
- Automatische Verzerrungsbereinigung

<p>&nbsp;</p>

## Browserunterstützung
{: #in-brw}

Für die Tools des {{site.data.keyword.aios_short}}-Service ist dieselbe Browsersoftware erforderlich wie für {{site.data.keyword.cloud_notm}}. Genaueres hierzu enthält der Abschnitt {{site.data.keyword.cloud_notm}} [Voraussetzungen](/docs/overview?topic=overview-prereqs-platform#browsers-platform).

<p>&nbsp;</p>

## CLI-Tool für ModelOps
{: #in-mop}

Das [{{site.data.keyword.aios_short}}-CLI-Tool für Modelloperationen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} ermöglicht Ihnen die Ausführung von Tasks, die sich auf das Lebenszyklusmanagement von Machine Learning-Modellen beziehen. Dieses Tool ergänzt das {{site.data.keyword.cloud_notm}}-CLI-Tool und ist mit dem [Machine Learning-Plug-in ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window} erweitert.

<p>&nbsp;</p>

## Python-Client
{: #in-pyc}

Der [Python-Client für {{site.data.keyword.aios_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://ai-openscale-python-client.mybluemix.net/){: new_window} ist eine Python-Bibliothek, die Ihnen ermöglicht, direkt mit dem {{site.data.keyword.aios_short}}-Service in {{site.data.keyword.cloud_notm}} zu arbeiten. Anstelle der Benutzerschnittstelle des {{site.data.keyword.aios_short}}-Clients können Sie den Python-Client verwenden, um eine Datenbank für die Protokollierung direkt zu konfigurieren, Ihre Machine Learning-Engine zu binden und Bereitstellungen auszuwählen und zu überwachen. Beispiele für die Verwendung des Python-Clients auf diese Weise enthält der Abschnitt [{{site.data.keyword.aios_short}}-Beispielnotizbücher ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Weitere Schritte
{: #in-next}

- Machen Sie Ihre [ersten Schritte](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) mit dem Service.
- Sichten Sie das [Referenzmaterial für die API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/ai-openscale){: new_window}.

Haben Sie immer noch offene Fragen? 

- [Neuerungen](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- Dann können Sie sich [an IBM wenden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
