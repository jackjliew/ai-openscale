---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# Confusion matrix ![beta tag](images/beta.png)
{: #it-conf-mtx}

As a detail of the quality metrics, you can view the records that the model analyzed incorrectly. Such anomalies can be false positives or false negatives for binary classification models or can be incorrect class assignments for multi-class models. You can also view a list of feedback records that the model did not analyze correctly.
{: shortdesc}

To review related details, such as confusion matrix for binary and multi-class classification, which are available for some metrics, click the chart.

![detail table of quality metrics](images/quality_metrics_002.png)

## Steps
{: #it-conf-mtx-steps}

1. From any of the **Quality** charts, such as **Accuracy** click on an hour/day in the chart.
    
    ![Transaction list biased](images/Confusion_Matrix_040819.004.png)

1. A confusion matrix displays the false positives and false negatives. Click a cell to view the subset of feedback records.

    ![Transaction list biased](images/Confusion_Matrix_040819.005.png)

1. Review the feedback records and request an explanation of the analysis against the feedback record.

    ![Transaction list biased](images/Confusion_Matrix_040819.006.png)

1. Transactions appear inline.

    ![Transaction list biased](images/Confusion_Matrix_040819.007.png)

