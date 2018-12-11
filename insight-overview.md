---

copyright:
  years: 2018
lastupdated: "2018-12-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Navigating the dashboard
{: #insights}

You can track all the deployments you are monitoring through the {{site.data.keyword.aios_short}} dashboard. The dashboard is your main view into {{site.data.keyword.aios_short}}. The dashboard consists of five tabs:

  ![Insight tabs](images/insight-tabs.png)

{: shortdesc}

## Insights
{: #insight-dash-tab}

The Insights tab ( ![Insight dashboard](images/insight-dash-tab.png) ) provides a high-level view of your deployment monitoring.

  ![Insight dashboard](images/insight-dashboard.png)

- ***Deployments Monitored*** - In this example, a total of 10 deployments are being monitored. Eight of the ten deployments are shown as individual tiles below.

- ***Accuracy Alerts*** - A total of 3 Accuracy alerts are represented in the tiles below by purple shading. In this example, the `Driver Performance`, `Market Analytics`, and `Pricing Risk` deployments show Accuracy values of `60%`, `65%`, and `79%`, respectively.

- ***Fairness Alerts*** - There are a total of 6 Fairness alerts, represented in the tiles below by both purple shading, and by a small `BIAS` tag. In this example, the `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization`, and `Damage Cost Estimator` deployments show Fairness values of `59%`, `68%`, `62%`, `64%`, `79%`, and `63%`, respectively.

Each tile provides a summary of monitoring activity for that deployment. Note that the `Call Center Routing` deployment tile shows no issues, indicating a fairly stable, accurate model.

### Next steps
{: #next-insight}

Select any of the individual deployment tiles to view more details about that deployment. See [Working with monitoring data](insight-timechart.html).

## Configuration
{: #insight-config-tab}

The Configuration tab ( ![Config tab](images/insight-config-tab.png) ) opens a Configuration Summary for the selected deployment.

  ![Config summary](images/insight-config-summary.png)

From here, you can directly edit the configuration settings for your deployment monitor.

## Transactions
{: #insight-transact-tab}

The Transactions tab ( ![Transactions tab](images/insight-transact-tab.png) ) lets you search a specific transaction ID to explain a particular deployment transaction. For more information, see [Monitoring Explainability](insight-timechart.html#insight-explain).

## AI Tools
{: #insight-tools-tab}

The AI Tools tab ( ![AI Tools tab](images/aitools.png) ) opens a dialog that provides a link to additional IBM AI tools options.

- *[Watson Studio lite plan](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp)*: Watson Studio provides you with the environment and tools to analyze and visualize data, to cleanse and shape data, to ingest streaming data, or to create, train, and deploy machine learning models.

- *[NeuNetS](https://dataplatform.cloud.ibm.com/ml/neunets)* (*Beta*): The Neural Network Synthesizer, or "NeuNetS", currently in beta release, allows you to synthesize AI models using {{site.data.keyword.aios_short}} technology in Watson Studio.

## Help tab
{: #insight-transact-tab}

The Help tab ( ![Transactions tab](images/insight-help-tab.png) ) provides additional information to assist you in using {{site.data.keyword.aios_short}}.
