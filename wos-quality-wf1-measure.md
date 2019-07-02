---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted F1-Measure

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

# Weighted F1-Measure ![beta tag](images/beta.png)
{: #quality_wght_f1-measure}

Weighted F1-Measure gives the weighted mean of F1-measure with weights equal to class probability.
{: shortdesc}

## Weighted F1-Measure at a glance
{: #quality_wght_f1-measure-glance}

- **Description**: Weighted mean of F1-measure with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

## Interpreting the display
{: #quality_wght_f1-measure-display}

![the Weighted F1-Measure chart is displayed.](images/quality-f1-meas.png)

## Do the math
{: #quality_wght_f1-measure-math}

The Weighted F1-Measure is the result of using weighted data.

```
          (precision * recall)
F1 = 2 *  ____________________

          (precision + recall)
```