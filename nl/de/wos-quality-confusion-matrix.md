---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# Wahrheitsmatrix ![Beta-Tag](images/beta.png)
{: #it-conf-mtx}

Als Detail der Qualitätsmetriken können Sie die Datensätze anzeigen, die das Modell nicht korrekt analysiert hat. Bei solchen Anomalien kann es sich um falsch-positive oder falsch-negative Ergebnisse für binäre Klassifizierungsmodelle handeln oder um fehlerhafte Kassenzuweisungen für Modelle mit mehreren Klassen. Darüber hinaus können Sie eine Liste mit Rückmeldedatensätzen anzeigen, die vom Modell nicht korrekt analysiert wurden.
{: shortdesc}

Klicken Sie auf das Diagramm, um zugehörige Details, wie z. B. die Wahrheitsmatrix für die binäre Klassifizierung und die Klassifizierung mit mehreren Klassen, die für einige Metriken zur Verfügung stehen.

![Detailtabelle für Qualitätsmetriken](images/quality_metrics_002.png)

Bei binären Problemen ordnet {{site.data.keyword.aios_full}} die Zielkategorie entweder der `positiven` oder der `negativen` Ebene zu. Die Ausgabe der Konfusionsmatrix folgt deshalb der Konvention, bei der sich die Kennzeichnung für die positive Kategorie in der zweiten Zeile oder Spalte befindet.


## Schritte
{: #it-conf-mtx-steps}

1. Klicken Sie in einem der Diagramme des Typs **Qualität**, z. B. **Genauigkeit**, auf eine Stunde bzw. einen Tag.
    
    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.004.png)

1. In einer Wahrheitsmatrix werden die falsch-positiven und falsch-negativen Ergebnisse angezeigt. Klicken Sie auf eine Zelle, um die Untergruppe der Rückmeldedatensätze anzuzeigen.

    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.005.png)

1. Überprüfen Sie die Rückmeldedatensätze und fordern Sie eine Erklärung für den Rückmeldedatensatz an.

    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.006.png)

1. Transaktionen sind in die Darstellung integriert.

    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.007.png)

