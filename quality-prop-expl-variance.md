---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# Proportion explained variance ![beta tag](images/beta.png)
{: #quality_var}

Proportion explained variance gives the ratio of explained variance and target variance. Explained variance is the difference between target variance and variance of prediction error.
{: shortdesc}

## Proportion explained variance at a glance
{: #quality_var-glance}

- **Description**: Proportion explained variance is the ratio of explained variance and target variance. Explained variance is the difference between target variance and variance of prediction error.
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

## Interpreting the display
{: #quality_var-display}

![the Proportion explained variance chart is displayed.](images/xxxx.png)

## Do the math
{: #quality_var-math}

The Proportion explained variance is calculated by averaging the numbers, then for each number, subtract the mean and square the results. Then work out the squares

```
                                  sum of squares between groups 
Proportion explained variance =  ________________________________

                                      sum of squares total
```