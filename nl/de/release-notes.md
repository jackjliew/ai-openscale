---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: release notes, what's new 

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

# Neuerungen
{: #rn-relnotes}

In diesem Dokument werden neue Funktionen und bekannte Probleme für {{site.data.keyword.aios_full_notm}} beschrieben.
{: shortdesc}

## 5. März 2019
{: #rn-5March2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

### Neue Funktionen und Änderungen
{: #rn-5March2019nf}

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Vorgängerrelease hinzugefügt oder funktional erweitert:

- __*Neues Kreditrisikomodell*__: Es wird ein neues Modell 'Kreditrisiko' für alle Scoring-Engines unterstützt. Weitere Informationen enthalten die Abschnitte [Erste Schritte](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) und [Zusätzliche Ressourcen](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Berechnung der Verzerrungsbereinigung*__: Es ist möglich, zwischen Ihrem Produktionsmodell und einem von {{site.data.keyword.aios_short}} erstellten verzerrungsbereinigten Modell hin- und herzuschalten. Weitere Informationen enthalten die Abschnitte [Produktionsmodell und verzerrungsbereinigtes Modell](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) und [Funktionsweise der Verzerrungsbereinigung verstehen](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

## 22. Februar 2019
{: #rn-22February2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

### Neue Funktionen und Änderungen
{: #rn-22February2019nf}

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Vorgängerrelease hinzugefügt oder funktional erweitert:

- __*Aktualisierungen der Benutzerschnittstelle (UI)*__: Sie können eine JSON-Datei importieren, um alle Überwachungen und Funktionen während der Erstellung des Abonnements programmgestützt zu konfigurieren. Sie können die Konfigurationsdatei auch exportieren. Weitere Informationen enthält der Abschnitt [Bereitstellungsabonnement mithilfe von JSON-Dateien konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-cf-ov).

## 7. Februar 2019
{: #rn-7February2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

### Neue Funktionen und Änderungen
{: #rn-7February2019nf}

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Vorgängerrelease hinzugefügt oder funktional erweitert:

- __*Aktualisierungen der Benutzerschnittstelle (UI)*__: An der Benutzerschnittstelle von {{site.data.keyword.aios_short}} wurden mehrere Verbesserungen durchgeführt, unter anderem durch eine Möglichkeit, [Fairness und Genauigkeit bei Bedarf zu überprüfen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep), und die Möglichkeit, eine Liste von Transaktionen aus der [Diagramm mit Details zur Fairness](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Verbesserungen bei der Erklärbarkeit*__: Für alle Zahlen gilt nun dieselbe Genauigkeit/derselbe Maßstab bei relevanten positiven und relevanten negativen Werten.

- __*SSL-Unterstützung bei Db2*__: {{site.data.keyword.aios_short}} unterstützt die Übergabe von selbst signierten Zertifikaten (in Base64-Codierung) mit DB2-Berechtigungsnachweisen.

- __*Unterstützung der IBM Cloud-Datenbank*__: {{site.data.keyword.aios_short}} unterstützt jetzt zusätzlich zu Compose for PostgreSQL und Db2 auch Databases for PostgreSQL.

### Bekannte Probleme
{: #rn-7February2019ki}

- **Angepasste ML-Serviceinstanz**

    - Beim [Python-Modul](/docs/services/ai-openscale?topic=ai-openscale-as-module) funktioniert derzeit die Erklärbarkeit für die angepasste Serviceinstanz nicht. Das liegt daran, dass die angepasste Serviceinstanz eine numerische Vorhersage in den Antwortdaten erfordert, die nicht im Modulscript enthalten ist.

## 14. Dezember 2018
{: #rn-14December2018}

Die folgenden neuen Funktionen, Änderungen und bekannten Probleme bei dem Service sind verfügbar.

### Neue Funktionen und Änderungen
{: #rn-12nf}

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Beta-Release hinzugefügt oder funktional erweitert:

- __*Allgemeine Verfügbarkeit*__: Das GA-Release von {{site.data.keyword.aios_full_notm}} als IBM Cloud-Standardplan (gebührenpflichtig).

- __*IBM Cloud Private for Data V1.2*__: Wenn Sie {{site.data.keyword.aios_short}} auf IBM Cloud Private for Data V1.2 verwenden, lesen Sie hier die Dokumentation einschließlich Installationsanweisungen: [Installationscheckliste](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install).

- __*Unterstützung für Ihren Modelltyp*__: Zusätzlich zu den Bereitstellungen von AI-Modellen in Watson Machine Learning unterstützt {{site.data.keyword.aios_short}} Modellbereitstellungen in Microsoft Azure, Amazon SageMaker und angepassten Umgebungen. Weitere Informationen enthält der Abschnitt [Unterstützte Modelltypen](/docs/services/ai-openscale?topic=ai-openscale-in-ov).

- __*Kostenlose 'Lite'-Datenbank*__: Eine kostenlose verwaltete 'Lite'-Datenbank bietet alles, was Sie benötigen, um mit der Verwendung von {{site.data.keyword.aios_short}} beginnen zu können. Weitere Informationen enthalten die [Preispläne für {{site.data.keyword.aios_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/watson-openscale){: new_window}.

- __*Verzerrungsüberwachung*__: Unterstützung für geschützte Attribute vom Typ `float` und `double` sowie Verzerrungserkennung bei Modellen mit linearer Regression. {{site.data.keyword.aios_short}} kann außerdem automatisch eine Verzerrungsbereinigung für Ihr AI-Modell durchführen. Weitere Informationen enthält der Abschnitt [Fairness verstehen](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

- __*Erklärbarkeit*__: Unterstützung für Regressionsmodelle, Python-Funktionen sowie ergänzende kontrastierende Erklärungen. Weitere Informationen enthält der Abschnitt [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

- __*Datenspeicher*__: Qualitätsüberwachung, ohne auf Watson Machine Learning angewiesen zu sein, und die Möglichkeit, Ihre eigene Datenbank zu verwenden, ganz gleich, ob es sich um Db2, Postgres oder Db2 on Cloud handelt.

- __*NeuNetS (Beta)*__: IBM Neural Network Synthesizer (NeuNetS) ist als Betaversion verfügbar (nur öffentliche Cloud). Weitere Informationen enthält die [Dokumentation für NeuNetS ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}.

- __*Funktional erweiterte Benutzerschnittstelle (UI)*__: Die Benutzerschnittstelle (UI) für {{site.data.keyword.aios_short}} wurde verbessert und enthält jetzt eine Laufzeithistogrammverteilung mit der Funktion zum Umschalten für Trainingsdaten, Modell-ID & Versionierung und eine Tabelle mit Transaktions-IDs aus dem Histogramm. Weitere Informationen enthält der Abschnitt [Visualisierung von Daten für eine bestimmte Uhrzeit anzeigen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).

- __*Alternative Option zur Konfiguration des Lernprogramms*__: Um die Einrichtung und Konfiguration der erforderlichen IBM Cloud-Services zu automatisieren und eine IBM {{site.data.keyword.aios_full}}-Anwendung einschließlich Stichprobendaten anzuzeigen, können Sie ein Python-Modul installieren und ausführen. Näheres hierzu enthält [Python-Modul zum Konfigurieren von {{site.data.keyword.aios_short}} installieren](/docs/services/ai-openscale?topic=ai-openscale-as-module).

### Bekannte Probleme
{: #rn-12ki}

- **Microsoft Azure**

    - Von den beiden Arten von Azure Machine Learning-Web-Services wird nur der Typ `Neu` von {{site.data.keyword.aios_short}} unterstützt. Der Typ `Klassisch` wird nicht unterstützt.

    - __*Standardeingabename muss verwendet werden*__: Im Azure-Web-Service lautet der Standardeingabename `"input1"`. Dieses Feld ist gegenwärtig für {{site.data.keyword.aios_short}} bevollmächtigt und wenn es fehlt, funktioniert {{site.data.keyword.aios_short}} nicht.

      Wenn Ihr Azure-Web-Service nicht den Standardnamen verwendet, ändern Sie den Namen für das Eingabefeld in `"input1"`, dann funktioniert der Code.

- **AWS SageMaker**

    - __*BlazingText-Algorithmus wird nicht unterstützt*__: Das Format der Eingabenutzdaten für den AWS SageMaker BlazingText-Algorithmus wird in der aktuellen Version von {{site.data.keyword.aios_short}} nicht unterstützt.

## 17. September 2018
{: #rn-17September2018}

### Neue Funktionen und Änderungen
{: #rn-17nf}

- **Beta-Vorschauversion**: Willkommen bei der Beta-Vorschauversion von {{site.data.keyword.aios_full_notm}}.
