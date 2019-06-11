---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# High availability and disaster recovery
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} is highly available within multiple {{site.data.keyword.cloud_notm}} locations, such as Dallas and Washington, DC. However, recovering from potential disasters that affect an entire location requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to re-create an instance of the service in a new location and to restore your data in any location. See [How do I ensure zero downtime? ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} for more information.

## High Availability 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}} is deployed and available on **us-south** data centers with multiple zone routing (MZR) on three availability zones. At any time, if one zone is not available, the system will continue to be available in other availability zones. The global-load balancer and DNS server routes traffic to available zones without any user interruption.

Data that is stored in PostgreSQL databases is also highly available and exists in multiple availability zones. It is, however, the customer’s responsibility to back up data in support of a disaster recovery plan so that services can be re-created.

{{site.data.keyword.aios_short}} traffic is load-balanced across multiple zones in a region. Each zone is a data center in the same region. 

Compose databases, such as PostgreSQL and distributed <code>etc</code> directory (etcd) databases are backed up periodically to ensure high availability and, in the event of disaster, the {{site.data.keyword.aios_short}} operations team will be able to recover service within Recovery Point Objective (RPO).
 
{{site.data.keyword.cloud_notm}} offers in-region data redundancy enabling high availability protection. IBM provides automatic data replication for client databases which contain training and/or custom model data at no additional cost. Replication is completed across in-region availability zones within {{site.data.keyword.cloud_notm}} data centers.
 
## Backup & Restore
{: #openscale-restore}

Clients are responsible for backing up and restoring their own data, including training and/or custom model data as well as any Client generated custom models. For client backup and restore instructions, please see the {{site.data.keyword.cloud_notm}} documentation.
 
## Disaster Recovery
{: #openscale-disaster-recovery}

In-region Business Continuity is completed by leveraging the automatic replication across in-region availability zones within {{site.data.keyword.cloud_notm}} data centers. Clients are responsible for multi-region Disaster Recovery. The responsibilities include backing up, restoring and synching of their own security policies, training and/or custom model data as well as any client generated custom models. In addition, the client is responsible for routing and/or load balancing across the regions. For client backup and restore instructions, see the {{site.data.keyword.cloud_notm}} documentation.