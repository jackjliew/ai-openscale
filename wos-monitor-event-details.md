---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: events, applications, monitor, configuration, event details, details

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

# Configuring event details in {{site.data.keyword.aios_short}}
{: #event-dets-monitor}

After you configure the application monitor and KPIs, you must supply event details to your monitor. You can do this in one of the following ways: by uploading a file with the details or by manually entering the information in the event details table.
{: shortdesc}

## Requirements
{: #event-dets-config-reqs}

On the **Event details** tab, you must provide the following information:

### Transaction ID
{: #event-dets-config-reqs-trxn_id}

The transaction ID field is required to map business key performance indicators (KPIs). It is the unique identifier for the business event. It must be a **text** data type and match exactly the identifier in the business event payload data.

### Timestamp
{: #event-dets-config-reqs-timestamp}

So that data is tracked by date and time, you must provide a timestamp. The timestamp is a required field so that transactions over time can align properly. It must be a **date** data type and match exactly the identifier in the business event payload data.

### Property name
{: #event-dets-config-reqs-property-name}

Enter the propery name as it appears in the business events payload.

### Description
{: #event-dets-config-reqs-descriptionofevent}

Type a free-form description to help you understand the event.

### Data type
{: #event-dets-config-reqs-data-type}

Select a data type from the drop-down box. The data type that you select here must match the data type in the events detail payload.

### Unit label
{: #event-dets-config-reqs-unit-label}

Type a free-form label, such as USD or Euros to provide context to the data.

## Steps to manually create event details
{: #event-dets-config}

1. From the **Insights dashboard**, on the **Application monitors** tab, click the **Add to dashboard** button to create a new application.
1. In the **Application name** field, type **the name of the application**, and then click **Configure**.
1. In the **Associated models** section, click the **Add associated model** button.
1. Select the **model** deployment, and then click **Save**.
1. In the **Event details** section, click **Enter event data manually**.
1. Fill out data for each event and click **Save**.


## Steps to create event details by uploading a file
{: #event-dets-config}

1. From the **Insights dashboard**, on the **Application monitors** tab, click the **Add to dashboard** button to create a new application.
1. In the **Application name** field, type **the name of the application**, and then click **Configure**.
1. In the **Associated models** section, click the **Add associated model** button.
1. Select the **model** deployment, and then click **Save**.
1. In the **Event details** section, click **Load event data from file**.
1. Download the **events detail** file.
1. Select the downloaded file, and then click **Save**.

### Next steps
{: #event-dets-next}

- [View correlation charts](/docs/services/ai-openscale?topic=ai-openscale-app-perform-vdet).
- [View KPI performance](/docs/services/ai-openscale?topic=ai-openscale-it-appkpi-vdet).
