---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# トランザクションの説明
{: #ie-ov}

デプロイメントごとに、特定のトランザクションについての説明性データを表示することができます。
{: shortdesc}

## トランザクションの説明
{: #ie-view}

選択したデプロイメント・タイルでナビゲーターの**「トランザクションの説明」**タブ (![「トランザクションの説明」タブ](images/insight-transact-tab.png)) を選択し、トランザクション ID を入力します。

予測のためにデータがモデルに送信されるたびに、HTTP ヘッダーの `X-Global-Transaction-Id` フィールドにトランザクション ID が設定されます。 このトランザクション ID はペイロード・テーブルに保管されます。 特定の予測のモデルの動作の説明を見つけるには、その予測リクエストに関連付けられたトランザクション ID を指定します。 この動作は Watson Machine Learning (WML) トランザクションにのみ適用され、WML 以外のトランザクションには適用されないことに注意してください。
{: note}

### {{site.data.keyword.aios_short}} でのトランザクション ID の検出
{: #ie-find}

1.  デプロイメントの時系列グラフにあるマーカーをグラフの上でスライドさせ、**「詳細を表示します」**リンクをクリックして、[特定時間のデータを視覚化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)します。
1.  **「トランザクションの表示」**ボタンをクリックして、[トランザクション ID のリストを表示](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)します。
1.  リストにあるいずれかのトランザクション ID をコピーして、それを**「トランザクションの説明」**ページの検索ボックスに貼り付け、Enter キーを押します。

    トランザクション ID のリストでは、トランザクションを「説明性」タブで簡単に開くオプションがあります。これを行うには、任意のトランザクション ID の「アクション」列で**「説明」**リンクをクリックします。
    {: note}

  さまざまなモデルのタイプに対する説明の例については、以下のセクションを参照してください。

  ![説明性のトランザクション ID](images/insight-explain-trans-id.png)

## カテゴリカル・モデルの例
{: #ie-class}

この説明性の例は、保険金請求を承認または拒否する二項分類モデルを示すものです。 この事例の最終結果が `DENIED` (拒否) になった原因となるプラス要因とマイナス要因を読み取ることができます。

特徴量 *POLICY AGE* の値が `< 1 year` であることが、モデルで DENIED の結果を決定する上で最大の影響がありました。 この結果の原因となった他の特徴量には、*CLAIM FREQUENCY* (`High`) および *AGE* (`18`) があり、また、ほんのわずかな影響ですが *CAR VALUE* (`$50,000`) がありました。

![説明性の二項分類](images/insight-explain-binary.png)

グラフは、トランザクションの結果を決定する最も有意な要因を示す上で役立ちますが、分類モデルには詳細説明も含まれる場合があります。これについては、`承認結果を導く最小の変更 (Minimum changes for Approved outcome)` および`この結果を導く最小の変更 (Minimum changes for this outcome)` のセクションで詳しく説明されています。

回帰、イメージ、および非構造化テキストのモデルでは、詳細説明は提供されません。
{: note}

`承認結果を導く最小の変更 (Minimum changes for Approved outcome)` は、特徴量の値がこのセクションにリストされている値に変更された場合に、モデルの予測が変わることを示します。

同様に、`この結果を導く最小の変更 (Minimum changes for this outcome)` は、特徴量の値がこのセクションにリストされた値に変更されても、モデルの予測は変わらないことを示します。

このため、これらの 2 つの値は、説明が生成されたデータ・ポイントの近辺でのモデルの振る舞いを示します。

![説明性の二項分類](images/insight-explain-binary2.png)

## 画像モデルの例
{: #ie-image}

説明性の例が画像分類モデルである場合、画像のどの部分が予測結果のプラス要因となり、どの部分がマイナス要因となったのかを確認できます。 以下の例では、右側の画像は予測にプラスに影響した部分を示し、左側の画像は結果にマイナスの影響があった部分を示しています。

- {{site.data.keyword.pm_full}} の場合、機械学習ゲートウェイ経由で送信される摂動済みのイメージのペイロードは、1 MB を超えることはできません。 タイムアウトの問題を避けるには、イメージは 125 x 125 ピクセルを超えてはならず、最初のものが完了してから 2 番目のイメージの説明が要求されるように、順次送信される必要があります。
{: note}

![説明性の画像分類](images/insight-explain-image.png)

## 非構造化テキスト・モデルの例
{: #ie-unstruct}

最後に、この説明性の例で、非構造化テキストを評価する分類モデルを示します。 この説明は、モデル予測に対してプラスおよびマイナスの影響があったキーワードを示します。 また、モデルへの入力情報として提供された元のテキストの中で、識別されたキーワードの位置も表示されています。

![説明性の画像分類](images/insight-explain-text.png)
