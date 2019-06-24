---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: metrics, monitoring, custom metrics, thresholds, weighted recal

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

# Weighted recall ![beta tag](images/beta.png)
{: #quality_weighted_recall}

Weighted recall gives the weighted mean of recall with weights equal to class probability.
{: shortdesc}

## Weighted recall at a glance
{: #quality_weighted_recall-glance}

- **Description**: Weighted mean of recall with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

## Interpreting the display
{: #quality_weighted_recall-display}

![the weighted recall chart is displayed](images/quality-recall.png)

## Do the math
{: #quality_weighted_recall-math}

Weighted Recall (wR) is defined as the number of true positives (Tp) over the number of true positives plus the number of false negatives (Fn) used with weighted data. 

```
            number of true positives
Recall =   ______________________________________________________

           (number of true positives + number of false negatives)
```
