---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# ダッシュボードのナビゲート
{: #io-ov}

モニターしているすべてのデプロイメントは、{{site.data.keyword.aios_short}} ダッシュボードで追跡できます。ダッシュボードは、{{site.data.keyword.aios_short}} の主要なビューです。ダッシュボードは 5 つのタブで構成されています。

  ![「インサイト」タブ](images/insight-tabs.png)

{: shortdesc}

## インサイト
{: #io-ins}

**「インサイト」**タブ (![「インサイト」ダッシュボード ](images/insight-dash-tab.png)) は、デプロイメント・モニタリングの概略を示します。

  ![「インサイト」ダッシュボード](images/insight-dashboard.png)

- ***デプロイメント・モニター済み*** - この例では、合計 10 個のデプロイメントがモニターされています。10 個の中の 8 個のデプロイメントは、下の個々のタイルで示されます。

- ***正確度アラート*** - 下のタイルで合計 3 個の正確度アラートが紫の陰影付けで表されています。この例では、`Driver Performance` デプロイメント、`Market Analytics` デプロイメント、`Pricing Risk` デプロイメントで、正確度の値がそれぞれ `60%`、`65%`、`79%` になっています。

- ***公平性アラート*** - ここには合計 6 個の公平性アラートがあり、下のタイルでは紫の陰影付けと小さな `BIAS` タグの両方で表されます。この例では、`Driver Performance`、`Market Analytics`、`Regulatory Compliance`、`Fraud Detection`、`Premium Optimization`、および `Damage Cost Estimator` の各デプロイメントで、公平性の値がそれぞれ `59%`、`68%`、`62%`、`64%`、`79%`、`63%` になっています。

.各タイルは、そのデプロイメントのモニタリング・アクティビティーの要約を示します。`Call Center Routing` デプロイメント・タイルは何の問題も示されていないことに注目してください。これは、かなり安定した、正確なモデルであることを示しています。

### 次のステップ
{: #io-next}

個々のデプロイメント・タイルを選択すると、そのデプロイメントについてより詳しく調べることができます。詳しくは、[公平性、毎分平均要求数、正確度のモニター](/docs/services/ai-openscale?topic=ai-openscale-it-ov)および[説明可能性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。

## 構成
{: #io-conf}

**「構成」**タブ (![「構成」タブ](images/insight-config-tab.png)) を使用すると、選択したデプロイメントに対応する「構成の要約」が開きます。

  ![構成の要約](images/insight-config-summary.png)

この場所からデプロイメント・モニターの構成設定を直接編集できます。

## トランザクション
{: #io-tran}

**「トランザクションの説明」**タブ (![「トランザクションの説明」タブ](images/insight-transact-tab.png)) では、個々のデプロイメント・トランザクションを説明する特定のトランザクション ID を検索できます。詳しくは、[説明可能性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。

## AI ツール
{: #io-too}

**「AI ツール」**タブ (![「AI ツール」タブ](images/aitools.png)) を使用すると、追加の IBM AI ツール・オプションへのリンクがあるダイアログが開きます。

- *[Watson Studio Lite プラン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*: Watson Studio は、データの分析と視覚化、データの浄化と具体化、ストリーミング・データの取り込み、または、機械学習モデルの作成、トレーニング、デプロイを行うための環境とツールを提供しています。「無料の Watson Studio ライト・プランに登録」リンクをクリックして、Watson Studio を入手してください。

- *[NeuNetS ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}* (*ベータ*): Neural Network Synthesizer (略称「NeuNetS」) は現在、ベータ版がリリースされており、Watson Studio で {{site.data.keyword.aios_short}} テクノロジーを使用して AI モデルを合成できます。「モデルの同期」ボタンをクリックして、NeuNetS を操作してください。

  ![NeuNetS ダイアログ](images/neunets-dialog.png)

## 「ヘルプ」タブ
{: #io-help}

「ヘルプ」タブ (![「トランザクション」タブ](images/insight-help-tab.png)) は、{{site.data.keyword.aios_short}} の使用に際してユーザーを支援する追加情報を提供します。
