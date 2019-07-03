---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 性能度量概述 ![beta 标记](images/beta.png)
{: #anlz_metrics_performance}

使用性能监视可了解部署处理数据记录的速度。可在选择要由 {{site.data.keyword.aios_short}} 跟踪和监视的部署时启用性能监视。
{: shortdesc}

性能度量的计算是基于以下信息：

- 评分载荷数据

为了进行适当的监视，每个评分请求也应该记录在 {{site.data.keyword.aios_short}} 中。 对于 {{site.data.keyword.pm_full}} 引擎，将自动进行载荷数据记录。对于其他机器学习引擎，可以使用Python客户机或REST API来提供载荷数据。 性能监视不会在受监视的部署上创建任何其他评分请求。

您可以在 {{site.data.keyword.aios_short}} 仪表板上查看一段时间内的性能度量值：

![性能图表](images/performance_metrics_001.png)

## 支持的性能度量
{: #anlz_metrics_performance_supp_quality_mets}

{{site.data.keyword.aios_short}} 支持以下性能度量：

- [吞吐量](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
