---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-06"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Navigating the dashboard
{: #io-ov}

You can track all the deployments you are monitoring through the {{site.data.keyword.aios_short}} dashboard. The dashboard is your main view into {{site.data.keyword.aios_short}}. The dashboard consists of five tabs:

  ![Insight tabs](images/insight-tabs.png)

{: shortdesc}

## Insights
{: #io-ins}

The **Insights** tab ( ![Insight dashboard](images/insight-dash-tab.png) ) provides a high-level view of your deployment monitoring.

  ![Insight dashboard](images/insight-dashboard.png)

- ***Deployments Monitored*** - In this example, a total of 10 deployments are being monitored. Eight of the ten deployments are shown as individual tiles below.

- ***Accuracy Alerts*** - A total of 3 Accuracy alerts are represented in the tiles below by purple shading. In this example, the `Driver Performance`, `Market Analytics`, and `Pricing Risk` deployments show Accuracy values of `60%`, `65%`, and `79%`, respectively.

- ***Fairness Alerts*** - There are a total of 6 Fairness alerts, represented in the tiles below by both purple shading, and by a small `BIAS` tag. In this example, the `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization`, and `Damage Cost Estimator` deployments show Fairness values of `59%`, `68%`, `62%`, `64%`, `79%`, and `63%`, respectively.

Each tile provides a summary of monitoring activity for that deployment. Note that the `Call Center Routing` deployment tile shows no issues, indicating a fairly stable, accurate model.

### Next steps
{: #io-next}

Select any of the individual deployment tiles to view more details about that deployment. For more information, see [Monitoring Fairness, Average Requests per Minute, and Accuracy](/docs/services/ai-openscale?topic=ai-openscale-it-ov) and [Monitoring explainability](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Configuration
{: #io-conf}

The **Configure** tab ( ![Config tab](images/insight-config-tab.png) ) opens a Configuration Summary for the selected deployment.

  ![Config summary](images/insight-config-summary.png)

From here, you can directly edit the configuration settings for your deployment monitor.

## Transactions
{: #io-tran}

The **Explain a transaction** tab ( ![Explain a transaction tab](images/insight-transact-tab.png) ) lets you search a specific transaction ID to explain a particular deployment transaction. For more information, see [Monitoring explainability](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## AI Tools
{: #io-too}

The **AI Tools** tab ( ![AI Tools tab](images/aitools.png) ) opens a dialog that provides a link to additional IBM AI tools options:

- *[Watson Studio lite plan ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*: Watson Studio provides you with the environment and tools to analyze and visualize data, to cleanse and shape data, to ingest streaming data, or to create, train, and deploy machine learning models. Click the "Sign up for the free Watson Studio Lite plan" link to get Watson Studio.

- *[NeuNetS ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}* (*Beta*): The Neural Network Synthesizer, or "NeuNetS", currently in beta release, allows you to synthesize AI models using {{site.data.keyword.aios_short}} technology in Watson Studio. Click the "Synthesize a model" button to work with NeuNetS.

  ![NeuNetS dialog](images/neunets-dialog.png)

## Help tab
{: #io-help}

The Help tab ( ![Transactions tab](images/insight-help-tab.png) ) provides additional information to assist you in using {{site.data.keyword.aios_short}}.
