---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

デプロイメントごとに、特定のトランザクションについての説明性データを表示することができます。
{: shortdesc}

## トランザクションの説明
{: #ie-view}

選択したデプロイメント・タイルでナビゲーターの**「トランザクションの説明」**タブ (![「トランザクションの説明」タブ](images/insight-transact-tab.png)) を選択し、トランザクション ID を入力します。

予測のためにデータがモデルに送信されるたびに、HTTP ヘッダーの `X-Global-Transaction-Id` フィールドにトランザクション ID が設定されます。 このトランザクション ID はペイロード・テーブルに保管されます。 特定の予測のモデルの動作の説明を見つけるには、その評価要求に関連付けられたトランザクション ID を指定します。 この動作は {{site.data.keyword.pm_full}} トランザクションにのみ適用され、WML 以外のトランザクションには適用されないことに注意してください。
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

## 画像モデル
{: #ie-image}

{{site.data.keyword.aios_short}} は、画像データの説明性をサポートします。

### 画像モデルの処理
{: #ie-image-working}

1. 環境をセットアップします。
   2. {{site.data.keyword.aios_short}} パッケージと {{site.data.keyword.pm_full}} パッケージをインストールします。
   3. 資格情報を構成します。
   4. モデルの作成や分析に必要なライブラリーをインストールします。これには、次のライブラリーが含まれます。
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. 画像ベースのモデルを作成してデプロイします。
   2. 画像の分類に基づいて、画像用のフォルダーを作成します。
       - メインの `data` ディレクトリー内に、`train` と `validation` の各サブディレクトリーを作成する必要があります。
       - 各サブディレクトリー内に、独自の分類ディレクトリーを作成する必要があります。
  2. 画像のサイズを標準化し、訓練用と検証用に使用するサブディレクトリーを設定します。
  3. データを前処理してスケールを変更し、画像とそのクラスを取り出します。
  4. モデルを定義し、訓練を行います。
  5. モデルを保管します。
  6. モデルをデプロイします。

7. `APIClient` を割り当て、アセットをサブスクライブし、モデルを評価することで、{{site.data.keyword.aios_short}} を構成します。
8. 説明性を構成します。
   9. 説明性を有効にします。
   10. トランザクションの説明性を取得します。
   11. 説明された画像を表示します。 

### 画像モデルのトランザクションの説明
{: #ie-image-workingviewing}

説明性の例が画像分類モデルである場合、画像のどの部分が予測結果のプラス要因となり、どの部分がマイナス要因となったのかを確認できます。 以下の例では、プラスのペインのイメージは予測にプラスに影響した部分を示し、マイナスのペインのイメージは結果にマイナスの影響があった部分を示しています。

![説明性の画像分類](images/insight-explain-image.png)

{{site.data.keyword.pm_full}} では、ペイロード・ロギングのために送信する画像分類モデルの評価入力データは、1 MB を超えてはなりません。タイムアウトの問題を避けるには、イメージは 125 x 125 ピクセルを超えてはならず、最初のものが完了してから 2 番目のイメージの説明が要求されるように、順次送信される必要があります。
{: note}


### 画像モデルの例
{: #ie-image-working-ntbks}

次の 2 つのノートブックを使用して、詳細なコードの例を確認し、独自の {{site.data.keyword.aios_short}} デプロイメントを開発してください。

- [画像ベース・モデルの説明を生成するチュートリアル](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [画像ベース 2 項分類器モデルの説明の生成に関するチュートリアル](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}


## 非構造化テキスト・モデル
{: #ie-unstruct}

{{site.data.keyword.aios_short}} は、非構造化テキスト・データの説明性をサポートします。

### 非構造化テキスト・モデルの処理
{: #ie-unstruct-steps}

1. 環境をセットアップします。
   2. {{site.data.keyword.aios_short}} パッケージと {{site.data.keyword.pm_full}} パッケージをインストールします。
   3. 資格情報を構成します。
   4. モデルの作成や分析に必要なライブラリーをインストールします。これには、次のライブラリーが含まれます。
      - `pandas`
      - `pyspark` ({{site.data.keyword.DSX}} を使用しない場合)

1. 画像ベースのモデルを作成してデプロイします。
   2. 訓練データを pandas フレームにロードします。
   2. データを使用してモデルを訓練します。
   3. モデルをパブリッシュします。
   4. モデルをデプロイして評価します。

7. `APIClient` を割り当て、アセットをサブスクライブし、モデルを評価することで、{{site.data.keyword.aios_short}} を構成します。
8. 説明性を構成します。
   9. 説明性を有効にします。
   10. トランザクションの説明性を取得します。

### 非構造化テキストのトランザクションの説明
{: #ie-unstruct-xplan}

次の説明性の例は、非構造化テキストを評価する分類モデルを示しています。この説明は、モデル予測に対してプラスおよびマイナスの影響があったキーワードを示します。 また、モデルへの入力情報として提供された元のテキストの中で、識別されたキーワードの位置も表示されています。

![説明性の画像分類](images/insight-explain-text.png)

### 非構造化テキスト・モデルの例
{: #ie-unstruct-ntbkssample}

次のノートブックを使用して、詳細なコード・サンプルを確認しながら独自の {{site.data.keyword.aios_short}} デプロイメントを開発します。

- [テキスト・ベース・モデルの説明を生成するチュートリアル](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}
