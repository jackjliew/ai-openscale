---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 非構造化テキスト・モデルの説明
{: #ie-unstruct}

{{site.data.keyword.aios_short}} は、非構造化テキスト・データの説明性をサポートします。
{: shortdesc}

## 非構造化テキスト・モデルの処理
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

## 非構造化テキストのトランザクションの説明
{: #ie-unstruct-xplan}

次の説明性の例は、非構造化テキストを評価する分類モデルを示しています。この説明は、モデル予測に対してプラスおよびマイナスの影響があったキーワードを示します。 また、モデルへの入力情報として提供された元のテキストの中で、識別されたキーワードの位置も表示されています。

![説明性画像分類グラフが表示されています。このグラフには、非構造化テキストの確信度レベルが表示されています。](images/insight-explain-text.png)

## 非構造化テキスト・モデルの例
{: #ie-unstruct-ntbkssample}

次のノートブックを使用して、詳細なコード・サンプルを確認しながら独自の {{site.data.keyword.aios_short}} デプロイメントを開発します。

- [テキスト・ベース・モデルの説明を生成するチュートリアル](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

