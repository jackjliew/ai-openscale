---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Metriken und Transaktionen analysieren ![Beta-Tag](images/beta.png)
{: #anlz_metrics}

{{site.data.keyword.aios_full}} bietet eine Vielzahl verschiedener Möglichkeiten zur Analyse von Metriken und Transaktionen.
{: shortdesc}

## Wahrheitsmatrix ![Beta-Tag](images/beta.png)
{: #it-conf-mtx}

Als Detail der Qualitätsmetriken können Sie die Datensätze anzeigen, die das Modell nicht korrekt analysiert hat. Bei solchen Anomalien kann es sich um falsch-positive oder falsch-negative Ergebnisse für binäre Klassifikationsmodelle handeln oder um fehlerhafte Kassenzuweisungen für Modelle mit mehreren Klassen. Darüber hinaus können Sie eine Liste mit Rückmeldedatensätzen anzeigen, die vom Modell nicht korrekt analysiert wurden.
{: shortdesc}

1. Klicken Sie in einem der Diagramme des Typs **Qualität**, wie z. B. **Fairness**, auf eine Stunde bzw. einen Tag.
    
    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.004.png)

1. In einer Wahrheitsmatrix werden die falsch-positiven und falsch-negativen Ergebnisse angezeigt. Klicken Sie auf eine Zelle, um die Untergruppe der Rückmeldedatensätze anzuzeigen.

    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.005.png)

1. Überprüfen Sie die Rückmeldedatensätze und fordern Sie eine Erklärung für den Rückmeldedatensatz an.

    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.006.png)

1. Transaktionen sind in die Darstellung integriert.

    ![Liste der verzerrten Transaktionen](images/Confusion_Matrix_040819.007.png)

