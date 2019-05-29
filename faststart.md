---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: ai, getting started, tutorial, understanding, fast start

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Automated setup
{: #wos-fast-start}

To quickly see how {{site.data.keyword.aios_short}} monitors a model, run the demo scenario option that is provided when you first log into the {{site.data.keyword.aios_short}} UI.  See [Working with the UI demo](#wos-work-demo).
{: shortdesc}

## Before you begin
{: #wos-prereqs}

Before you begin the tour, you must have the following resources already set up:

- {{site.data.keyword.ibmid}}
- {{site.data.keyword.aios_full}}

## Working with the UI demo
{: #wos-work-demo}

1.  Sign into your {{site.data.keyword.aios_short}} instance on {{site.data.keyword.bluemix_full}}.
1.  To work with the demo scenario, click **Run Demo**.

   ![Demo welcome](images/fastpath_demo_11.31.04.png)

   As the {{site.data.keyword.aios_short}} services are being provisioned, you can review the demo scenario:

   ![Demo preview](images/fastpath_demo_11.31.58.png)

When provisioning is complete, click the **Let's Go** button to tour the {{site.data.keyword.aios_short}} dashboard, and proceed with [Viewing results in {{site.data.keyword.aios_short}}](#wos-open).

   ![Demo Let's go](images/fastpath_demo_11.33.45.png)


## Viewing results in {{site.data.keyword.aios_short}}
{: #wos-open}

To view insights into the fairness and accuracy of the model, details of data that is monitored, and explainability for an individual transaction, open the {{site.data.keyword.aios_short}} dashboard. Each deployment is shown as a tile. The tour configured a deployment called `GermanCreditRiskModel`, as shown in the following screen capture:


   ![Demo Lets go](images/fastpath_demo_11.33.54.png)


### View insights
{: #wos-insights}

At a glance, the Insights page shows any issues with fairness and accuracy, as determined by the thresholds that are configured.

   ![Demo Lets go](images/fastpath_demo_11.34.00.png)

### View monitoring data
{: #wos-monitoring}

1.  From the Insights page, click the `GermanCreditRiskModelICP` tile to view details about the monitored data.
1.  Click and drag the marker across the chart to view a day and time period that shows data and then click the **View details** link. Alternatively, you can click different time periods in the chart to change the data that you see.

     - For example, the following screen shows data for a specific date and time. The dates and times vary, depending on when you run the module.

     - For information about interpreting the time series chart, see [Monitoring Fairness, Average Requests per Minute, and Accuracy](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).

   ![Demo Lets go](images/fastpath_demo_11.34.17.png)

1.  To see details about `SEX` data monitoring, ensure that `SEX` is selected from the drop-down menu.

    - Notice that in the following screen capture, bias exists.
    
   ![Demo Lets go](images/fastpath_demo_11.34.27.png)

    - For information about interpreting the chart of the data points at a specific hour, see [Data visualization](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual).


### View explainability
{: #wos-explain}

To understand the factors that contribute when bias is present for a given time period, from the visualization screen shown in the previous section, click the **Biased transactions** radio button.

   ![Demo Lets go](images/fastpath_demo_11.35.06.png)

Transaction IDs for the past hour are listed for those transactions that have bias. For the model used in this module, bias exists for requests that are available.

   ![Demo Lets go](images/fastpath_demo_11.35.12.png)

For information about finding and explaining transactions, see [Monitoring explainability](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov).

   ![Demo Lets go](images/fastpath_demo_11.35.50.png)

## Finishing up the tour
{: #wos-done-demo}

1. Click the **Done** button.

   ![Demo Lets go](images/fastpath_demo_11.37.22.png)

2. Click the **Let's Go** button to start working with {{site.data.keyword.aios_short}}.

   ![Demo Lets go](images/fastpath_demo_11.33.45.png)


## Related information
{: #wos-info}

- To learn about biases, see [Fairness](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor).
- To learn about how well your model predicts outcomes, see [Accuracy](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- To learn about interpreting charts, data, and transactions, see [Monitoring Fairness, Average Requests per Minute, and Accuracy](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).