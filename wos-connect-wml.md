---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Specifying an {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} service instance
{: #wml-connect}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify an {{site.data.keyword.pm_full}} instance. Your {{site.data.keyword.pm_short}} instance is where you store your AI models and deployments.
{: shortdesc}

## Prerequisites
{: #wml-prereq}

You should have provisioned an {{site.data.keyword.pm_full}} instance in the same {{site.data.keyword.Bluemix_notm}} account where the {{site.data.keyword.aios_short}} service instance is present. If you have provisioned a {{site.data.keyword.pm_full}} instance in some other account, then you will not be able to configure that instance with automatic payload logging with {{site.data.keyword.aios_short}}.

## Connect your {{site.data.keyword.pm_short}} service instance
{: #wml-config}

{{site.data.keyword.aios_short}} connects to AI models and deployments in an {{site.data.keyword.pm_full}} instance.

1.  From the **Configure** tab, click **Machine learning provider**.

    ![the select your machine learning service provider screen is shown with tiles for the supported machine learning engines](images/wos-machine-learning-providers-selection.png)

2.  Select the {{site.data.keyword.pm_full}} tile. {{site.data.keyword.aios_short}} checks your {{site.data.keyword.Bluemix_notm}} account to locate any existing {{site.data.keyword.pm_full}} instances. 
3. Select an instance from the **Watson Machine Learning service** drop-down menu.

    ![Select {{site.data.keyword.pm_short}} service](images/gs-set-wml.png)

4.  (Optional) You also have the option to **Select a different location**, to specify a machine learning location outside of your {{site.data.keyword.Bluemix_notm}} account. Provide credentials for your location as valid JSON:

    ![Set {{site.data.keyword.pm_short}} instance](images/gs-get-wml.png)

    Click **Save**.

1.  {{site.data.keyword.aios_short}} lists your deployed models; select the ones you want to monitor and click **Configure**.

### Next steps
{: #wml-next}

{{site.data.keyword.aios_short}} is now ready for you to [configure monitors](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
