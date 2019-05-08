---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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
{: #iov-insights}

{{site.data.keyword.aios_short}} ダッシュボードを介して、モニターしているすべてのデプロイメントを追跡できます。このダッシュボードは、{{site.data.keyword.aios_short}} 内へのメイン・ビューです。

  ![「洞察 (Insight)」タブ](images/insight-tabs.png)

{: shortdesc}

## 洞察
{: #iov-dash-tab}

「洞察 (Insights)」タブ (![「洞察 (Insight)」ダッシュボード](images/insight-dash-tab.png)) には、デプロイメントのモニターの概略が示されます。

  ![「洞察 (Insight)」ダッシュボード](images/insight-dashboard.png)

- ***モニター対象デプロイメント (Deployments Monitored)*** - この例では、合計で 10 個のデプロイメントがモニターされています。10 のデプロイメントのうち 8 つは、以下の個々のタイルとして表示されます。

- ***正確度のアラート (Accuracy Alerts)*** - 下記の紫の陰影が付いたタイルに、合計で 3 つの正確度のアラートが示されます。この例では、`「ドライバー・パフォーマンス (Driver Performance)」`、`「市場分析 (Market Analytics)」`、および `「価格リスク (Pricing Risk)」`の各デプロイメントに、正確度の値 `60%`、`65%`、および `79%` がそれぞれ表示されます。

- ***公平性のアラート (Fairness Alerts)*** - 合計で 6 つの公平性のアラートがあります。これらは、ともに紫の陰影付きで、小さな `BIAS` タグの付いた以下のタイルで表されます。この例では、`「ドライバー・パフォーマンス (Driver Performance)」`、`「市場分析 (Market Analytics)」`、`「法規制への適合 (Regulatory Compliance)」`、`「詐欺検出 (Fraud Detection)」`、`「プレミアム最適化 (Premium Optimization)」`、および`「被害額の見積り者 (Damage Cost Estimator)」`の各デプロイメントに、公平性の値 `59%`、`68%`、`62%`、`64%`、`79%`、および `63%` がそれぞれ表示されます。

各タイルには、そのデプロイメントのモニター活動のサマリーがあります。なお、`「コール・センター・ルーティング (Call Center Routing)」`デプロイメント・タイルには問題が表示されていませんが、これはかなり安定した正確なモデルであることを示しています。

個々のデプロイメント・タイルのいずれかを選択して、そのデプロイメントに関する詳細を表示します。[公平性、分当たりの平均要求数、および正確度のモニター](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)を参照してください。

## 構成
{: #iov-config-tab}

「構成 (Configuration)」タブ (![「構成 (Configuration)」タブ](images/insight-config-tab.png)) では、選択したデプロイメントの「構成のサマリー (Configuration Summary)」が開きます。

  ![構成のサマリー](images/insight-config-summary.png)

ここから、デプロイメント・モニターの構成設定を直接編集できます。

## トランザクション
{: #iov-transact-tab}

「トランザクション (Transaction)」タブ (![「トランザクション (Transactions)」タブ](images/insight-transact-tab.png)) を使用すると、特定のデプロイメント・トランザクションを説明するための特定のトランザクション ID を検索できます。詳しくは、[説明可能性のモニター](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov)を参照してください。

## 「ヘルプ」タブ
{: #iov-help-tab}

「ヘルプ」タブ (![「トランザクション (Transactions)」タブ](images/insight-help-tab.png)) には、{{site.data.keyword.aios_short}} を使用する際に役立つ追加情報が提供されます。
