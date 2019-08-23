---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# 效能度量概觀 ![測試版標記](images/beta.png)
{: #anlz_metrics_performance}

使用效能監視來瞭解部署所處理的資料記錄的速度。當您選取要由 {{site.data.keyword.aios_short}} 追蹤及監視的部署時，即啟用效能監視。
{: shortdesc}

效能度量是根據下列資訊來計算：

- 評比有效負載資料

為了達到適當的監視目的，每個評分要求都應該記載在 {{site.data.keyword.aios_short}} 中。對於 {{site.data.keyword.pm_full}} 引擎，會自動進行有效負載資料記載。對於其他機器學習引擎，可以使用 Python 用戶端或 REST API 來提供有效負載資料。效能監視不會在受監視部署上建立任何其他評分要求。

您可以在 {{site.data.keyword.aios_short}} 儀表板上檢閱一段時間的度量值：

![效能圖表](images/performance_metrics_001.png)

## 支援的效能度量
{: #anlz_metrics_performance_supp_quality_mets}

{{site.data.keyword.aios_short}} 支援下列效能度量：

- [傳輸量](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
