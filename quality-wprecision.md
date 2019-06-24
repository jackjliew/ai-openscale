---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted precision

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

# Weighted precision ![beta tag](images/beta.png)
{: #quality_wgth_prec}

Weighted precision gives the weighted mean of precision with weights equal to class probability.
{: shortdesc}

## Weighted precision at a glance
{: #quality_wgth_prec-glance}

- **Description**: Weighted mean of precision with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

## Interpreting the display
{: #quality_wgth_prec-display}

![the Weighted precision chart is displayed.](images/quality-precision.png)

## Do the math
{: #quality_wgth_prec-math}

Precision (P) is defined as the number of true positives (Tp) over the number of true positives plus the number of false positives (Fp).


```
                        number of true positives
Precision =  __________________________________________________________

             (number of true positives + the number of false positives)
```