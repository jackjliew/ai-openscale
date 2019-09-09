---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: accuracy, 

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

# Configuring the application monitor ![beta tag](images/beta.png)
{: #app-monitor}

In {{site.data.keyword.aios_short}} application refers to either the business application or business process that uses AI models. Applications that are configured in {{site.data.keyword.aios_short}} enable you to monitor business KPIs as well as to understand the impact of model metrics, such as model drift on an application's business key performance indicators (KPIs).
{: shortdesc}

## Steps
{: #app-monitor-steps}

1. To start the configuration process, from the **Insights** dashboard, on the Applications monitor tab, click Add to dashboard.
2. Follow the prompts and enter required information. 
3. Review the configuration. After you finish, a summary of your selections is presented. 
4. To make changes, click the **Edit** icon for that section, otherwise, save your work. 

## Requirements
{: #app-config-reqs}

On the successive pages of the **Applications monitor** tab, you must provide the following information:

### Associated models
{: #app-config-reqs}

Select models that are deployed and associated with {{site.data.keyword.aios_short}}.

Only models with a defined `transaction_id` column can be associated with the application. To configure the `transaction_id` column, from the **Model monitor** configuration window, click **Model details**.
{: note}

### Event details
{: #app-config-event-dts}

Events represent a business transaction. Event data must contain all the data that is required to calculate your business KPIs. Each event must also contain timestamp information,such as `2019-09-03T10:44:13.000Z` as well as a business transaction ID. The business transaction ID must be the same as the `transaction_id` value in the scoring payload.


### KPIs
{: #app-config-kpisss}

A key performance indicator is a measurable value that a business uses to determine operational effectiveness and profitability.

### Logging endpoint
{: #app-config-log-endpt}

After you configure associated models, event details, and KPIs, on the **Logging endpoint** window, you must activate the application monitor by clicking **Activate monitor**.

After you activate application monitoring is activated, you can log business events data either by uploading a .csv file or by using the REST API.

There is no possibility to edit activated monitor configuration in the current Beta version.
{: note}


### Next steps
{: #app-next}

- [Configure KPI metrics](/docs/services/ai-openscale?topic=ai-openscale-kpi-monitor)
- Get insights into how your KPIs correlate to model drift. For more information, see [Getting application insights](/docs/services/ai-openscale?topic=ai-openscale-io-app-ov).
- [View correlation charts](/docs/services/ai-openscale?topic=ai-openscale-app-perform-vdet).
- [View KPI performance](/docs/services/ai-openscale?topic=ai-openscale-it-appkpi-vdet).
