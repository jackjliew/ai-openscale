---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: dashboard, navigating, navigation, insights

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

# Getting insights with {{site.data.keyword.aios_short}}
{: #io-ov}

You can track all the deployments you are monitoring through the {{site.data.keyword.aios_full}} dashboard. The dashboard is your main view into {{site.data.keyword.aios_short}} and provides you with the means of getting insights into how your models are performing.
{: shortdesc}

## Insights
{: #io-ins}

The **Insights** tab ( ![Insight dashboard](images/insight-dash-tab.png) ) provides a high-level view of your deployment monitoring.

  ![Insight dashboard](images/insight-dashboard.png)

- ***Deployments Monitored*** - In this example, a total of 10 deployments are being monitored. Eight of the ten following deployments are shown as individual tiles.

- ***Quality Alerts*** - A total of 3 Quality (previously called Accuracy) alerts are represented in the following tiles. In this example, the `Driver Performance`, `Market Analytics`, and `Pricing Risk` deployments show Accuracy values of `60%`, `65%`, and `79%`, respectively.

- ***Fairness Alerts*** - There are a total of 6 Fairness alerts, represented in the following tiles, and by a small `BIAS` tag. In this example, the `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization`, and `Damage Cost Estimator` deployments show Fairness values of `59%`, `68%`, `62%`, `64%`, `79%`, and `63%`, respectively.

Each tile provides a summary of monitoring activity for that deployment. Note that the `Call Center Routing` deployment tile shows no issues, indicating a fairly stable, accurate model.


## Fairness, quality, performance, accuracy, and analytics insights
{: #it-ov}

Select any of the individual deployment tiles to view more details about that deployment. Monitoring data for individual deployments displays in a series of charts. The charts track metrics, such as fairness, average requests per minute, and accuracy over days, weeks, or months.

- [Viewing data for a deployment](/docs/services/ai-openscale?topic=ai-openscale-it-vdep)
- [Visualizing data for a specific hour](/docs/services/ai-openscale?topic=ai-openscale-it-vdet)
- [Fairness](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)
- [Quality](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)
- [Drift](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
- [Performance](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_performance)
- [Analytics](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)
- [De-biasing options](/docs/services/ai-openscale?topic=ai-openscale-it-dbo)

## Explainability
{: #io-tran}

Use the **Explain a transaction** tab ( ![Explain a transaction tab](images/insight-transact-tab.png) ) to search a specific transaction ID to explain a particular deployment transaction.

- [Explaining transactions](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)
- [Explaining categorical models](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Explaining image models](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Explaining unstructured text models](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Contrastive explanations](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)

## Next steps
{: #io-next}

- [Add more deployments to monitor](/docs/services/ai-openscale?topic=ai-openscale-dpl-select).

