---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# トランザクションの説明
{: #ie-ov}

デプロイメントごとに、特定のトランザクションについての説明性データを表示することができます。トランザクションが表示されるのは、モニタリングをサポートするデータが存在しており、そのデータが、設定したしきい値、モニタリングの実行予定時刻、および {{site.data.keyword.pm_full}} からのペイロード・データの可用性に基づいている場合のみです。
{: shortdesc}

## トランザクション ID を使用した説明の表示
{: #ie-view}

1. デプロイメント・タイルをクリックします。
2. ナビゲーターで**「トランザクションの説明」**タブ (![「トランザクションの説明」タブ](images/insight-transact-tab.png)) をクリックします。
3. トランザクション ID を入力します。

予測のためにデータがモデルに送信されるたびに、HTTP ヘッダーの `X-Global-Transaction-Id` フィールドにトランザクション ID が設定されます。 このトランザクション ID はペイロード・テーブルに保管されます。 特定の予測のモデルの動作の説明を見つけるには、その評価要求に関連付けられたトランザクション ID を指定します。 この動作は {{site.data.keyword.pm_full}} トランザクションにのみ適用され、WML 以外のトランザクションには適用されないことに注意してください。
{: note}

## {{site.data.keyword.aios_short}} でのトランザクション ID の検出
{: #ie-find}

1.  デプロイメントの時系列グラフにあるマーカーをグラフの上でスライドさせ、**「詳細を表示します」**リンクをクリックして、[特定時間のデータを視覚化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)します。
1.  **「トランザクションの表示」**ボタンをクリックして、[トランザクション ID のリストを表示](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)します。
1.  リストにあるいずれかのトランザクション ID をコピーして、それを**「トランザクションの説明」**ページの検索ボックスに貼り付け、Enter キーを押します。

    トランザクション ID のリストでは、トランザクションを「説明性」タブで簡単に開くオプションがあります。これを行うには、任意のトランザクション ID の「アクション」列で**「説明」**リンクをクリックします。
    {: note}

  さまざまなモデルのタイプに対する説明の例については、以下のセクションを参照してください。

  ![説明性のトランザクション ID](images/insight-explain-trans-id.png)

## グラフの詳細での説明の検索
{: #ie-view-ui}

公平性指標とドリフト指標を対象とした説明が存在しているので、グラフをクリックしてデータ・セットの詳細ビューを表示してから、公平性指標の**「トランザクションの表示」**ボタンをクリックするか、またはドリフト・トランザクション・タイルをクリックして、トランザクションの説明を表示します。

- いずれかの公平性属性 (性別や年齢など) について属性をクリックしてからグラフをクリックし、**「トランザクションの表示」**ボタンをクリックします。
- ドリフト・モニタリングの場合は**「ドリフト絶対値 (Drift magnitude)」**をクリックしてからグラフをクリックし、タイルをクリックして、特定のドリフト・グループに関連付けられているトランザクションを表示します。

## 次のステップ
{: #ie-trans-id-next}

- [分類モデルの説明](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [画像モデルの説明](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [非構造化テキスト・モデルの説明](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [対比的説明](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
