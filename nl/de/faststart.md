---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, getting started, tutorial, understanding, fast start

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Automatisierte Konfiguration
{: #wos-fast-start}

Wenn Sie schnell sehen möchten, wie von {{site.data.keyword.aios_short}} ein Modell überwacht wird, nutzen Sie die Option für das Demo-Szenario, die bereitgestellt wird, wenn Sie sich zum ersten Mal an der Benutzerschnittstelle von {{site.data.keyword.aios_short}} anmelden.  Informationen hierzu finden Sie unter [Mit Demo der Benutzerschnittstelle arbeiten](#wos-work-demo).
{: shortdesc}

## Vorbereitende Schritte
{: #wos-prereqs}

Bevor Sie mit der Tour beginnen, müssen die folgenden Ressourcen bereits konfiguriert sein:

- {{site.data.keyword.ibmid}}
- {{site.data.keyword.aios_full}}

## Mit Demo der Benutzerschnittstelle arbeiten
{: #wos-work-demo}

1.  Melden Sie sich an der {{site.data.keyword.aios_short}}-Instanz in {{site.data.keyword.bluemix_full}} an.
1.  Wenn Sie mit dem Demoszenario arbeiten möchten, klicken Sie auf **Demo ausführen**.

   ![Demo 'Willkommen'](images/fastpath_demo_11.31.04.png)

   Wenn die {{site.data.keyword.aios_short}}-Services bereitgestellt werden, können Sie das Demoszenario überprüfen:

   ![Demovorschau](images/fastpath_demo_11.31.58.png)

Klicken Sie nach dem Abschluss der Bereitstellung auf die Schaltfläche **Los geht's**, um eine Tour durch das {{site.data.keyword.aios_short}}-Dashboard zu starten. Fahren Sie mit [Ergebnisse in {{site.data.keyword.aios_short}} anzeigen](#wos-open) fort.

   ![Demo zum Einstieg](images/fastpath_demo_11.33.45.png)


## Ergebnisse in {{site.data.keyword.aios_short}} anzeigen
{: #wos-open}

Um Einblicke in die Fairness und Genauigkeit des Modells, die Details der zu überwachenden Daten und die Erklärbarkeit für eine einzelne Transaktion zu erhalten, öffnen Sie das {{site.data.keyword.aios_short}}-Dashboard. Jede Bereitstellung wird als Kachel angezeigt. Die Tour hat eine Bereitstellung namens `GermanCreditRiskModel` konfiguriert, wie auf dem folgenden Screenshot zu sehen ist:


   ![Demo zum Einstieg](images/fastpath_demo_11.33.54.png)


### Insights anzeigen
{: #wos-insights}

Die Seite 'Insights' zeigt auf einen Blick alle eventuellen Probleme mit Fairness und Genauigkeit wie durch die konfigurierten Schwellenwerte bestimmt an.

   ![Demo zum Einstieg](images/fastpath_demo_11.34.00.png)

### Überwachungsdaten anzeigen
{: #wos-monitoring}

1.  Klicken Sie auf der Seite 'Insights' auf die Kachel `GermanCreditRiskModelICP`, um Details zu den überwachten Daten anzuzeigen.
1.  Klicken Sie auf die Markierung und ziehen Sie sie über das Diagramm, um einen Tag und einen Zeitraum anzuzeigen, zu dem Daten dargestellt werden; klicken Sie danach auf den Link **Details anzeigen**. Alternativ können Sie auf unterschiedliche Zeiträume im Diagramm klicken, um das angezeigte Datum zu ändern.

     - Die folgende Anzeige enthält beispielsweise Daten für ein bestimmtes Datum und eine bestimmte Uhrzeit. Die Daten und Zeiten variieren je nachdem, wann Sie das Modul ausführen.

     - Informationen zur Interpretation des Zeitreihendiagramms erhalten Sie in [Fairness, durchschnittliche Zahl der Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).

   ![Demo zum Einstieg](images/fastpath_demo_11.34.17.png)

1.  Damit Details zur Überwachung von Daten zum `GESCHLECHT` angezeigt werden, stellen Sie sicher, dass im Dropdown-Menü die Option `GESCHLECHT` ausgewählt ist.

    - Beachten Sie, dass im folgenden Screenshot eine Verzerrung vorhanden ist.
    
   ![Demo zum Einstieg](images/fastpath_demo_11.34.27.png)

    - Informationen zum Interpretieren des Diagramms der Datenpunkte zu einer bestimmten Stunde finden Sie unter [Datenvisualisierung](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual).


### Erklärbarkeit anzeigen
{: #wos-explain}

Um die Faktoren zu verstehen, die beteiligt sind, wenn eine Verzerrung für einen bestimmten Zeitraum vorliegt, klicken Sie in der im vorherigen Abschnitt dargestellten Visualisierungsanzeige auf das Optionsfeld **Verzerrte Transaktionen**.

   ![Demo zum Einstieg](images/fastpath_demo_11.35.06.png)

Für diejenigen Transaktionen, die eine Verzerrung aufweisen, werden die Transaktions-IDs der letzten Stunde aufgelistet. Für das in diesem Modul verwendete Modell gibt es für die verfügbaren Anforderungen eine Verzerrung.

   ![Demo zum Einstieg](images/fastpath_demo_11.35.12.png)

Informationen zum Suchen und Erklären von Transaktionen finden Sie im Abschnitt [Erklärbarkeit überwachen](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov).

   ![Demo zum Einstieg](images/fastpath_demo_11.35.50.png)

## Tour beenden
{: #wos-done-demo}

1. Klicken Sie auf die Schaltfläche **Fertig**.

   ![Demo zum Einstieg](images/fastpath_demo_11.37.22.png)

2. Klicken Sie auf die Schaltfläche **Los geht's**, um mit der Verwendung von {{site.data.keyword.aios_short}} zu beginnen.

   ![Demo zum Einstieg](images/fastpath_demo_11.33.45.png)


## Zugehörige Informationen
{: #wos-info}

- Wenn Sie mehr über Verzerrungen erfahren möchten, können Sie in [Fairness](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor) nachlesen.
- Informationen dazu, wie gut Ihr Modell Ergebnisse vorhersagt, finden Sie in [Genauigkeit](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- Informationen zum Interpretieren von Diagrammen, Daten und Transaktionen finden Sie unter [Fairness, durchschnittliche Anforderungen pro Minute und Genauigkeit überwachen](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).
