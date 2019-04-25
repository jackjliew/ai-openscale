---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-25"

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

# Custom metrics
{: #cst_mtrcs}

Metrics are quantitative measures. You can define custom metrics, and use them alongside the standard metrics monitored in {{site.data.keyword.aios_full}}, and view them on the  {{site.data.keyword.aios_short}} Dashboard. You can create metrics definitions programatically by using the API or by using the **Create New Monitor** function. Depending on the model and feedback data, each metric is calculated periodically or continuously and stored in the data mart.
{: shortdesc}

1. [Create a custom monitor.](#cst_mtrcs_registration)
2. [Define the monitor.](#cst_mtrcs_monitor_definitions)
3. [Create a custom metric.](#cst_mtrcs_metric_definations)
3. [Set thresholds]()

## Create a custom monitor
{: #cst_mtrcs_registration}

To create a monitor, you must give it a name and description.

1. Click **Create New Monitor**. 
2. Review information about custom monitors and click **Begin**.
3. Type a monitor name and description and click **Next**.

## Define the monitor
{: #cst_mtrcs_monitor_definitions}

To define the monitor, you must specify the input and model types that the monitor supports. Not all metrics make sense for certain input or model types.

1. Select one or more of the following inputs types and click **Next**:

	- Numeric/Categorical Models
	- Image Models
	- Unstructured Text Models
	
2. Select the model types to support and click **Next**.

## Create a custom metric
{: #cst_mtrcs_metric_definations}

In a single run, each monitor can produce multiple metrics, which are defined by a name, description, threshold values, and validation requirements.

1. Type a metric name and description.
2. Choose whether to assign upper and lower thresholds. Include corresponding values and remediation comments for each threshold that you set. Thresholds can be specified when enabling monitoring for a specific target (e.g. subscription) and updated over time.
3. Choose whether to enforce a validation requirement, which ensures that the metric is enforced by the API.
4. Click **Next**.
5. Review the metric.
6. To save the metric without adding another, click **Next**, and then click **Save**.
7. To continue adding metrics, click the **Add another** button.

When you have completed adding metrics, they appear in the list on the **Configuration** page, along with **Accuracy**, **Fairness**, and **Explainability**.

## Visualizing custom metrics
{: #cst_mtrcs_viz}

Multiple metrics that are part of a single custom monitor are visualized on a single chart that displays the following parameters:

- Threshold lower and upper bound values
- Multiple time series split by the grouping property

![Custom metric visualisation example](https://ibm.box.com/shared/static/64kfdi6c6lpjjfw3o295hxag2deafibb.png)