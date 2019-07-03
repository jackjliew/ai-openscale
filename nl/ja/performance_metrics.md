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

# パフォーマンス指標の概要 ![ベータ・タグ](images/beta.png)
{: #anlz_metrics_performance}

デプロイメントで処理されるデータ・レコードの速度を知るには、パフォーマンス・モニタリングを使用します。 {{site.data.keyword.aios_short}} で追跡してモニターするデプロイメントを選択すると、パフォーマンス・モニタリングが有効になります。
{: shortdesc}

パフォーマンス指標は、以下の情報に基づいて計算されます。

- ペイロード・データの評価

適切なモニタリングのために、すべての評価要求は {{site.data.keyword.aios_short}} でログ記録する必要もあります。 {{site.data.keyword.pm_full}} エンジンの場合、ペイロード・データのロギングは自動化されています。 その他の機械学習エンジンの場合、Python クライアントか REST API を使用してペイロード・データを提供できます。 パフォーマンス・モニタリングでは、モニター対象のデプロイメントに関する追加の評価要求は作成されません。

{{site.data.keyword.aios_short}} ダッシュボードで、パフォーマンス指標値を経時的に確認できます。

![パフォーマンスのグラフ](images/performance_metrics_001.png)

## サポートされているパフォーマンス指標
{: #anlz_metrics_performance_supp_quality_mets}

以下のパフォーマンス指標が {{site.data.keyword.aios_short}} によってサポートされています。

- [スループット](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
