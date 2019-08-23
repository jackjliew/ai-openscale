---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Übersicht zu Qualitätsmetriken
{: #anlz_metrics}

Verwenden Sie die Qualitätsüberwachung, um zu ermitteln, wie gut die Ergebnisse von Ihrem Modell vorhergesagt werden. Wenn die Qualitätsüberwachung aktiviert ist, generiert sie standardmäßig jede Stunde eine Gruppe von Metriken. Sie können diese Metriken bedarfsgesteuert generieren, indem Sie auf die Schaltfläche **Qualität jetzt überprüfen** klicken oder indem Sie den Python-Client verwenden.
{: shortdesc}

Qualitätsmetriken werden auf der Basis der folgenden Informationen berechnet:

- Manuell gekennzeichnete Rückmeldedaten
- Überwachte Bereitstellungsantworten für diese Daten

Für eine korrekte Überwachung müssen Rückmeldedaten regelmäßig in {{site.data.keyword.aios_short}} protokolliert werden. Die Rückmeldedaten können entweder über die Option "Rückmeldedaten hinzufügen" oder über den Python-Client bzw. die REST-API bereitgestellt werden.

Bei Machine Learning-Engines, bei denen es sich nicht um {{site.data.keyword.aios_short}} handelt, z. B. Microsoft Azure ML Studio, Microsoft Azure ML Service oder Amazon Sagemaker ML, werden durch die Qualitätsüberwachung zusätzliche Scoring-Anforderungen für die überwachte Umgebung erstellt.
{: note}

Alle Metrikwerte für einen bestimmten Zeitraum können im {{site.data.keyword.aios_short}}-Dashboard überwacht werden:

![Diagramm mit Qualitätsmetriken, das die Drift bei der Fläche unterhalb der ROC-Kurve anzeigt](images/quality_metrics_001.png)


Klicken Sie auf das Diagramm, um zugehörige Details, wie z. B. die Wahrheitsmatrix für die binäre Klassifizierung und die Klassifizierung mit mehreren Klassen, die für einige Metriken zur Verfügung stehen.

![Detailtabelle für Qualitätsmetriken](images/quality_metrics_002.png)

## Unterstützte Qualitätsmetriken
{: #anlz_metrics_supqualdets}

Die folgenden Qualitätsmetriken werden von {{site.data.keyword.aios_short}} unterstützt:

- [Fläche unterhalb der ROC-Kurve](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [Fläche unterhalb der PR-Kurve](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [Proportion der erklärten Varianz](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_var)
- [Mittlerer absoluter Fehler](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_abserror)
- [Mittlerer quadratischer Fehler](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_squerror)
- [R im Quadrat](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_r_squared)
- [Wurzel für mittleren quadratischen Fehler](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-supqualdets_squ_errors_mean)
- [Genauigkeit](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [Gewichtete Wahr-positiv-Rate (wTPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-wtpr)
- [Wahr-positiv-Rate (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [Gewichtete Falsch-positiv-Rate (wFPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wfpr_weighted)
- [Falsch-positiv-Rate (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [Gewichtete Trefferquote](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_weighted_recall)
- [Trefferquote](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [Gewichtete Genauigkeit](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wgth_prec)
- [Genauigkeit](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [Gewichtetes F1-Maß](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wght_f1-measure)
- [F1-Maß](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [Logarithmischer Verlust](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## Unterstützte Qualitätsdetails
{: #anlz_metrics_supqualdets_suppr_dets}

Die folgenden Details für Qualitätsmetriken werden von {{site.data.keyword.aios_short}} unterstützt:

### Wahrheitsmatrix
{: #anlz_metrics_supqualdets_confusion-quickovr}

Mithilfe der Wahrheitsmatrix können Sie analysieren, für welche der Rückmeldedaten die Antwort der überwachten Bereitstellung korrekt ist und für welche nicht.

Weitere Informationen finden Sie in [Wahrheitsmatrix](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx).

## Weitere Schritte

- Nachdem {{site.data.keyword.aios_short}} ein Qualitätsproblem wie z. B. Schwellenwertverstöße bei der Genauigkeit erkannt hat, müssen Sie eine neue Version des Modells erstellen, durch die das Problem behoben wird. Wenn Sie die manuell gekennzeichneten Daten in der Rückmeldungstabelle verwenden, müssen Sie das Modell zusammen mit den ursprünglichen Trainingsdaten erneut trainieren.

