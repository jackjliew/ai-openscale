---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: dashboard, navigating, navigation, insights

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

# {{site.data.keyword.aios_short}} のインサイトの取得
{: #io-ov}

モニターしているすべてのデプロイメントは、{{site.data.keyword.aios_full}} ダッシュボードで追跡できます。 ダッシュボードは、{{site.data.keyword.aios_short}} のメインのビューです。ここで、モデルの動作に関するインサイトを得ることができます。
{: shortdesc}

## インサイト
{: #io-ins}

**「インサイト」**タブ (![「インサイト」ダッシュボード ](images/insight-dash-tab.png)) は、デプロイメント・モニタリングの概略を示します。

  ![「インサイト」ダッシュボード](images/insight-dashboard.png)

- ***デプロイメント・モニター済み*** - この例では、合計 10 個のデプロイメントがモニターされています。 以下の 10 個の中の 8 個のデプロイメントは、個々のタイルで示されます。

- ***正解率の警告*** - 下のタイルで合計 3 個の正解率の警告が表されています。 この例では、`Driver Performance` デプロイメント、`Market Analytics` デプロイメント、`Pricing Risk` デプロイメントで、正解率の値がそれぞれ `60%`、`65%`、`79%` になっています。

- ***公平性の警告*** - 合計で 6 つの公平性の警告があります。これらは、小さな `BIAS` タグの付いた以下のタイルで表されます。 この例では、`Driver Performance`、`Market Analytics`、`Regulatory Compliance`、`Fraud Detection`、`Premium Optimization`、および `Damage Cost Estimator` の各デプロイメントで、公平性の値がそれぞれ `59%`、`68%`、`62%`、`64%`、`79%`、`63%` になっています。

各タイルは、そのデプロイメントのモニタリング・アクティビティーの要約を示します。 `Call Center Routing` デプロイメント・タイルは何の問題も示されていないことに注目してください。これは、かなり安定した、正確なモデルであることを示しています。

### 次のステップ
{: #io-next}

個々のデプロイメント・タイルを選択すると、そのデプロイメントについてより詳しく調べることができます。 詳しくは、[公平性、毎分平均リクエスト数、正解率のモニター](/docs/services/ai-openscale?topic=ai-openscale-it-ov)および[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。



## トランザクション
{: #io-tran}

個々のデプロイメント・トランザクションを説明するための特定のトランザクション ID を検索するには、**「トランザクションの説明」**タブ (![「トランザクションの説明」タブ](images/insight-transact-tab.png)) を使用します。 詳しくは、[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。


