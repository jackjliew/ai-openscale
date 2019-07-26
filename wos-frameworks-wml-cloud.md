---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #frmwrks-wml}

You can use {{site.data.keyword.pm_full}} to perform payload logging, feedback logging, and to measure performance accuracy, run-time bias detection, explainability, and auto-debias function in {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} fully supports the following {{site.data.keyword.pm_full}} frameworks: 
{: shortdesc}

Table 1. Framework support details

| Framework | Problem type | Data type |
|:---|:---:|:---:|
| Apache Spark MLlib | Classification | Structured |
| Python function | Classification | Structured |
| Python function | Regression | Structured |
| XGBoost | Classification | Structured |
| XGBoost | Regression | Structured |
| scikit-learn | Classification | Structured |
| scikit-learn | Regression | Structured |
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Classification | Unstructured (image, text) |
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Regression | Unstructured (image, text) |
| Apache Spark MLLib | Regression | Structured |
{: caption="Framework support details" caption-side="top"}

<sup>1</sup>Keras support does not include support for fairness.
{: note}

<sup>2</sup>Explainability is supported if your model / framework outputs prediction probabilities.
{: note}

## Specifying an {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} service instance
{: #wml-connect}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify an {{site.data.keyword.pm_full}} instance. Your {{site.data.keyword.pm_short}} instance is where you store your AI models and deployments.
{: shortdesc}

### Prerequisites
{: #wml-prereq}

You should have provisioned an {{site.data.keyword.pm_full}} instance in the same {{site.data.keyword.Bluemix_notm}} account where the {{site.data.keyword.aios_short}} service instance is present. If you have provisioned a {{site.data.keyword.pm_full}} instance in some other account, then you will not be able to configure that instance with automatic payload logging with {{site.data.keyword.aios_short}}.

### Connect your {{site.data.keyword.pm_short}} service instance
{: #wml-config}

{{site.data.keyword.aios_short}} connects to AI models and deployments in an {{site.data.keyword.pm_full}} instance.

1.  From the **Configure** tab, in the navigation pane, click **Machine learning providers**.

    ![the select your machine learning service provider screen is shown with tiles for the supported machine learning engines](images/wos-machine-learning-providers-selection.png)

2.  Click the **Add machine learning provider** button, and then click the {{site.data.keyword.pm_full}} tile. {{site.data.keyword.aios_short}} checks your {{site.data.keyword.Bluemix_notm}} account to locate any existing {{site.data.keyword.pm_full}} instances. 
3. Select an instance from the **Watson Machine Learning service** drop-down menu.

    ![Select {{site.data.keyword.pm_short}} service](images/gs-set-wml.png)

4.  (Optional) You also have the option to **Select a different location**, to specify a machine learning location outside of your {{site.data.keyword.Bluemix_notm}} account. Provide credentials for your location as valid JSON:

    ![Set {{site.data.keyword.pm_short}} instance](images/gs-get-wml.png)

    Click **Save**.

1.  {{site.data.keyword.aios_short}} lists your deployed models; select the ones you want to monitor and click **Configure**.

## Next steps
{: #wml-next}

{{site.data.keyword.aios_short}} is now ready for you to [configure monitors](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
