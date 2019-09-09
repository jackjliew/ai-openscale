---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

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

# Creating custom monitors and metrics ![beta tag](images/beta.png)
{: #cst_mtrcs}

Custom monitors consolidate a set of custom metrics that enable you to track, in a quantitative way, any aspect of your model deployment and business application. You can define custom metrics, and use them alongside the standard metrics, such as model quality, performance, or fairness metrics that are monitored in {{site.data.keyword.aios_full}}.
{: shortdesc}

To manage custom monitors and metrics you must use the programmatic interface that is part of the Python SDK. In similar way, you can store custom metrics in the {{site.data.keyword.aios_short}} datamart to access them when needed. Custom metrics are also visualized on the {{site.data.keyword.aios_short}} Dashboard.

## Managing custom metrics
{: #cst_mtrc_mgmt}

To work with custom metrics you must perform the following tasks:

1. [Register custom monitor with metrics definition](#cst_mtrc_mgmt-step1).
2. [Enable custom monitor](#cst_mtrc_mgmt-step2).
3. [Store metric values](#cst_mtrc_mgmt-step3).

The following advanced tutorials show how to do this:

- [Working with {{site.data.keyword.pm_full}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

You can disable and enable again custom monitoring at any time. You can remove custom monitor if you do not need it anymore.

For more information, see the [Python SDK documentation](http://ai-openscale-python-client.mybluemix.net/){: external}.


### Step 1: Register custom monitor with metrics definition.
{: #cst_mtrc_mgmt-step1}

Before you can start using custom metrics, you must register the custom monitor, which is the processor that tracks the metrics. You also must define the metrics themselves.

1. Use the `ibm_ai_openscale.supporting_classes` method to import the `Metric` and `Tag` objects.
2. Use the `metrics` method to define the metrics, which require `name` and `lower_limit_default` values.
3. Use the `tags` method to define metadata.

The following code is from the working sample notebook that was previously mentioned:

```
from ibm_ai_openscale.supporting_classes import Metric, Tag

metrics = [Metric(name='sensitivity', lower_limit_default=0.8), Metric(name='specificity', lower_limit_default=0.75)]
tags = [Tag(name='region', description='customer geographical region')]

my_monitor = client.data_mart.monitors.add(name='model performance', metrics=metrics, tags=tags)
```

To check how you're doing, run the `client.data_mart.monitors.list()
` command to see if your newly-created monitor and metrics are configured properly.
{: tip}

You can also get the monitor ID by running the following command:

```
monitor_uid = my_monitor['metadata']['guid']

print(monitor_uid)
```

For a more detailed look, run the following command:

```
my_monitor = client.data_mart.monitors.get_details(monitor_uid=monitor_uid)
print('monitor definition details', my_monitor)
```


### Step 2: Enable custom monitor.
{: #cst_mtrc_mgmt-step2}

Next, you must enable the custom monitor for subscription. This activates the monitor and sets the thresholds.

1. Use the `ibm_ai_openscale.supporting_classes` method to import the `Threshold` object.
2. Use the `threshold` method to set the metric `lower_limit` value. You'll need to supply the `metric_uid` value as one of the parameters. If you don't remember, you can always use the `my_monitor` command to get the details as shown in the previous example.

The following code is from the working sample notebook that was previously mentioned:

```
from ibm_ai_openscale.supporting_classes import Threshold

thresholds = [Threshold(metric_uid='sensitivity', lower_limit=0.9)]
subscription.monitoring.enable(monitor_uid=monitor_uid, thresholds=thresholds)
```

To check on your configuration details, use the `subscription.monitoring.get_details(monitor_uid=monitor_uid)` command.

### Step 3: Store metric values.
{: #cst_mtrc_mgmt-step3}

You must store, or save, your custom metrics to the region where your {{site.data.keyword.aios_short}} instance exists.

1. Use the `metrics` method to set which metrics you are storing.
2. Use the `subscription.monitoring.store_metrics` method to commit the metrics.

The following code is from the working sample notebook that was previously mentioned:

```
metrics = {"specificity": 0.78, "sensitivity": 0.67, "region": "us-south"}

subscription.monitoring.store_metrics(monitor_uid=monitor_uid, metrics=metrics)
```

## Accessing and visualizing custom metrics
{: #cst_mtrcs_viz}

To access and visualize custom metrics you can use programmatic interface. The following advanced tutorials show how to do this:

- [Working with {{site.data.keyword.pm_full}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

   For more information, see [the Python SDK documentation](http://ai-openscale-python-client.mybluemix.net/){: external}.

Visualization of your custom metrics appear on the {{site.data.keyword.aios_short}} Dashboard.
