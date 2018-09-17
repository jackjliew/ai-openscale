---

copyright:
  years: 2015, 2018
lastupdated: "2018-9-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# About

{{site.data.keyword.aios_full}} is an enterprise-grade environment for AI-infused applications, providing enterprises visibility into how AI is being built, used, and delivering return on investment at the scale of your business.
{: shortdesc}

## Implementation

Here's how you will implement {{site.data.keyword.aios_short}}:

- **Configure {{site.data.keyword.aios_short}}**: With the easy-to-use graphical environment, [set up a payload logging database](connect-db.html), and the [Watson Machine Learning instance](connect-wml.html) where your AI models and deployments are stored.

- **Work with monitors**: For each deployment, configure how {{site.data.keyword.aios_short}} will monitor that deployment. You can monitor for:

    - [Fairness](monitor-fairness.html)
    - [Accuracy](monitor-accuracy.html)
    - [Explainability](monitor-explain.html)

- **View and edit monitored data**: The {{site.data.keyword.aios_short}} [dashboard](insight-overview.html) lets you easily view key insights and identify issues for your deployments. Visualization of individual data points for each monitored feature provides additional detail.

## Limitations

- The current release only supports one PostgreSQL database, one Watson Machine Learning instance, and one instance of {{site.data.keyword.aios_short}}

- The PostgreSQL database and Watson Machine Learning instance must be deployed in the same {{site.data.keyword.Bluemix_notm}} account.

- There is a license limit of 20 deployed models per instance of {{site.data.keyword.aios_short}}.

## Supported machine learning engines

Table 1. Feature support details

| ML engine | **Performance** | **Accuracy monitoring** | **Fairness detection** | **Payload logging** | **Explainability**
|:---|:---:|:---:|:---:|:---:|:---|
| **Watson Machine Learning**  | Yes | Yes | Yes | Yes | Yes |
| **Generic Machine Learning service**         | No | No | No | Yes | No ||
{: caption="Feature support details" caption-side="top"}

## Supported Watson machine learning frameworks and functions

Table 1. Feature support details

| Framework | **performance** | **Accuracy monitoring** | **Fairness detection** | **Payload logging** | **Explainability**
|:---|:---:|:---:|:---:|:---:|:---:|
| **spark mllib**        | Yes | Yes | Yes* | Yes | Yes* |
| **scikit-learn**       | Yes | No | No | No | No |
| **xgboost**            | Yes | No | No | No | No |
| **pmml**               | Yes | No | No | No | No |
| **spss**               | Yes | No | No | No | No |
| **keras**              | Yes | Yes** | Yes* | Yes | Yes* |
| **tensorflow**         | Yes | Yes** | Yes* | Yes | Yes* |
| **caffe**              | Yes | No | No | No | No |
| **pytorch**            | Yes | No | No | No | No |
| **python functions**   | Yes | No | Yes* | Yes | No ||
{: caption="Feature support details" caption-side="top"}

`*` Fairness detection and explainability require payload logging to be supported; they also need a WML scoring endpoint to be available.

`**` New version of model only, no evaluation.

## Browser support

The {{site.data.keyword.aios_short}} service tooling requires the same level of browser software as is required by {{site.data.keyword.Bluemix_notm}}. See the {{site.data.keyword.Bluemix_notm}} [Prerequisites ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/overview/prereqs.html#browsers){: new_window} topic for details.

## Next steps

- [Get started](getting-started.html) with the service.
- View the [API Reference material ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/ai-openscale){: new_window}.

Still have questions? [Contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
