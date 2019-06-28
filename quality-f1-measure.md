---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, F1-Measure

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

# F1-Measure ![beta tag](images/beta.png)
{: #quality_f1-measr}

F1-Measure gives the harmonic mean of precision and recall.
{: shortdesc}

## F1-Measure at a glance
{: #quality_f1-measr-glance}

- **Description**: Harmonic mean of precision and recall
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

## Interpreting the display
{: #quality_f1-measr-display}

![the F1-Measure chart is displayed.](images/quality-f1-meas.png)

## Do the math
{: #quality_f1-measr-math}

The F1-Measure is the waited harmonic average, or mean, of precision and recall.

```
          (precision * recall)
F1 = 2 *  ____________________

          (precision + recall)
```