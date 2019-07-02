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

# Creating custom monitors and metrics ![beta tag](images/beta.png)
{: #cst_mtrcs}

Custom monitors consolidate a set of custom metrics that enable you to track, in a quantitative way, any aspect of your model deployment and business application. You can define custom metrics, and use them alongside the standard metrics, such as model quality, performance, or fairness metrics that are monitored in {{site.data.keyword.aios_full}}.
{: shortdesc}

To manage custom monitors and metrics you must use the programmatic interface that is part of the Python SDK. In similar way, you can store custom metrics in the {{site.data.keyword.aios_short}} datamart to access them when needed. Custom metrics are also visualized on the {{site.data.keyword.aios_short}} Dashboard.

## Managing custom metrics
{: #cst_mtrc_mgmt}

To work with custom metrics you must perform the following tasks:

1. Register custom monitor with metrics definition.
2. Enable custom monitor.
3. Store metric values.

The following advanced tutorials show how to do this:

- [Working with {{site.data.keyword.pm_full}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

You can disable and enable again custom monitoring at any time. You can remove custom monitor if you do not need it anymore.

For more information, see the [Python SDK documentation](http://ai-openscale-python-client.mybluemix.net/).

## Accessing and visualizing custom metrics
{: #cst_mtrcs_viz}

To access and visualize custom metrics you can use programmatic interface. The following advanced tutorials show how to do this:

- [Working with {{site.data.keyword.pm_full}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   For more information, see [the Python SDK documentation](http://ai-openscale-python-client.mybluemix.net/).

Visualization of your custom metrics appear on the {{site.data.keyword.aios_short}} Dashboard.

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
