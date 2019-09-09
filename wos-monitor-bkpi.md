---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: KPIs, applications, monitor, configuration 

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

# Configuring KPI metrics in {{site.data.keyword.aios_short}}
{: #kpi-monitor}

After you configure the application monitor, you must add key performance indicators to your monitor. 
{: shortdesc}

## Requirements
{: #kpi-config-reqs}

On the successive pages of the **Application** tab, you must provide the following information:

### KPI name and description
{: #kpi-config-reqs-name}

You must give your KPI a name and, optionally, a description. 

### Calculation
{: #kpi-config-reqs-num-ev-dets}

In the **Numeric evaluation details** pane you must select the type of numeric evaluation that is performed on the KPI. You can choose from several mathematcial operators, such as summation or average.

### Numeric operation
{: #kpi-config-reqs-sumtocalc}

Depending on the mathematical operator you choose, you must select the details of the operation.

### Upper or Lower Threshold
{: #kpi-config-reqs-threshold}

Choose either an upper or lower threshold for the alert. Then enter a numeric value for the threshold that {{site.data.keyword.aios_short}} uses for alerting user to data drift.

### Logging endpoint activation
{: #kpi-config-reqs-logging-activation}

To activate the application, along with any of the KPIs that you created, you must upload the business payload file, which is in the form of a .csv file.

## Steps
{: #kpi-config}

1. To start the configuration process, from the 
2. Follow the prompts and enter required information. When you finish, a summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section, otherwise, save your work.
3. A summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section. Otherwise, click **Save** to complete your configuration.

### Next steps
{: #kpi-next}

- [View correlation charts](/docs/services/ai-openscale?topic=ai-openscale-app-perform-vdet).
- [View KPI performance](/docs/services/ai-openscale?topic=ai-openscale-it-appkpi-vdet).
