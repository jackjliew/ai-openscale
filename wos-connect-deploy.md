---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: deployment, monitoring 

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

# Select deployments to monitor
{: #dpl-select}

To add monitors to the {{site.data.keyword.aios_short}} dashboard, you must have deployed models that are available through one of the machine learning providers that you have configured for {{site.data.keyword.aios_short}}. Select from a list of machine learning providers and deployments to monitor.
{: shortdesc}

## Choosing deployments
{: #dpl-config}

1.  From the {{site.data.keyword.aios_short}} dashboard, click **Add to dashboard**.
1.  {{site.data.keyword.aios_short}} checks your machine learning providers to compile a list of deployed models. From the list of deployments, you can select the ones that you want to monitor.

    ![Select deployments](images/wos-select-model-deployment.png)

1.  Click **Configure**.

You have successfully selected deployments to monitor. You must now configure the monitors for this model. 

## Next steps
{: #dpl-next}

{{site.data.keyword.aios_short}} is now ready for you to [configure monitors](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
