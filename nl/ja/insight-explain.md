---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 説明可能性のモニター
{: #ie-ov}

デプロイメントごとに、特定のトランザクションの説明可能性データを確認できます。
{: shortdesc}

## トランザクションの説明
{: #ie-view}

選択したデプロイメント・タイルで、ナビゲーターの**「トランザクションの説明 (Explain a transaction)」**タブ (![「トランザクションの説明 (Explain a transaction)」タブ](images/insight-transact-tab.png)) を選択して、トランザクション ID を入力します。

スコアリングのためにデータがモデルに送信されるたびに、`X-Global-Transaction-Id` フィールドが設定されて、HTTP ヘッダーにトランザクション ID が設定されます。このトランザクション ID は、ペイロード・テーブルに保管されます。特定のスコアリングのモデルの動作の説明を見つけるには、そのスコアリング要求に関連付けられたトランザクション ID を指定します。この動作は、Watson Machine Learning (WML) トランザクションにのみ適用され、WML 以外のトランザクションには適用されません。
{: note}

### {{site.data.keyword.aios_short}} でのトランザクション ID の検索
{: #ie-find}

1.  デプロイメントの時間グラフから、グラフでマーカーをスライドさせて**「詳細の表示 (View details)」**リンクをクリックし、[特定時間のデータを可視化](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual)します。
1.  **「トランザクションの表示 (View transactions)」**ボタンをクリックして、[トランザクション ID のリストを表示](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-tra)します。
1.  リストからいずれかのトランザクション ID をコピーして、**「トランザクションの説明 (Explain a transaction)」**ページの検索ボックスに貼り付け、Enter キーを押します。

    トランザクション ID のリストでは、単に任意のトランザクション ID の「アクション (Action)」列の**「説明 (Explain)」**リンクをクリックするというオプションもあります。そうすると、「説明可能性 (Explainability)」タブでそのトランザクションが開かれます。
    {: note}

  さまざまなタイプのモデルの説明の例については、以下のセクションを参照してください。

  ![説明可能性のトランザクション ID](images/insight-explain-trans-id.png)

## カテゴリー・モデルの例
{: #ie-class}

この説明可能性の例は、保険金請求を承認または拒否するバイナリー分類モデルに関するものです。この場合、`DENIED` という最終的な結果に対して、肯定的または否定的な影響を与えた要因を確認できます。

DENIED という結果を判別する際に、モデルに最大の影響を与えたのは、値が `< 1 year` であるフィーチャー *POLICY AGE* です。この結果に影響を与えたその他のフィーチャーは、*CLAIM FREQUENCY* (`High`) と *AGE* (`18`) でした。この場合、*CAR VALUE* (`$50,000`) からの影響は、小さなものに過ぎません。

![説明可能性の二項分類](images/insight-explain-binary.png)

グラフは、トランザクションの結果の判別に最も重要な要因を示す場合に有用ですが、分類モデルに詳細な説明を含めることもできます。これらについては、`「承認された結果の最小限の変更 (Minimum changes for Approved outcome)」`セクションと`「この結果の最小限の変更 (Minimum changes for this outcome)」`セクションに説明があります。

回帰、イメージ、および非構造化テキストの各モデルの詳細な説明はありません。
{: note}

`「承認された結果の最小限の変更 (Minimum changes for Approved outcome)」`は、フィーチャーの値がこのセクションにリストされている値に変更された場合、モデルの予測が変更されることを示しています。

同様に、`「この結果の最小限の変更 (Minimum changes for this outcome)」`は、フィーチャーの値がこのセクションにリストされている値に変更された場合であっても、モデルの予測は変更されないことを示します。

したがって、これら 2 つの値は、説明が生成されているデータ・ポイント周辺のモデルの動作を示しています。

![説明可能性の二項分類](images/insight-explain-binary2.png)

## イメージ・モデルの例
{: #ie-image}

説明可能性のイメージ分類モデルの例では、予測された結果に肯定的な影響を与えたイメージの部分と、否定的な影響を与えたイメージの部分を確認できます。下記の例では、予測に肯定的な影響を与えた部分が右側のイメージに表示され、結果に否定的な影響を与えたイメージの部分が左側のイメージに表示されます。

現在、サイズが 1 MB より大きいイメージの説明は生成できません。
{: note}

![説明可能性のイメージの分類](images/insight-explain-image.png)

## 非構造化テキスト・モデルの例
{: #ie-unstruct}

最後に、この説明可能性の例には、非構造化テキストを評価する分類モデルが示されます。説明には、モデルの予測に肯定的な影響と否定的な影響を与えたキーワードが示されます。モデルへの入力としてフィードされた、元のテキスト内の識別されたキーワードの位置も示されます。

![説明可能性のイメージの分類](images/insight-explain-text.png)
