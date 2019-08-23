---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: release notes, what's new 

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

# Neuerungen
{: #rn-relnotes}

In diesem Dokument werden neue Funktionen für {{site.data.keyword.aios_full_notm}} beschrieben.
{: shortdesc}

## 9. Juli 2019
{: #rn-9jul2019}

Die folgenden neuen Funktionen und Änderungen sind für {{site.data.keyword.aios_short}} verfügbar.

- __*Aktualisierte und erweiterte Onlinehilfe*__: Die {{site.data.keyword.aios_short}}-Onlinehilfe wurde kürzlich neu organisiert, um die Suche nach Themen über das Inhaltsfenster zu erleichtern. Darüber hinaus wurden viele neue Themen verfasst und erweitert.

   Weitere Informationen finden Sie in den Abschnitten [Insights abrufen](/docs/services/ai-openscale?topic=ai-openscale-io-ov) und [{{site.data.keyword.aios_short}} von einem Lite- auf einen gebührenpflichtigen Plan aktualisieren](/docs/services/ai-openscale?topic=ai-openscale-cf-upgrade).
   
## 02. Juli 2019
{: #rn-2jul2019}

Die folgenden neuen Funktionen und Änderungen sind für {{site.data.keyword.aios_short}} verfügbar.

- __*Drift-Erkennung*__: ![Beta-Tag](images/beta.png)

  {{site.data.keyword.aios_short}} unterstützt jetzt die Drifterkennung.

   Weitere Informationen finden Sie im Abschnitt [Drifterkennung](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr).

- __*Microsoft Azure ML Service-Unterstützung*__: {{site.data.keyword.aios_short}} unterstützt jetzt Microsoft Azure ML Service, das die Integration der AI-Modelle von Microsoft Azure ML Service mit Fairness, Genauigkeit und Erklärbarkeit von {{site.data.keyword.aios_short}} ermöglicht.

   Weitere Informationen finden Sie im Abschnitt [Microsoft Azure ML Service-Frameworks](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service).

- __*Verbesserter Workflow*__: Ein besonderer Schwerpunkt wurde von {{site.data.keyword.aios_short}} auf die Verbesserung des Workflows gelegt, sodass Sie Ihre Arbeit nun umgehend mit weniger Klicks und mehr erklärenden Informationen erledigen können. Das Navigationsfenster zeigt an, an welchem Punkt Sie sich befinden, und ermöglicht es Ihnen, zwischen Konfigurationsaufgaben hin- und herzuspringen.

   Weitere Informationen hierzu finden Sie im Abschnitt [Überwachungen für eine Bereitstellung vorbereiten](/docs/services/ai-openscale?topic=ai-openscale-mo-config).

- __*Mehrere Machine Learning-Provider*__: Warum sollte man an einen einzigen Machine Learning-Provider oder eine einzige Machine Learning-Engine gebunden sein? Mit der neuesten Version von {{site.data.keyword.aios_short}} können Sie mehrere Anbieter hinzufügen, damit Sie von den jeweiligen Vorteilen profitieren und bei veralteten Versionen von Apps für Kontinuität sorgen können.

   Weitere Informationen hierzu enthält der Abschnitt [Unterstützung für mehrere Machine Learning-Engines](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng).

- __*Weitere Out-of-the-box Metriken*__: Die neue Version von {{site.data.keyword.aios_short}} beinhaltet viele neue Fairness-, Qualitäts-, Leistungs- und Analysemetriken. Sie können aus dem Vollen schöpfen!

   Weitere Informationen hierzu finden Sie im Abschnitt [Übersicht zu Qualitätsmetriken](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics). Klicken Sie sich danach durch die übrigen Abschnitte: [Fairness](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness), [Leistung](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through), [Analyse](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload) und [Verhalten](/docs/services/ai-openscale?topic=ai-openscale-behavior-ovr).

- __*Verzerrungsabwicklung im Eiltempo*__: Empfohlene Fairnessattribute und automatische Werte für die Verzerrungskonfiguration erleichtern es zu erkennen, an welchen Punkten {{site.data.keyword.aios_short}} potenzielle Verletzungen von Schwellenwerten für Fairness im Modell erkennt. Die Entscheidung, ob Sie die empfohlenen zu überwachenden Merkmale akzeptieren oder die Werte ändern, liegt bei Ihnen.

   Weitere Informationen hierzu enthält der Abschnitt [Übersicht zu Fairnessmetriken](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness).

## 11. Juni 2019
{: #rn-11June2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

- __*Aktualisierte Dashboard-Funktionalität*__: Das {{site.data.keyword.aios_short}}-Dashboard wurde mehreren Überarbeitungen unterzogen. Diese neue Version beinhaltet die folgenden Verbesserungen:

    - Vereinfachung der Suche nach Ressourcen wie StackOverflow oder IBM Support durch eine neue Hilfeanzeige 
    - Aktivierung der Globalisierung für das Dashboard
    - Verbesserungen der Benutzerfreundlichkeit durch funktionale Erweiterungen

## 7. Juni 2019
{: #rn-7June2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

- __*Funktional erweiterte Befehlszeilenschnittstelle*__: Die Befehlszeilenschnittstelle ibm-ai-openscale-cli wurde aktualisiert und Version 0.2.148 wurde nun freigegeben. Diese neue Version beinhaltet die folgenden Verbesserungen:

    - Aktualisierung des Verlaufsprotokolls für Qualitätsmetriken, sodass nun das gesamte Sortiment der von OpenScale unterstützten neuen Qualitätsmetriken einbezogen wird
    - Unterstützung der Angabe eines SSL-Zertifikats direkt bei Verwendung von IBM Db2
    - Unterstützung für das neue Python-SDK für ibm-ai-openscale 2.1.8
    - Sonstige Fehlerkorrekturen und Verbesserungen der Stabilität

   Die Installation über PyPI ist durch Ausführen des Befehls `pip install -U ibm-ai-openscale-cli` möglich. Hilfe zur Syntax kann durch Ausführen des Befehls `ibm-ai-openscale-cli --help` abgerufen werden. Weitere Informationen finden Sie auf der [PyPI-Projektseite](https://pypi.org/project/ibm-ai-openscale-cli).

## 29. Mai 2019
{: #rn-29May2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

- __*Erweiterungen für die Visualisierung für Verzerrungen*__: ![Beta-Tag](images/beta.png) Die Visualisierung für Verzerrungen umfasst die folgenden Ansichten: 

    - Nutzdaten + durch Perturbation veränderten Daten: Enthält die für die ausgewählte Stunde erhaltene Scoring-Anforderung sowie zusätzliche Datensätze für vorherige Stunden, falls die für die Bewertung erforderliche Mindestanzahl von Datensätzen nicht erreicht wurde. Darüber hinaus sind zusätzliche durch Perturbation veränderte/synthetisierte Datensätze enthalten, die dazu verwendet werden, die Antwort des Modells zu testen, wenn sich der Wert des überwachten Merkmals ändert.
    - Nutzdaten: Die tatsächlichen Scoring-Anforderungen, die das Modell für die ausgewählte Stunde erhält.
    - Trainingsdaten: Die Trainingsdatensätze, die für das Training des Modells verwendet werden.
    - Verzerrungsbereinigte Daten: Die Ausgabe des Verzerrungsbereinigungsalgorithmus nach der Verarbeitung der Laufzeitdaten und der durch Perturbation veränderten Daten.

   Weitere Informationen hierzu enthält der Abschnitt [Visualisierung für Verzerrungen](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz).

- __*Genauigkeitsberechnung für verzerrungsbereinigte Ausgabe*__: Die Genauigkeitsberechnung bezieht auch die verzerrungsbereinigte Ausgabe ein. Sie können die Genauigkeit des verzerrungsbereinigten Modells mit der Genauigkeit eines Produktionsmodells vergleichen.

   Weitere Informationen hierzu enthält der Abschnitt [Genauigkeit](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view).

- __*Unterstützung für mehrere Machine Learning-Engines*__: {{site.data.keyword.aios_short}} unterstützt mehrere Machine Learning-Engines innerhalb einer einzelnen Instanz, vorausgesetzt, dass die Bereitstellung über das [Python-SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) erfolgt.

   Weitere Informationen hierzu enthält der Abschnitt [Unterstützung für mehrere Machine Learning-Engines](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng).

- __*Internationalisierungsunterstützung*__: {{site.data.keyword.aios_short}} unterstützt lokalisierte Versionen und umfasst die Verarbeitung von Daten in unterstützten Sprachen. Die Benutzerschnittstelle, die Dokumentation und die Fehlernachrichten von {{site.data.keyword.aios_short}} werden derzeit in die folgenden Sprachen übersetzt: 
    - Deutsch
    - Französisch
    - Italienisch
    - Spanisch
    - Portugiesisch (Brasilien)
    - Japanisch
    - Vereinfachtes Chinesisch
    - Traditionelles Chinesisch
    - Koreanisch

   Weitere Informationen (auch zu Einschränkungen) finden Sie in [Unterstützte Sprachen für {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-sl-langs).

- __Erweiterungen des *{{site.data.keyword.pm_full}}-Frameworks*__: {{site.data.keyword.aios_short}} unterstützt nun die Frameworks 'Scikit-learn' und 'XGBoost' für die {{site.data.keyword.pm_full}}-Engine.

   Weitere Informationen enthält der Abschnitt [{{site.data.keyword.pm_full}}-Frameworks](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml).

## 25. April 2019
{: #rn-25April2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

Zusätzlich zur Verbesserung der Benutzerfreundlichkeit und den Sicherheitsupdates wurden neue Funktionen entwickelt. Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden in den vergangenen Wochen hinzugefügt oder erweitert:

- __*Tour für automatisierte Konfiguration*__: Eine neue Möglichkeit, die {{site.data.keyword.aios_short}}-Umgebung anhand einer Tour einzurichten. Mit der [automatisierten Konfiguration](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start) können Sie Services bereitstellen und ein Modell herunterladen und konfigurieren. Wenn Sie über eine neue Instanz von {{site.data.keyword.aios_short}} verfügen, wird diese Option angezeigt.
- __*Zu Beta wechseln*__: ![Beta-Tag](images/beta.png) Die neue Wechseloption **Neue Betaversion erkunden** ermöglicht es Ihnen, in der Betaumgebung zu arbeiten, in der Sie die neuesten Features und neue Funktionen erkunden können. Sie sind nicht überzeugt? Wechseln Sie einfach zurück, indem Sie auf **Zurück zur Originalversion** klicken. Die Konfiguration und die Überwachungen sind davon nicht betroffen. Die folgenden Funktionen sind Teil des aktuellen Betaprogramms:
    - __*Wahrheitsmatrix*__: Eine [Wahrheitsmatrix](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx) zeigt die falsch-positiven und die falsch-negativen Ergebnisse an. Klicken Sie auf eine Zelle, um die Untergruppe der Rückmeldedatensätze anzuzeigen.

## 10. April 2019
{: #rn-10April2019}

- __*Express Path-Tool unterstützt nun Kundenmodelle*__: Mit diesem Tool wird der Onboarding-Prozess für {{site.data.keyword.aios_short}} automatisiert.

   Weitere Informationen finden Sie in [ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/).


## 5. März 2019
{: #rn-5March2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Vorgängerrelease hinzugefügt oder funktional erweitert:

- __*Neues Kreditrisikomodell*__: Es wird ein neues Modell 'Kreditrisiko' für alle Scoring-Engines unterstützt. Weitere Informationen enthalten die Abschnitte [Erste Schritte](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) und [Zusätzliche Ressourcen](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Berechnung der Verzerrungsbereinigung*__: Es ist möglich, zwischen Ihrem Produktionsmodell und einem von {{site.data.keyword.aios_short}} erstellten verzerrungsbereinigten Modell hin- und herzuschalten. Weitere Informationen enthalten die Abschnitte [Produktionsmodell und verzerrungsbereinigtes Modell](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) und [Informationen zur Funktionsweise der Verzerrungsbereinigung](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

## 22. Februar 2019
{: #rn-22February2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Vorgängerrelease hinzugefügt oder funktional erweitert:

- __*Aktualisierungen der Benutzerschnittstelle (UI)*__: Sie können eine JSON-Datei importieren, um alle Überwachungen und Funktionen während der Erstellung des Abonnements programmgestützt zu konfigurieren. Sie können die Konfigurationsdatei auch exportieren. Weitere Informationen enthält der Abschnitt [Bereitstellungsabonnement mithilfe von JSON-Dateien konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-cf-ov).

## 7. Februar 2019
{: #rn-7February2019}

Die folgenden neuen Funktionen und Änderungen beim Service sind verfügbar.

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Vorgängerrelease hinzugefügt oder funktional erweitert:

- __*Aktualisierungen der Benutzerschnittstelle (UI)*__: An der Benutzerschnittstelle von {{site.data.keyword.aios_short}} wurden mehrere Verbesserungen durchgeführt, unter anderem durch eine Möglichkeit, [Fairness und Genauigkeit bei Bedarf zu überprüfen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep), und die Möglichkeit, eine Liste von Transaktionen aus der [Diagramm mit Details zur Fairness](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Verbesserungen bei der Erklärbarkeit*__: Für alle Zahlen gilt nun dieselbe Genauigkeit/derselbe Maßstab bei relevanten positiven und relevanten negativen Werten.

- __*SSL-Unterstützung bei Db2*__: {{site.data.keyword.aios_short}} unterstützt die Übergabe von selbst signierten Zertifikaten (in Base64-Codierung) mit DB2-Berechtigungsnachweisen.

- __*Unterstützung der {{site.data.keyword.Bluemix}}-Datenbank*__: {{site.data.keyword.aios_short}} unterstützt jetzt zusätzlich zu Compose for PostgreSQL und Db2 auch Databases for PostgreSQL.

## 14. Dezember 2018
{: #rn-14December2018}

Die folgenden neuen Funktionen, Änderungen und bekannten Probleme bei dem Service sind verfügbar.

Die folgenden {{site.data.keyword.aios_short}}-Funktionen wurden seit dem Beta-Release hinzugefügt oder funktional erweitert:

- __*Allgemeine Verfügbarkeit*__: Das GA-Release von {{site.data.keyword.aios_full_notm}} als {{site.data.keyword.Bluemix}}-Standardplan (gebührenpflichtig).

- __*{{site.data.keyword.icp4dfull_notm}} 1.2*__: Ziehen Sie bei Verwendung von {{site.data.keyword.wos4d_full}} die Dokumentation einschließlich der Installationsanweisungen im Abschnitt [Installationscheckliste](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#install) zurate.

- __*Unterstützung für Ihren Modelltyp*__: Zusätzlich zu den Bereitstellungen von AI-Modellen in {{site.data.keyword.pm_full}} unterstützt {{site.data.keyword.aios_short}} Modellbereitstellungen in Microsoft Azure, Amazon SageMaker und angepassten Umgebungen. Weitere Informationen enthält der Abschnitt [Unterstützte Modelltypen](/docs/services/ai-openscale?topic=ai-openscale-in-ov).

- __*Kostenlose 'Lite'-Datenbank*__: Eine kostenlose verwaltete 'Lite'-Datenbank bietet alles, was Sie benötigen, um mit der Verwendung von {{site.data.keyword.aios_short}} beginnen zu können. Genaueres hierzu enthält der Abschnitt [Preispläne für {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external}.

- __*Verzerrungsüberwachung*__: Unterstützung für geschützte Attribute vom Typ `float` und `double` sowie Verzerrungserkennung bei Modellen mit linearer Regression. {{site.data.keyword.aios_short}} kann außerdem automatisch eine Verzerrungsbereinigung für Ihr AI-Modell durchführen. Weitere Informationen enthält der Abschnitt [Informationen zu Fairness](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

- __*Erklärbarkeit*__: Unterstützung für Regressionsmodelle, Python-Funktionen sowie ergänzende kontrastierende Erklärungen. Weitere Informationen enthält der Abschnitt [Erklärbarkeit überwachen](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

- __*Datenspeicher*__: Qualitätsüberwachung, ohne auf {{site.data.keyword.pm_full}} angewiesen zu sein, und die Möglichkeit, Ihre eigene Datenbank zu verwenden, ganz gleich, ob es sich um Db2, Postgres oder Db2 on Cloud handelt.

- __*Funktional erweiterte Benutzerschnittstelle (UI)*__: Die Benutzerschnittstelle (UI) für {{site.data.keyword.aios_short}} wurde verbessert und enthält jetzt eine Laufzeithistogrammverteilung mit der Funktion zum Umschalten für Trainingsdaten, Modell-ID & Versionierung und eine Tabelle mit Transaktions-IDs aus dem Histogramm. Weitere Informationen enthält der Abschnitt [Visualisierung von Daten für eine bestimmte Stunde anzeigen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).

- __*Alternative Option zur Konfiguration des Lernprogramms*__: Um die Einrichtung und Konfiguration der erforderlichen {{site.data.keyword.Bluemix}}-Services zu automatisieren und eine IBM {{site.data.keyword.aios_full}}-Anwendung einschließlich Stichprobendaten anzuzeigen, können Sie ein Python-Modul installieren und ausführen. Näheres hierzu enthält [Python-Modul zum Konfigurieren von {{site.data.keyword.aios_short}} installieren](/docs/services/ai-openscale?topic=ai-openscale-as-module).

## 17. September 2018
{: #rn-17September2018}

- **Beta-Vorschauversion**: Willkommen bei der Beta-Vorschauversion von {{site.data.keyword.aios_full_notm}}.

<p>&nbsp;</p>

## Weitere Schritte
{: #relnotes-in-next}

Haben Sie immer noch offene Fragen?

- [Einschränkungen](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [Bekannte Probleme](/docs/services/ai-openscale?topic=ai-openscale-rn-12ki#cloud-limitations)
