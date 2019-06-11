---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Analyzing metrics and transactions ![beta tag](images/beta.png)
{: #anlz_metrics}

You can use {{site.data.keyword.aios_full}} to analyze metrics and transactions through a variety of means.
{: shortdesc}

## Fairness metrics
{: #anlz_metrics_fairness}

Use fairness monitoring to determine whether outcomes that are produced by your model are fair or not for monitored group. When fairness monitoring is enabled, it generates a set of metrics every hour by default. You can generate these metrics on demand by clicking the **Check quality now** button or by using the Python client.

Fairness metrics are calculated based on the following information:

- scoring payload data.

For proper monitoring purpose, every scoring request should be logged in {{site.data.keyword.aios_short}} as well. Payload data logging is automated for {{site.data.keyword.pm_full}} engines.

For other machine learning engines, the payload data can be provided either by using the Python client or the REST API.

For machine learning engines other than {{site.data.keyword.pm_full}}, fairness monitoring creates additional scoring requests on the monitored deployment.
{: note}

You can review all metrics value over time on the {{site.data.keyword.aios_short}} dashboard:

![fairness metrics chart showing drift lower than the set threshold](images/fairness_metrics_001.png)

You can review related details, such as favourable and unfavourable outcomes:

![fairness details](images/fairness_metrics_002.png)

You can view detailed transactions:

![a chart on fairness showing a list of transactions](images/fairness_metrics_003.png)

You can view the recommended debiased scoring endpoint:

![details of the debiased scoring endpoint](images/fairness_metrics_004.png)

### Supported fairness metrics
{: #anlz_metrics_supfairmets}

The following fairness metrics are supported by {{site.data.keyword.aios_short}}:

#### Fairness for a group
{: #anlz_metrics_supfairmets_group}

- **Description**: The models propensity to deliver favourable outcomes to one group over another.
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**: Debiased scoring endpoint you can use in your business application for receiving debiased responses from your deployed model.
- **Problem type**: All
- **Data type**: Structured
- **Chart values**: Last value in the time frame
- **Metrics details available**: Yes

### Supported fairness details
{: #anlz_metrics_supfairdets}

The following details for fairness metrics are supported by {{site.data.keyword.aios_short}}:

- The favorable percentages for each of groups
- Fairness averages for all the fairness groups

  Disparate Impact Ratio = (% of favorable outcome in monitored group) / (% of favorable outcome in reference group)

- Distribution of the data for each of the monitored groups
- Distribution of payload data


<!---
BTW, I propose to use screenshots with data from FastPath.
Source monitored group or referenced group
Source of bias is also in fairness metrics
--->


## Quality metrics
{: #anlz_metrics_quality}

Use quality monitoring to determine how well your model predicts outcomes. When quality monitoring is enabled, it generates a set of metrics every hour by default. You can generate these metrics on demand by clicking the **Check quality now** button or by using the Python client.

Quality metrics are calculated based on the following information:

- manually labeled feedback data,
- monitored deployment responses for these data.

For proper monitoring, feedback data must be logged to {{site.data.keyword.aios_short}} on a regular basis. The feedback data can be provided either by using "Add Feedback data" option or using Python client or REST API.

For machine learning engines other than {{site.data.keyword.aios_short}}, such as Microsoft Azure ML Studio or Amazon Sagemaker ML quality monitoring creates additional scoring requests on the monitored deployment.
{: note}

You can review all metrics values over time on the {{site.data.keyword.aios_short}} dashboard:

![quality metrics chart showing drift of area under ROC](images/quality_metrics_001.png)


To review related details, such as confusion matrix for binary and multi-class classification, which are available for some metrics, click the chart.

![detail table of quality metrics](images/quality_metrics_002.png)

### Supported quality metrics
{: #anlz_metrics_supqualdets}

The following quality metrics are supported by {{site.data.keyword.aios_short}}:

#### Area under ROC
{: #anlz_metrics_supqualdets_roc}

- **Description**: Area under recall and false positive rate curve
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Area under PR
{: #anlz_metrics_supqualdets_pr}

- **Description**: Area under precision and recall curve
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Proportion explained variance
{: #anlz_metrics_supqualdets_var}

- **Description**: Proportion explained variance is the ratio of explained variance and target variance. Explained variance is the difference between target variance and variance of prediction error.
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

#### Mean absolute error
{: #anlz_metrics_supqualdets_abserror}

- **Description**: Mean of absolute difference between model prediction and target value
- **Default thresholds**: Upper limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Downward trend**: A downward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

#### Mean squared error
{: #anlz_metrics_supqualdets_squerror}

- **Description**: Mean of squared difference between model prediction and target value
- **Default thresholds**: Upper limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Downward trend**: A downward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

#### R squared
{: #anlz_metrics_supqualdets_r_squared}

- **Description**: Ratio of difference between target variance and variance for prediction error to target variance
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

#### Root of mean squared error
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Description**: Square root of mean of squared difference between model prediction and target value
- **Default thresholds**: Upper limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Downward trend**: A downward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Regression
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

#### Accuracy
{: #anlz_metrics_supqualdets_acc}

- **Description**: The proportion of correct predictions
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem types**: Binary classification and multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Weighted True Positive Rate (wTPR)
{: #anlz_metrics_supqualdets_wtpr}

- **Description**: Weighted mean of class TPR with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### True positive rate (TPR)
{: #anlz_metrics_supqualdets_tpr}

- **Description**: Proportion of correct predictions in predictions of positive class
- **Default thresholds**: lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Weighted False Positive Rate (wFPR)
{: #anlz_metrics_supqualdets_wfpr_weighted}

- **Description**: Weighted mean of class FPR with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### False positive rate (FPR)
{: #anlz_metrics_supqualdets_fpr_false}

- **Description**: Proportion of incorrect predictions in positive class
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Weighted recall
{: #anlz_metrics_supqualdets_weighted_recall}

- **Description**: Weighted mean of recall with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Recall
{: #anlz_metrics_supqualdets_recall}

- **Description**: Proportion of correct predictions in positive class
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Weighted precision
{: #anlz_metrics_supqualdets_wgth_prec}

- **Description**: Weighted mean of precision with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Precision
{: #anlz_metrics_supqualdets_precision}

- **Description**: Proportion of correct predictions in predictions of positive class
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Weighted F1-Measure
{: #anlz_metrics_supqualdets_wght_f1-measure}

- **Description**: Weighted mean of F1-measure with weights equal to class probability
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### F1-Measure
{: #anlz_metrics_supqualdets_f1-measr}

- **Description**: Harmonic mean of precision and recall
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that the feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: Confusion matrix

#### Logarithmic loss
{: #anlz_metrics_supqualdets_log_loss}

- **Description**: Mean of logarithms target class probabilities (confidence). It is also known as Expected log-likelihood.
- **Default thresholds**: Lower limit = 80%
- **Default recommendation**:
   - **Upward trend**: An upward trend indicates that the metric is improving. This means that model retraining is effective.
   - **Downward trend**: A downward trend indicates that the metric is deteriorating. Feedback data is becoming significantly different than the training data.
   - **Erratic or irregular variation**: An erratic or irregular variation indicates that t The feedback data is not consistent between evaluations. Increase the minimum sample size for the Quality monitor.
- **Problem type**: Binary classification and multiclass classification
- **Chart values**: Last value in the time frame
- **Metrics details available**: None

### Supported quality details
{: #anlz_metrics_supqualdets_suppr_dets}

The following details for quality metrics are supported by {{site.data.keyword.aios_short}}:

#### Confusion matrix
{: #anlz_metrics_supqualdets_confusion}

Confusion matrix helps you to understand for which of your feedback data the monitored deployment response is correct and for which it is not.

## Performance metrics
{: #anlz_metrics_performance}

Use performance monitoring to know the velocity of data records processed by your deployment. You enable performance monitoring when you select the deployment to be tracked and monitored by {{site.data.keyword.aios_short}}.

Performance metrics are calculated based on the following information:

- scoring payload data

For proper monitoring purpose, every scoring request should be logged in {{site.data.keyword.aios_short}} as well. Payload data logging is automated for {{site.data.keyword.pm_full}} engines. For other machine learning engines, the payload data can be provided either by using using the Python client or the REST API. Performance monitoring does not create any additional scoring requests on the monitored deployment.

You can review performance metrics value over time on the {{site.data.keyword.aios_short}} dashboard:

![performance chart](images/performance_metrics_001.png)

### Supported performance metrics
{: #anlz_metrics_performance_supp_quality_mets}

The following performance metrics are supported by {{site.data.keyword.aios_short}}:

#### Throughput
{: #anlz_metrics_performance_supp_quality_mets_through}

- **Description**: Average scoring requests per minute in specific timeframe
- **Default thresholds**: Not applicable
- **Default recommendation**: Not applicable
- **Problem type**: All
- **Chart values**: Average value in the time frame
- **Metrics details available**: None

## Payload data analytics
{: #anlz_metrics_payload}

You can analyze the scoring payload that is sent to your deployment in the selected data range by either of the following methods:

- By review prediction classes and confidence distribution in each class
   
   ![a chart that maps prediction by confidence distribution](images/by_confidence.png)
   
- By custom chart (selecting between features, prediction classes and confidence)
   
   ![a chart that shows feature prediction for gender by the feature age](images/by_custom_chart.png)

