---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# 高可用性和灾难恢复
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} 在多个 {{site.data.keyword.cloud_notm}} 位置（如达拉斯和华盛顿）中高度可用。但是，从影响整个位置的潜在灾难中恢复需要规划和准备。
{: shortdesc}

您负责了解服务的配置、定制和使用情况。您还负责准备就绪在新位置重新创建服务实例以及在任何位置复原数据。有关更多信息，请参阅[如何确保零停机时间？](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external}。

## 高可用性 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}} 部署在 **us-south** 数据中心上并可用，这些数据中心在三个可用性专区中进行多专区路由 (MZR)。在任何时候，如果一个专区不可用，那么系统将继续在其他可用性专区中可用。全局负载均衡器和 DNS 服务器在没有任何用户中断的情况下将流量路由到可用性专区。

存储在 PostgreSQL 数据库中的数据也高度可用，并且存在于多个可用性专区中。但是，由客户负责备份数据来支持灾难恢复计划，以便能够重新创建服务。

{{site.data.keyword.aios_short}} 流量在某个区域中的多个专区之间进行了负载均衡。每个专区都是同一区域中的一个数据中心。 

PostgreSQL 数据库和分布式 <code>etc</code> 目录 (etcd) 数据库之类的 Compose 数据库会定期备份，以确保高可用性，并且在发生灾难的情况下，{{site.data.keyword.aios_short}} 操作团队将能够在恢复点目标 (RPO) 内恢复服务。
 
{{site.data.keyword.cloud_notm}} 提供支持高可用性保护的区域内数据冗余。IBM 为包含训练和/或定制模型数据的客户数据库提供自动数据复制，而没有任何额外成本。将在 {{site.data.keyword.cloud_notm}} 数据中心内的区域内可用性专区中完成复制。
 
## 备份和复原
{: #openscale-restore}

客户负责备份和复原其自己的数据，包括训练和/或定制模型数据以及任何客户生成的定制模型。有关客户备份和复原指示信息，请参阅 {{site.data.keyword.cloud_notm}} 文档。
 
## 灾难恢复
{: #openscale-disaster-recovery}

通过利用 {{site.data.keyword.cloud_notm}} 数据中心内的区域内可用性专区中的自动复制，可完成区域内业务连续性。客户负责执行多区域灾难恢复。职责包括备份、复原和同步其自己的安全策略，训练和/或定制模型数据以及任何客户生成的定制模型。此外，客户还负责跨区域路由和/或负载均衡。有关客户备份和复原指示信息，请参阅 {{site.data.keyword.cloud_notm}} 文档。
